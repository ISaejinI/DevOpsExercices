# Exercices DevOps

![Version](https://img.shields.io/github/v/release/ISaejinI/DevOpsExercices?label=version)
![Contributors](https://img.shields.io/github/contributors/ISaejinI/DevOpsExercices)
![Stars](https://img.shields.io/github/stars/ISaejinI/DevOpsExercices)
![Last commit](https://img.shields.io/github/last-commit/ISaejinI/DevOpsExercices?label=dernier%20commit)

## État des workflows

![Display Commit Message](https://github.com/ISaejinI/DevOpsExercices/actions/workflows/commit-message.yml/badge.svg)
![Generate Image and Push to Github Pages](https://github.com/ISaejinI/DevOpsExercices/actions/workflows/generate-image.yml/badge.svg)
![Add Comment on Commit](https://github.com/ISaejinI/DevOpsExercices/actions/workflows/comment-on-commit.yml/badge.svg)
![Send Discord Notification](https://github.com/ISaejinI/DevOpsExercices/actions/workflows/discord-notification.yml/badge.svg)

## Présentation

Ce projet utilise **GitHub Actions** pour générer automatiquement une image à partir du message du dernier commit envoyé sur la branche `main`.

À chaque nouveau commit, un workflow récupère le message du commit, l’envoie à l’API **DynaPictures**, télécharge l’image générée, met à jour une page `index.html`, puis déploie le contenu sur **[GitHub Pages](https://isaejini.github.io/DevOpsExercices/)**.

## Fonctionnalités

- Génération automatique d’une image à chaque commit sur `main`
- Utilisation du message du commit comme texte dans l’image
- Sauvegarde des images dans le dossier `public/images`
- Génération automatique d’une galerie HTML
- Déploiement automatique sur GitHub Pages
- Envoi d’une notification Discord après génération
- Ajout d’un commentaire sur le commit avec l’image générée
- Sauvegarde de l’image générée en artifact GitHub Actions

## Workflows GitHub Actions

### `generate-image.yml`

Ce workflow est le cœur du projet.

Il permet de :

1. récupérer le dernier message de commit ;
2. envoyer ce message à l’API DynaPictures ;
3. récupérer l’URL de l’image générée ;
4. télécharger l’image dans `public/images` ;
5. générer une page `index.html` ;
6. commit et push les fichiers générés ;
7. publier le dossier `public` sur GitHub Pages ;
8. sauvegarder l’image comme artifact.

### `discord-notification.yml`

Ce workflow se déclenche lorsque le workflow de génération d’image est terminé.

Il permet de :

1. récupérer l’artifact de l’image générée ;
2. reconstruire l’URL publique de l’image ;
3. envoyer un message dans Discord avec le message du commit et le lien vers l’image.

### `comment-on-commit.yml`

Ce workflow se déclenche également après la génération de l’image.

Il permet d’ajouter un commentaire directement sur le commit GitHub avec l’image générée.

### `commit-message.yml`

Ce workflow sert principalement à tester l’affichage du message du dernier commit.

## Structure du projet

```txt
.
├── .github/
│   └── workflows/
│       ├── generate-image.yml
│       ├── discord-notification.yml
│       ├── comment-on-commit.yml
│       └── commit-message.yml
│
├── public/
│   ├── images/
│   │   └── img-commit.jpeg
│   └── index.html
│
├── scripts/
│   └── generate-html-index.js
│
└── README.md