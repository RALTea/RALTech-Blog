---
title: August 6th, 2025 - Getting started with monads
date: 2025-08-06
draft: false
tags:
  - programming
  - diary
  - journal
slug: getting-started-with-monads
---

If you've written any amount of TypeScript, you probably have written code similar to this:

```typescript
function getUsersZipCode(id: number): string | null {
  const user = users.find(u => u.id === id);
  if (!user) {
    return null;
  }

  if (!user.profile || !user.profile.address) {
    return null;
  }

  return user.profile.address.zipCode || null;
}
```

This works, and it's definitely flatter than a bunch of nested ifs. But it's still noisy. Each step is a defensive check, a guard clause that interrupts the flow. The core logic is obscured by boilerplate.

In today's lesson on my journey to learn Functional Programming (FP), I learnt about the concept of Monads, that might fix this issue I always had. The challenge was to build a Maybe monad from scratch.

## Part 1: Wait, Why Do I Need flatMap?

My first task was to create a Maybe type, which could be either a `Just(value)` or a `Nothing()`. I decided to use simple factory functions instead of classes to keep things feeling functional. After some back-and-forth on getting the TypeScript generics right, I had my building blocks:

```typescript
// A function that returns a value inside a box
const Just = <T>(value: T): Maybe<T> => ({ ... });

// A function that returns an empty box
const Nothing = <T>(): Maybe<T> => ({ ... });
```

With these, I wrote my first function, `findUser`, which returned a `Maybe<User>`.

To apply concepts I learnt about earlier in my FP course, I curried the function to make my functions pure. This part was rather straightforward.

```typescript
// findUser is curried: it takes the user list, and returns a new function
// that is waiting for an id.
const findUser = (users: User[]) => (id: number): Maybe<User> => {
  const user = users.find((u) => u.id === id)
  // A helper to convert a null/undefined value into a Maybe
  return fromNullable(user);
}
```

But then came `getStreetName`. My first attempt was to just use `.map()` to access the nested properties. This felt intuitive, but it was wrong. I ended up with a `Just` containing `undefined`, which wasn't what I wanted at all. A missing property should result in `Nothing`.

```typescript
// The wrong way, using map for a fallible operation
const getStreetName_wrong = (user: User): Maybe<string> => {
  // Typing error: returning Maybe<string | undefined> instead of Maybe<string>
  return Just(user)
   .map(u => u.profile) // This gives Maybe<Profile | undefined>
   .map(p => p?.address) // This gives Maybe<Address | undefined>
   .map(a => a?.street); // This gives Maybe<string | undefined>
}

// When called on a user with no profile, this returns Just(undefined), NOT Nothing()!
```

**This was my first mistake.**

The function I was passing to `map` was `user => user.profile`. This action could fail (i.e., return `undefined`). A `map` is for transformations that are guaranteed to succeed. I needed something else.

"Oh," I thought, "so that's where `flatMap` comes in."

`flatMap` is for chaining operations that might fail. It expects a function that returns not a plain value, but another `Maybe`. This lets you build a pipeline where each step can safely fail without breaking the whole chain.

This is where the `fromNullable` helper comes in. Instead of writing `value ? Just(value) : Nothing()` over and over, I could create a reusable function that does exactly that. It takes a value that could be `T | null | undefined` and safely wraps it in a `Maybe<T>`.

```typescript
const fromNullable = <T>(value: T | null | undefined): Maybe<T> => {
  if (value === null || value === undefined) {
    return Nothing();
  }
  return Just(value);
}
```

This little utility is the key to making the pipeline clean. It encapsulates the null-checking logic, so my main functions can focus on the business logic.

My `getStreetName` function evolved from a clunky one-liner into this clean, readable pipeline:

```typescript
const getStreetName = (user: User): Maybe<string> => {
  return Just(user)
   .flatMap(user => fromNullable(user.profile))
   .flatMap(profile => fromNullable(profile.address))
   .flatMap(address => fromNullable(address.street))
}
```

Suddenly, it all made sense. But the biggest breakthrough was yet to come. The next thing I did not fully grasp yet was "Do I have to handle the `Just`/`Nothing` case inside my `flatMap`?"

The answer was **no**. The logic is inside the implementation of `flatMap` itself. I realized:

> "If `findUser` returns `Nothing()`, then the whole chain returns `Nothing()`, because calling `flatMap` on a `Nothing()` object returns directly `Nothing()`. If the user is found, the chain applies the functions."

The `Nothing` object acts as a short-circuit. The moment it appears, the pipeline stops and just passes the `Nothing` down to the end. No more defensive ifs. The type system was doing the work for me.

## Part 2: Actual use of Monads with fp-ts

After building it myself, using the industry-standard `fp-ts` library felt very straightforward. The names were different (`Option` instead of `Maybe`, `chain` instead of `flatMap`), but the concepts were identical.

I rewrote my functions, but this time with a focus on making them as clean and reusable as possible. I'm really proud of my final code. I had a reusable `getAddress` helper, and my `getStreetName` and `getZipCode` functions became simple, declarative pipelines.

```typescript
// The final, elegant pipeline
const street = pipe(
  findUser(users)(1), // Start with a Maybe<User>
  chain(getStreetName),  // Chain it with a function that returns Maybe<string>
  getOrElse(() => "No street") // Exit the Maybe world with a default value
);
```

Looking at that `pipe`, I finally understood. The monad isn't as scary as it sounds. It's a way to wrap up the messy logic of null-checking into a clean, reusable, and safe container. It turns a screen full of guard clauses into a straight, elegant pipeline. And I have to say, it feels pretty great.

## Final Code

```typescript
import * as O from "fp-ts/Option";
import { pipe } from "fp-ts/function";

// --- Sample Data ---
type User = {
  id: number;
  name: string;
  profile?: {
    address?: {
      street?: string;
      zipCode?: string;
    }
  }
};

const users: User[] = [
  { id: 1, name: 'Alice', profile: { address: { street: '123 Main St', zipCode: '10001' } } },
  { id: 2, name: 'Bob', profile: {} },
  { id: 3, name: 'Charlie' }
];

// --- FP Functions ---
const findUser = (users: User[]) => (id: number): O.Option<User> => {
  return O.fromNullable(users.find(user => user.id === id));
}

const getAddress = (user: User): O.Option<{ street?: string; zipCode?: string; }> => {
  return pipe(
    O.fromNullable(user.profile),
    O.chain(profile => O.fromNullable(profile.address)),
  )
}

const getStreetName = (user: User): O.Option<string> => {
  return pipe(
    getAddress(user),
    O.chain(address => O.fromNullable(address.street)),
  )
}

const getZipCode = (user: User): O.Option<string> => {
  return pipe(
    getAddress(user),
    O.chain(address => O.fromNullable(address.zipCode)),
  );
}

// --- Execution ---
const findUserInDb = findUser(users); // Create a specific findUser function for our db

// Find street for User 1
const street = pipe(
  findUserInDb(1),
  O.chain(getStreetName),
  O.getOrElse(() => "No street found")
);

// Find zip for User 2 (will fail)
const zipCode = pipe(
  findUserInDb(2),
  O.chain(getZipCode),
  O.getOrElse(() => "No zip code found")
)

console.log(`User 1's street: ${street}`);
console.log(`User 2's zip code: ${zipCode}`);
```