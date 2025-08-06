---
title: 6 août 2025 - Premiers pas avec les Monades
date: 2025-08-06
draft: false
tags:
  - programming
  - diary
  - journal
---
Si vous avez écrit un tant soit peu de TypeScript, vous avez probablement écrit du code similaire à ceci :

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

Cela fonctionne, et c'est définitivement plus plat qu'une multitude d'ifs imbriqués. Mais c'est encore bruyant. Chaque étape est une vérification défensive, une clause de garde qui interrompt le flux. La logique métier est obscurcie par du code répétitif.

Dans la leçon d'aujourd'hui de mon parcours d'apprentissage de la Programmation Fonctionnelle (PF), j'ai appris le concept des Monades, qui pourrait résoudre ce problème que j'ai toujours eu. Le défi était de construire une monade Maybe depuis zéro.

## Partie 1 : Attendez, Pourquoi Ai-je Besoin de flatMap ?

Ma première tâche était de créer un type Maybe, qui pourrait être soit un `Just(value)` soit un `Nothing()`. J'ai décidé d'utiliser des fonctions factory simples au lieu de classes pour garder une approche fonctionnelle. Après quelques allers-retours pour bien configurer les génériques TypeScript, j'avais mes blocs de construction :

```typescript
// Une fonction qui retourne une valeur dans une boîte
const Just = <T>(value: T): Maybe<T> => ({ ... });

// Une fonction qui retourne une boîte vide
const Nothing = <T>(): Maybe<T> => ({ ... });
```

Avec celles-ci, j'ai écrit ma première fonction, `findUser`, qui retournait un `Maybe<User>`.

Pour appliquer les concepts que j'ai appris plus tôt dans mon cours de PF, j'ai currifié la fonction pour rendre mes fonctions pures. Cette partie était plutôt simple.

```typescript
// findUser est currifiée : elle prend la liste d'utilisateurs, et retourne une nouvelle fonction
// qui attend un id.
const findUser = (users: User[]) => (id: number): Maybe<User> => {
  const user = users.find((u) => u.id === id)
  // Un helper pour convertir une valeur null/undefined en Maybe
  return fromNullable(user);
}
```

Mais ensuite est venue `getStreetName`. Ma première tentative était d'utiliser simplement `.map()` pour accéder aux propriétés imbriquées. Cela semblait intuitif, mais c'était faux. J'ai fini avec un `Just` contenant `undefined`, ce qui n'était pas du tout ce que je voulais. Une propriété manquante devrait résulter en `Nothing`.

```typescript
// La mauvaise façon, utiliser map pour une opération fallible
const getStreetName_wrong = (user: User): Maybe<string> => {
  // Erreur de typage : retourne Maybe<string | undefined> au lieu de Maybe<string>
  return Just(user)
   .map(u => u.profile) // Ceci donne Maybe<Profile | undefined>
   .map(p => p?.address) // Ceci donne Maybe<Address | undefined>
   .map(a => a?.street); // Ceci donne Maybe<string | undefined>
}

// Quand appelée sur un utilisateur sans profil, ceci retourne Just(undefined), PAS Nothing() !
```

**C'était ma première erreur.**

La fonction que je passais à `map` était `user => user.profile`. Cette action pouvait échouer (c'est-à-dire, retourner `undefined`). Un `map` est pour des transformations qui sont garanties de réussir. J'avais besoin d'autre chose.

"Oh," ai-je pensé, "c'est là que `flatMap` intervient."

`flatMap` est pour chaîner des opérations qui peuvent échouer. Elle attend une fonction qui ne retourne pas une valeur simple, mais un autre `Maybe`. Cela vous permet de construire un pipeline où chaque étape peut échouer en toute sécurité sans casser toute la chaîne.

C'est là que le helper `fromNullable` intervient. Au lieu d'écrire `value ? Just(value) : Nothing()` encore et encore, je pouvais créer une fonction réutilisable qui fait exactement cela. Elle prend une valeur qui pourrait être `T | null | undefined` et l'encapsule en toute sécurité dans un `Maybe<T>`.

```typescript
const fromNullable = <T>(value: T | null | undefined): Maybe<T> => {
  if (value === null || value === undefined) {
    return Nothing();
  }
  return Just(value);
}
```

Ce petit utilitaire est la clé pour rendre le pipeline propre. Il encapsule la logique de vérification null, donc mes fonctions principales peuvent se concentrer sur la logique métier.

Ma fonction `getStreetName` a évolué d'un one-liner maladroit vers ce pipeline propre et lisible :

```typescript
const getStreetName = (user: User): Maybe<string> => {
  return Just(user)
   .flatMap(user => fromNullable(user.profile))
   .flatMap(profile => fromNullable(profile.address))
   .flatMap(address => fromNullable(address.street))
}
```

Soudainement, tout avait un sens. Mais la plus grande percée était encore à venir. La prochaine chose que je ne saisissais pas encore complètement était "Dois-je gérer le cas `Just`/`Nothing` à l'intérieur de mon `flatMap` ?"

La réponse était **non**. La logique est à l'intérieur de l'implémentation de `flatMap` elle-même. J'ai réalisé :

> "Si `findUser` retourne `Nothing()`, alors toute la chaîne retourne `Nothing()`, parce qu'appeler `flatMap` sur un objet `Nothing()` retourne directement `Nothing()`. Si l'utilisateur est trouvé, la chaîne applique les fonctions."

L'objet `Nothing` agit comme un court-circuit. Dès qu'il apparaît, le pipeline s'arrête et passe simplement le `Nothing` jusqu'à la fin. Plus d'ifs défensifs. Le système de types faisait le travail pour moi.

## Partie 2 : Utilisation Réelle des Monades avec fp-ts

Après l'avoir construit moi-même, utiliser la bibliothèque standard de l'industrie `fp-ts` s'est avéré très simple. Les noms étaient différents (`Option` au lieu de `Maybe`, `chain` au lieu de `flatMap`), mais les concepts étaient identiques.

J'ai réécrit mes fonctions, mais cette fois en me concentrant sur les rendre aussi propres et réutilisables que possible. Je suis vraiment fier de mon code final. J'avais un helper `getAddress` réutilisable, et mes fonctions `getStreetName` et `getZipCode` sont devenues des pipelines simples et déclaratifs.

```typescript
// Le pipeline final, élégant
const street = pipe(
  findUser(users)(1), // Commencer avec un Maybe<User>
  chain(getStreetName),  // Le chaîner avec une fonction qui retourne Maybe<string>
  getOrElse(() => "No street") // Sortir du monde Maybe avec une valeur par défaut
);
```

En regardant ce `pipe`, j'ai finalement compris. La monade n'est pas aussi effrayante qu'elle en a l'air. C'est un moyen d'encapsuler la logique désordonnée de vérification null dans un conteneur propre, réutilisable et sûr. Elle transforme un écran plein de clauses de garde en un pipeline droit et élégant. Et je dois dire, ça fait du bien.

## Code Final

```typescript
import * as O from "fp-ts/Option";
import { pipe } from "fp-ts/function";

// --- Données d'Exemple ---
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

// --- Fonctions FP ---
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

// --- Exécution ---
const findUserInDb = findUser(users); // Créer une fonction findUser spécifique pour notre db

// Trouver la rue pour l'Utilisateur 1
const street = pipe(
  findUserInDb(1),
  O.chain(getStreetName),
  O.getOrElse(() => "Aucune rue trouvée")
);

// Trouver le code postal pour l'Utilisateur 2 (va échouer)
const zipCode = pipe(
  findUserInDb(2),
  O.chain(getZipCode),
  O.getOrElse(() => "Aucun code postal trouvé")
)

console.log(`Rue de l'utilisateur 1 : ${street}`);
console.log(`Code postal de l'utilisateur 2 : ${zipCode}`);
```