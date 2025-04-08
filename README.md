# mon-projet-docker
Projet realiser pour le tp linux.
Télécharger depuis une VM le .zip nommé mon-projet-docker.

## Description
Ce projet montre un exemple simple d'utilisation de Docker Compose pour faire communiquer deux conteneurs Docker :

- **web** : un serveur Flask exposant une route HTTP
- **client** : un script Python qui contacte le serveur `web` et affiche la réponse

## Structure du projet
```
mon-projet-docker/

├── docker-compose.yaml

├── README.md

├── web/

│   ├── app.py

│   └── Dockerfile
└── client/
    ├── script.py
    └── Dockerfile
```

## Cloner et utiliser le projet sur une autre VM

```bash
git clone [<url-du-depot>](https://github.com/fiml-123/mon-projet-docker)
cd mon-projet-docker
docker compose up --build
```

## Explication de la configuration Docker
- Chaque service est décrit dans `docker-compose.yaml`.
- Le service `web` expose le port `5000` vers l'hôte.
- Le service `client` dépend de `web` (il ne sera démarré qu'après que `web` soit prêt).
- Un réseau privé nommé `appnet` permet aux conteneurs de se retrouver par leurs noms de service (`web` et `client`).

## Communication entre les conteneurs

Docker Compose crée automatiquement un réseau virtuel et configure un DNS interne. Ainsi, le conteneur `client` peut faire des requêtes HTTP à `http://web:5000` sans besoin d'IP explicite.

## Tester le projet

1. Assurez-vous que Docker et Docker Compose sont installés sur votre machine.
2. Ouvrez un terminal dans le dossier du projet.
3. Exécutez :
   ```bash
   docker compose up --build
   ```
4. Observez les logs du conteneur `client`, il doit afficher la réponse du conteneur `web`.
5. Vous pouvez aussi tester manuellement dans un autre terminal :
   ```bash
   curl http://localhost:5000
   ```
   Cela renverra :
   ```
   Hello depuis le conteneur web !
   ```

   ## Exemple de sortie attendue
```
client_1  | Réponse du serveur web: Hello depuis le conteneur web !
```
