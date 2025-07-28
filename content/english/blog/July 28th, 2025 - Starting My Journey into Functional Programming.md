---
title: July 28th, 2025 - Starting My Journey into Functional Programming
date: 2025-07-28
draft: true
tags:
  - tag1
---

## Why starting learning FP ?
One of the main issues I encounter when building apps is the amount of small bugs that I create. No matter how much I try to test my apps, when I finally showcase my projects, I always face new bugs that I never saw before. Even behaviors that I know I tested start breaking again, and this perpetual regression is really bothering me, even if in the last few years, my apps tend to be more robust and less filled with bugs.

It feels like I'm playing a game of whack-a-mole. I'll fix a bug in the user profile section, and suddenly the payment processing logic, which I haven't touched in weeks, starts acting up. How? It's that spooky "action at a distance" that drives me crazy. A change in one part of the codebase inexplicably affects a completely different, seemingly unrelated part. My code feels fragile, like a house of cards.

## The very basics
Today, I spent a couple of hours reading about Functional Programming (FP). It wasn't the first time, but this time something clicked. The core ideas—immutability and pure functions—feel like a direct answer to my problems.

The concept of **immutability** means data doesn't change after it's created. If I need to modify something, I create a new copy with the changes. This sounds like it could eliminate that whole class of bugs where data gets unexpectedly changed by some other part of the program.

Another main concept of functional programming is **pure functions**. For a given input, they always return the same output and have no "side effects" (like modifying a global variable or writing to a database). This means they are predictable. Utterly, beautifully predictable. You can test them in a vacuum, and if they work, they'll _always_ work the same way.

## Today's conclusion
This honestly feels like the way to go. It’s not just about getting the code to work. I’m done looking like a noob when I put my tears and blood in a project. I really want to build apps that don't just work for now, but are actually tough and don't fall apart easily. So, this is it, day one. Wish me luck!