---
title: Pourquoi s'intéresser à l'architecture logicielle
date: 2025-03-19
draft: true
tags:
  - "#SoftwareArchitecture"
---
# Les Défis de l'Apprentissage de l'Architecture Logicielle : Mon Parcours Personnel

Quand on parle d'architecture logicielle dans le monde académique, il existe un fossé considérable entre la théorie enseignée et la réalité du terrain. Laissez-moi vous partager mon expérience et comment ma vision a radicalement changé au fil du temps.

## Le Problème des Projets Éphémères en École

En formation, nous travaillons principalement sur des projets à court terme – quelques semaines, peut-être quelques mois. Cette temporalité ne permet jamais de ressentir les véritables douleurs d'une architecture mal pensée.

La dette technique? Les divergences avec les besoins clients? L'évolutivité du code? Ces problématiques n'ont tout simplement pas le temps d'émerger avant la fin du projet et la remise des notes.

## Le Piège du Modèle Unique

En tant que développeurs juniors, nous avons tendance à nous accrocher au premier modèle d'architecture qu'on nous présente en cours. Le problème? Ces modèles sont souvent enseignés comme des recettes à suivre, sans explication approfondie de leur raison d'être.

Je me souviens avoir considéré l'architecture logicielle comme un concept "vieux, chiant et pratiquement hors d'usage". Quelle ironie quand je pense qu'à peine quelques années plus tard, j'allais complètement changer d'avis!

## Mon Éveil à l'Architecture Logicielle

Deux problèmes majeurs m'ont fait prendre conscience de l'importance de l'architecture:

### 1. La Croissance Incontrôlable des Projets

Mes projets personnels grossissaient, et avec eux, le temps nécessaire pour implémenter de nouvelles fonctionnalités s'allongeait dramatiquement. Mes dossiers `controllers` et `services` devenaient monstrueux, rendant la navigation dans mon propre code de plus en plus laborieuse.

J'appliquais bien la séparation classique (contrôleurs, services, accès DB, middlewares) apprise en cours, mais cette approche montrait ses limites dès qu'on dépassait une dizaine de ressources différentes.

### 2. L'Impossibilité de Tester Efficacement

J'ai toujours été attiré par les tests automatisés – cette promesse de valider que tout fonctionne avant de déployer en production. Mais en pratique, je me heurtais à deux obstacles:
- Je devais constamment réécrire mes tests
- Pour le backend, je ne voyais pas l'intérêt de tester ce qui n'était essentiellement que des wrappers de base de données
- Côté frontend, sans structure claire, mes tests avec Playwright cassaient constamment

C'est cette frustration qui m'a poussé à reconsidérer complètement mon approche de l'architecture logicielle.

La suite de mon parcours m'a montré que l'architecture n'est pas qu'une question d'organisation de fichiers, mais une discipline fondamentale qui détermine la capacité d'un projet à évoluer dans le temps.