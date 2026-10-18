# Mettre le site vitrine en ligne

Ce site est **séparé de l'application de caisse** : il a son propre projet Firebase, son propre dépôt GitHub et son propre nom de domaine. Il ne contient aucune donnée, aucun mot de passe et aucun lien vers la caisse.

## 1. Créer un projet Firebase rien que pour le site

1. Sur **console.firebase.google.com**, cliquez sur **Créer un projet** et nommez-le par exemple `chez-manou-site`.
2. N'activez **ni Firestore, ni Authentication** : le site n'en a pas besoin, et moins il y a de services, moins il y a de risques.

## 2. Modifier vos informations

Tout ce qui change souvent se trouve dans **`public/config.js`**. Ouvrez-le avec le Bloc-notes :

- **CONFIG** : numéros WhatsApp, téléphones, adresses, horaires et lien Google Maps de chaque établissement.
- **MENU** : les plats et boissons du bar-resto, avec leurs prix.
- **DEPOT** : les caisses du dépôt et leurs prix.
- **PHOTOS** : vos images. Déposez-les dans `public/photos/`, puis listez-les ici (voir `public/photos/LISEZMOI.txt`).

## 3. Envoyer en ligne

Installez **Node.js** (version LTS) depuis nodejs.org. Ouvrez un terminal dans ce dossier et tapez :

```
npm install -g firebase-tools
firebase login
firebase use --add        (choisissez chez-manou-site, puis tapez « default »)
firebase deploy
```

Le site est alors en ligne à l'adresse `https://chez-manou-site.web.app`. Après chaque modification, relancez `firebase deploy`.

## 4. Brancher votre nom de domaine

1. Dans Firebase, ouvrez **Hosting**, puis **Ajouter un domaine personnalisé**. Tapez `chezmanou.sn`, puis `www.chezmanou.sn`.
2. Ajoutez chez votre registraire les enregistrements **TXT** et **A** que Firebase vous donne.
3. Le certificat https arrive en quelques heures, parfois jusqu'à 24 h.

## Protections incluses

Elles sont configurées dans `firebase.json` :

- **Politique de sécurité du contenu (CSP)** : le site ne peut exécuter que ses propres fichiers, et ne peut envoyer aucune donnée nulle part.
- **Interdiction d'afficher le site dans une autre page**, pour empêcher les pages pièges.
- **https obligatoire** (HSTS), protection contre le reniflage de type de fichier, et navigateur privé d'accès à la caméra, au micro et à la position.
