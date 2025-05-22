---
title: Easily Deploy Your Apps with Coolify
date: 2025-05-22
draft: false
tags:
  - deployment
description: Découvrez Coolify, et comment vous pouvez gagner BEAUCOUP de temps sur le déploiement de vos applications !
---
Salut ! Si vous êtes un développeur, un propriétaire de petite entreprise, ou simplement quelqu'un qui aime créer des choses sympas, vous connaissez ce sentiment lorsque votre application est enfin prête. Génial, n'est-ce pas ? Mais ensuite vient la partie délicate : le **déploiement**. Pour beaucoup d'entre nous, c'est là que les choses se gâtent. Les plateformes d'hébergement cloud promettent de simplifier pas mal de choses, mais nous confrontent souvent à des courbes d'apprentissage compliquées, à des factures qui ne cessent de grimper, et à cette sensation agaçante de ne pas vraiment être maître de vos projets.

**Vous en avez marre des étapes de déploiement compliquées, des coûts d'hébergement exorbitants, ou simplement de lutter pour mettre vos applications en ligne sans tracas ?** Et si vous pouviez obtenir cette expérience de déploiement ultra fluide et moderne, mais avec tout le contrôle et l'économie d'un hébergement sur votre propre serveur ?

Alors, dites bonjour à **Coolify** – une solution open-source que vous pouvez héberger vous-même, conçue spécifiquement pour rendre le déploiement de vos applications, bases de données et services incroyablement facile, même si vous débutez !

Lorsque j'ai utilisé Coolify pour la première fois, j'ai été vraiment dérouté par le peu d'étapes à suivre avant d'avoir une configuration opérationnelle. Avant de vous montrer comment l'utiliser, voyons ce qu'il peut faire pour vous, et si vous voulez l'utiliser ou non.

## Alors, qu'est-ce que Coolify exactement ?

À la base, Coolify est une **alternative open-source et auto-hébergeable aux grandes entreprises de Platform-as-a-Service (PaaS)**. Imaginez ceci : vous obtenez votre propre tableau de bord de gestion cloud que vous configurez et exécutez directement sur votre propre serveur. Au lieu de payer une grande entreprise pour gérer votre infrastructure et déployer vos applications, Coolify vous redonne le pouvoir. Vous pouvez le faire vous-même, sur du matériel que vous contrôlez totalement !

Il est conçu pour simplifier tous les aspects délicats qui accompagnent habituellement l'auto-hébergement. Il vous suffit de fournir le serveur – peut-être un serveur privé virtuel (VPS) super abordable de fournisseurs comme Hetzner ou DigitalOcean, une machine puissante que vous possédez, un minuscule Raspberry Pi, ou même un vieil ordinateur portable que vous avez sous la main. Coolify vous offre ensuite une interface géniale et facile à utiliser, ainsi que toute l'automatisation dont vous avez besoin pour déployer et gérer sans effort vos projets numériques.

## Comment Coolify opère sa magie pour un déploiement ultra facile

Le véritable génie de Coolify réside dans la façon dont il prend toutes les informations techniques complexes des opérations de serveur et les présente dans une interface web conviviale et simple. Voici comment il facilite le déploiement :

### Utilisez votre propre serveur

Avant toute chose, vous aurez besoin d'un serveur avec accès SSH. C'est là que Coolify résidera et où vos applications s'exécuteront. N'oubliez pas, Coolify ne vous _fournit pas_ le serveur ; c'est le puissant logiciel qui gère tout _dessus_.

### Installation

L'installation de Coolify sur le serveur de votre choix est étonnamment simple. Généralement, il suffit d'une seule commande, et hop ! Tous les éléments nécessaires à son tableau de bord et à ses capacités de déploiement sont mis en place.

### Gérez plusieurs VPS à la fois

Une fois Coolify installé, vous accédez à son tableau de bord web. De là, vous connectez en toute sécurité votre ou vos serveurs à Coolify à l'aide de clés SSH. Cette connexion sécurisée permet à Coolify d'automatiser les tâches et de déployer vos applications avec une facilité incroyable.

### Applications conteneurisées avec Docker

Coolify utilise des conteneurs Docker pour tous vos déploiements. C'est un ÉNORME avantage pour la simplicité ! Cela signifie que vos applications et services s'exécutent dans leurs propres environnements isolés et portables. Vous n'avez pas besoin d'être un expert Docker ; Coolify gère toute l'orchestration complexe pour vous, que vous déployiez un site web basique, une base de données complexe ou quelque chose de totalement personnalisé.

### Déploiement simplifié et CI/CD

- **Intégration Git (Push-to-Deploy !) :** Vous pouvez lier vos dépôts Git (de GitHub, GitLab, Bitbucket, Gitea, etc.). Ensuite, Coolify peut automatiquement construire et déployer votre application chaque fois que vous poussez du nouveau code vers une branche spécifique. Fini les connexions manuelles aux serveurs ou les scripts compliqués – poussez simplement votre code, et Coolify fait le reste !
   
- **Services en un clic :** Pour les applications et bases de données populaires (comme WordPress, PostgreSQL, Redis, MongoDB, etc.), Coolify propose des options de déploiement "en un clic". Sérieusement, vous pouvez avoir un service entièrement configuré en quelques minutes, sans aucune configuration manuelle fastidieuse.
   
- **Images Docker personnalisées :** Vous avez une image Docker spécifique pour votre application ? Donnez simplement le nom de l'image à Coolify, et il la téléchargera et l'exécutera pour vous. C'est un jeu d'enfant !
   

Les services peuvent être un composant unique, ou être plutôt complexes, comme la version auto-hébergée de Supabase qui nécessite 7 ou 8 conteneurs différents pour fonctionner correctement. Avec Coolify, la configuration de Supabase ne prend que quelques clics.

### Essentiels automatisés

Coolify gère toutes ces tâches cruciales qui bloquent souvent les débutants :

- **Certificats SSL gratuits :** Il obtient et renouvelle automatiquement ces importants certificats SSL Let's Encrypt pour vos noms de domaine personnalisés. Cela signifie des connexions HTTPS sécurisées sans que vous ayez à lever le petit doigt !
   
- **Gestion de domaine :** Vous pouvez facilement attribuer vos noms de domaine personnalisés à vos applications déployées directement depuis le tableau de bord Coolify.
   
- **Sauvegardes automatiques :** Configurez des sauvegardes automatiques de vos bases de données vers un stockage compatible S3. Bonjour, la tranquillité d'esprit ! Vos données sont en sécurité.
   
- **Surveillance :** Obtenez des vérifications de base sur les ressources de votre serveur et la santé de vos applications, avec des options d'alertes si quelque chose tourne mal.
   

Cette approche super simplifiée et automatisée signifie que vous passez beaucoup moins de temps sur la configuration ennuyeuse du serveur et beaucoup plus de temps sur ce que vous aimez vraiment : construire et améliorer vos projets !

## Exemple : Mettre en place un serveur Minecraft avec Coolify

Plongeons dans un exemple concret qui montre vraiment à quel point Coolify est facile : la configuration d'un serveur Minecraft ! Vous verrez avec quelle facilité vous pouvez faire fonctionner des services même complexes.

### Ce dont vous aurez besoin

- Un serveur (un VPS, une machine dédiée, etc.) avec Coolify déjà installé et prêt à l'emploi.
   
- Accès SSH à votre serveur (vous en aurez besoin pour la configuration initiale de Coolify, mais moins pour les déploiements quotidiens).
   
- Un nom de domaine (facultatif, mais cela rend la connexion beaucoup plus facile à retenir !).
   

> Je recommande personnellement d'utiliser [Hostinger](https://hostinger.fr/?REFERRALCODE=AG8ROTOURI3W "null") comme fournisseur de VPS. Des machines solides, aucun problème après plus d'un an d'utilisation de leurs services.

### Voici les étapes

Connectez-vous à votre tableau de bord Coolify

Ouvrez simplement votre navigateur web et accédez à l'URL de votre instance Coolify (comme http://votre-ip-serveur:8000). Entrez vos identifiants d'administrateur et vous êtes connecté.

![[Pasted image 20250522102419.png]]

Créez un nouveau projet (veuillez rester organisé.)

Dans Coolify, les projets vous aident à organiser vos affaires. Cliquez sur "Projets" dans la barre latérale, puis sur "Ajouter un nouveau projet". Donnez-lui un nom, puis créez-le et sélectionnez l'environnement de production.

Ajoutez une nouvelle ressource

Rendez-vous dans votre nouveau projet (ou celui par défaut si vous avez sauté la dernière étape). Cliquez sur "Ajouter une nouvelle ressource".

Choisissez "Service" et recherchez "Minecraft".

![[Pasted image 20250522102454.png]]

Configurez les variables d'environnement

Les serveurs Minecraft ont besoin de quelques paramètres spécifiques pour fonctionner correctement. Dans la section "Variables d'environnement", vous ajouterez ceci :

- `EULA` : Ajoutez-le et mettez-le à `true`. Cela accepte automatiquement le Contrat de Licence Utilisateur Final de Minecraft lorsque le serveur démarre.
   
- `MINECRAFT_MAX_MEMORY` : Décidez de la quantité de RAM que vous souhaitez allouer à votre serveur, par exemple, `2G` pour 2 Gigaoctets. Ajustez cela en fonction de la puissance de votre serveur et du nombre d'amis qui vous rejoindront !
   
- `MINECRAFT_VERSION` : Choisissez la version exacte de Minecraft que vous souhaitez, comme `1.21.1`.
   
- Vous pouvez même ajouter d'autres variables ici pour ajuster les propriétés du serveur, et potentiellement configurer des mods si vous le souhaitez. Consultez la documentation !
   

Configurez le stockage persistant

Cette étape est SUPER importante ! Vous voulez absolument que les données de votre monde Minecraft (toutes vos constructions, la progression des joueurs, tout !) restent même si le serveur redémarre ou se met à jour. Dans la section "Volumes", ajoutez un nouveau volume.

> Une minute... En fait, Coolify a déjà créé les volumes pour nous. Rien à faire ici !

Configurez les ports

Les serveurs Minecraft utilisent généralement le port 25565. Je ne recommanderais pas de le modifier si vous n'êtes pas habitué à configurer le mappage des ports.

Attribuez un domaine (facultatif, mais beaucoup plus facile à retenir) :

Dans la section "Général > Services", vous pouvez ajouter votre propre nom de domaine personnalisé ou un sous-domaine (comme minecraft.votredomaine.com). Coolify gérera automatiquement le certificat SSL pour ce domaine, le gardant sécurisé et facilitant grandement la mémorisation de la connexion pour les joueurs. Si vous n'avez pas de domaine, pas de soucis, les joueurs peuvent toujours se connecter en utilisant l'adresse IP de votre serveur et le port.

Déployez votre serveur Minecraft

Une fois que tout semble bon, cliquez sur le bouton "Déployer" ! Coolify gérera alors tout : le téléchargement de l'image Docker, la configuration du conteneur avec tous vos paramètres choisis, et le démarrage du serveur Minecraft. Vous pouvez même consulter les journaux de déploiement directement dans le tableau de bord Coolify.

Connectez-vous à votre serveur (Il est temps de jouer !)

Après un déploiement réussi, votre serveur Minecraft sera en ligne ! Vos amis pourront se connecter en utilisant votre domaine fantaisie (par exemple, minecraft.votredomaine.com) ou l'adresse IP de votre serveur suivie du port (par exemple, votre-ip-serveur:25565).