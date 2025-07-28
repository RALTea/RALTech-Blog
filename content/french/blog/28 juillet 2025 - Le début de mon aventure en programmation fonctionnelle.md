---
title: 28 juillet 2025 - Le début de mon aventure en programmation fonctionnelle
date: 2025-07-28
draft: false
tags:
  - diary
  - programming
  - journal
---

## Pourquoi apprendre la FP ?
(FP = Functional Programming)

Un des principaux problèmes que je rencontre quand je crée des applications, c'est la quantité de petits bugs que je fais. J'ai beau tester mes applis dans tous les sens, quand je présente enfin mes projets, je tombe toujours sur de nouveaux bugs que je n'avais jamais vus. Même des fonctionnalités que je suis sûr d'avoir testées se remettent à planter, et cette régression perpétuelle commence vraiment à m'énerver, même si mes applis sont devenues plus solides et moins buguées ces dernières années.

J'ai l'impression de jouer au jeu de la taupe. Je corrige un bug dans la section du profil utilisateur, et tout à coup, la logique de paiement, que je n'ai pas touchée depuis des semaines, se met à dérailler. Comment c'est possible ? C'est cette "action à distance" fantôme qui me rend fou. Un changement dans une partie du code affecte de manière inexplicable une autre partie qui n'a rien à voir. Mon code me semble fragile, comme un château de cartes.

## Les principes fondamentaux
Aujourd'hui, j'ai passé quelques heures à lire sur la programmation fonctionnelle (PF). Ce n'était pas la première fois, mais cette fois, j'ai eu un déclic. Les idées de base — l'immuabilité et les fonctions pures — semblent être la réponse directe à mes problèmes.

Le concept d'**immuabilité** signifie que les données ne changent pas une fois qu'elles sont créées. Si j'ai besoin de modifier quelque chose, je crée une nouvelle copie avec les changements. Ça a l'air de pouvoir éliminer toute cette catégorie de bugs où les données sont modifiées à notre insu par une autre partie du programme.

L'autre concept principal de la programmation fonctionnelle, ce sont les **fonctions pures**. Pour une même entrée, elles retournent toujours la même sortie et n'ont pas d'"effets de bord" (comme modifier une variable globale ou écrire dans une base de données). Ça veut dire qu'elles sont prévisibles. Totalement, magnifiquement prévisibles. On peut les tester isolément, et si elles fonctionnent, elles fonctionneront _toujours_ de la même manière.

## Conclusion du jour
Honnêtement, j'ai l'impression que c'est la voie à suivre. J'en ai marre de passer pour un débutant alors que je mets tout mon cœur et mon énergie dans un projet. Je veux vraiment créer des applis qui ne se contentent pas de fonctionner sur le moment, mais qui sont vraiment solides et ne s'effondrent pas facilement. Alors voilà, c'est le premier jour. Souhaitez-moi bonne chance !