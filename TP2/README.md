Antoine Tessier

# 3. Execution d'un serveur Web

## a. Récupération de l'image nginx
CMD : docker pull nginx:stable-alpine3.17

## b. Vérification de l'image en local
CMD : docker images

![image](https://github.com/KaoDje/DevOpsYnovAntoine/assets/113984329/26319ffc-58fe-4d8c-8567-0e3dbe466a58)

L'image nginx est bien présente en local.

## d. Démarrage d'un container nginx qui sert la page index.html
CMD : docker run --name nginx-html -v D:\YNOV\DEVOPS\TP2\html\index.html:/usr/share/nginx/html/index.html:ro -p 8080:80 -d nginx:stable-alpine3.17

L'ajout de :ro à la fin rend le volume en lecture seule à l'intérieur du conteneur, ce qui est généralement une bonne pratique pour les fichiers statiques.

![image](https://github.com/KaoDje/DevOpsYnovAntoine/assets/113984329/eef36d5e-80b2-4721-b367-9ac66db69db9)

Index.html a bien été servi sur le port 8080 en localhost.

## e. Suppression du container 
Arrêt du container

CMD : docker kill nginx-html

![image](https://github.com/KaoDje/DevOpsYnovAntoine/assets/113984329/24f17eae-95df-47bb-9722-7a14b2b27a3a)

Suppression du container (et son volume)

CMD : docker rm -v nginx-html

## f. Démarrage d'un nouveau container sans l'option -v
Démarrage d'un container nginx vide

CMD : docker run --name nginx-html -p 8080:80 -d nginx:stable-alpine3.17

Copie du index.html dans le container

CMD : docker cp D:\YNOV\DEVOPS\TP2\html\index.html nginx-html:/usr/share/nginx/html/index.html

"Successfully copied 2.05kB to nginx-html:/usr/share/nginx/html/index.html"

![image](https://github.com/KaoDje/DevOpsYnovAntoine/assets/113984329/eef36d5e-80b2-4721-b367-9ac66db69db9)

# 4. Builder une image

## a.b. Création et exécution de l'image nginx-html
Dockerfile : 

```
FROM nginx:stable-alpine3.17
COPY ./html /usr/share/nginx/html
```

CMD : docker build -t nginx-html .

CMD : docker run -dp 8080:80 nginx-html

![image](https://github.com/KaoDje/DevOpsYnovAntoine/assets/113984329/eef36d5e-80b2-4721-b367-9ac66db69db9)

## c. Avantages et inconvénients de chaque procédure

Les questions 3 et 4 explorent deux méthodes différentes pour servir un fichier index.html. La différence clé entre ces méthodes réside dans la façon dont le fichier index.html est rendu disponible au sein du container nginx.

### Utilisation du volume (option -v) :
**Avantages :**
+ Développement et test rapides : Le fichier index.html peut être mis à jour facilement sans reconstruire ou redémarrer le container. Cette solution est idéal pendant le développement.
+ Séparation des données et de l'application : Le contenu servi peut être modifié sans modifier l'image du conteneur, ce qui favorise la réutilisabilité.

**Invonvénients :**
+ Complexité de la commande : Executer un container sans monter l'image nécessite une commande plus complexe et longue, ce qui peut favoriser les erreurs.
+ Moins portable : Le conteneur dépend du fichier index.html sur l'hôte. Pour déployer le conteneur ailleurs, il faudra également gérer le transfert du fichier index.html.

### Constrution d'une image personnalisée :
**Avantages :**
+ Portabilité : L'image contient tout le nécessaire pour servir le fichier index.html, ce qui facilite le partage ou le déploiement sur différents hôtes sans configurations supplémentaires.
+ Simplicité et clarté : Le processus de déploiement est simplifié car il ne dépend pas de fichiers externes ou de configurations spécifiques à l'hôte.

**Invonvénients :**
+ Mises à jour moins flexibles : Pour modifier le fichier index.html, il faut reconstruire et redéployer l'image, ce qui peut être plus lent que de simplement modifier un fichier sur un volume.
+ Gestion des versions : Chaque changement nécessite une nouvelle image, ce qui peut entraîner une prolifération d'images si les mises à jour sont fréquentes.

# 5. Utiliser une base de données dans un container

CMD : docker network create local-network

CMD : docker run --name mysql-container --network local-network -e MYSQL-ROOT-PASSWORD=root -d mysql:8.3.0

CMD : docker run --name phpadmin-container --network local-network -d -p 8080:80 phpmyadmin/phpmyadmin

![image](https://github.com/Devops-Dev-B-2024/DevOpsYnovAntoine/assets/113984329/edc57233-0e93-40cb-a904-6f36db8a76e0)



