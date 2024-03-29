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
