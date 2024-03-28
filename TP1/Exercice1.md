Mon cas est un peu spécial, je n'ai pas d'alternance et je travaille en full time sur mon projet (Cartographie de l'écosystème Web3). Cependant, j'effectue quand même un stage, au sein de la structure (We Are One, WAO) qui m'accompagne dans le développement de mon projet. Cette structure repose en partie sur un fonctionnement communautaire et décentralisé, c'est une plateforme d'innovation collective, donc une sorte d'incubateur décentralisé.
Ducoup pour l'exercice, au lieu de lister les différentes pratiques et processus (il n'y en a aucun), je vais plutôt lister tout ce que j'aimerais mettre en place pour mon projet (avec le peu de connaissances que j'ai actuellement).

## Les silots
Il n'y a pas de silots traditionnels, étand donné que que les différents projets au sein de WAO sont des entreprises à part entière.

## Les pratiques DevOps
- Automatisation des processus nécessaire à la complétion des tâches lors d'un sprint SCRUM (Definition of Done)
  - Tests unitaires & qualité/couverture du code
- Automatisation de l'organisation des repos Git
  - Chaque commit est unique et spécifique
  - Utilisation des émojis de catégorisation rapide (gitmoji)
  - Automatisation des rapports de branches (Comme sur iObeya, avec une liste des différents commits avec les émojis)
- CI/CD
- Conteneurisation : La conteneurisation sera absolument essentiel pour le projet. Le but est de décentraliser notre plateforme en exploitant des technologies de cloud décentralisé basé sur la blockchain. Ainsi, il faut d'une part rendre l'entièreté du projet modulaire et chaque service indépendant, et permettre également à chacun de ces services de tourner simplement sur n'importe quel machine.
- Jira pour la gestion globale du SI
- Jenkins pour la gestion de la chaine DevOps

## Processus de build
Processus actuel : Développement en local et versionning partiel avec Git.
Il faut mettre en place un processus d'intégration continue.

## Processus de release
Aucun

## Processus de déploiement
Le déploiement se fait à la volée, de manière un peu chaotique (il n'y a pas d'utilisateurs réels pour le moment).
Au démarrage de la beta, nous allons entamer une phase de Test & Learn en collaboration directe avec la communauté. Pour cela, il sera essentiel de mettre en place un processus de déploiement continu en environnement de production pour diminuer au maximum le Time to Market entre le feedback d'un utilisateur et le déploiement de la mise en jour.

## Moyens de test
Aucun, ils viendront automatiquement avec la mise en place du processus CI (tests unitaires à minima).



