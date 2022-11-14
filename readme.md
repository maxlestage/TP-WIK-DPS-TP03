# TP-WIK-DPS-TP03

AJOUTER DOCKER

## CONSIGNES :

- Créer un docker-compose avec pour seul service un container basé sur le Dockerfile créé dans le TP WIK-DPS-TP02
- Augmenter le nombre de réplicas à 4 pour ce service
- Modifier le docker-compose pour ajouter un reverse-proxy (nginx), seule le reverse-proxy doit être exposé sur votre hôte - sur le port 8080
- Configurer nginx (nginx.conf) pour loadbalancer les requêtes vers le service basé sur votre image
- Modifier le code de votre API pour afficher le hostname dans les logs à chaque requête sur /ping, lancer votre
- docker-compose.yaml et observer l'effet du l'équilibrage de charge

## Choix des Technos :

- Rust : `Comme langage de programmation.`
- Actix : `Web framework pour Rust.`
- Serde : `Outil de sérialization JSON.`
- Hostname : `permet d'afficher l'host de la machine dans le programme rust`

## Lancer le projet :

Commande à lancer dans le temrinal à la racine du projet :

```rs
cargo run // Cette commande permet de lancer le projet Rust sans configurer le port (par défaut 8080).
```

```rs
export PING_LISTEN_PORT=9000 && cargo run // Le port peut-être choisi au lancement de l'app, dans le cas présent on le définit sur 9000.
```

```rs
docker compose up // Affiche l'état de l'app avec le serveur démarré, ainsi que l'action du server balancing.
```

![screenshot](https://github.com/maxlestage/TP-WIK-DPS-TP03/blob/main/Docker_balancingServer.png)

```rs
docker inspect $(docker ps -q) --format '{{.Config.User}} {{.Name}}' // Permet de visualiser l'utilisateur, dans notre cas on run avec "userapi"
```

![screenshot](https://github.com/maxlestage/TP-WIK-DPS-TP03/blob/main/Display_user.png)

### Tester l'application :

- Depuis le Terminal avec la commande curl :

```txt
curl http://127.0.0.1:9000/ping
```

- \*Depuis un Navigateur Web via le lien suivant en local :

```txt
http://127.0.0.1:9000/ping
```

\*Retourne à l'utilisateur l'affichage du header sous la forme d'un JSON dans le body

Si l'utilisateur essaie de visiter tout autres routes que `/ping`, le serveur renverra une erreur une 404, celle-ci est visible dans la console du navigateur dans l'onglet Network ou Réseau.

LESTAGE Maxime - TP DevOps n°3 - Ynov 2022.
