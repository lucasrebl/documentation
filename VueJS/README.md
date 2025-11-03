# Création d'un projet Vue.js

Ce guide explique comment créer un nouveau projet Vue.js avec une configuration spécifique.

## Prérequis

- Node.js installé sur votre machine
- NPM (Node Package Manager)

## Étapes de création

1. Ouvrez un terminal et exécutez la commande suivante pour créer un nouveau projet Vue :
```bash
npm create vue@latest
```

2. Répondez aux questions de configuration comme suit :

- Project name (target directory): `nom-du-projet`
- Select features to include in your project:
  - TypeScript ✅
  - Router (SPA development) ✅
- Select experimental features to include in your project:
  - Oxlint ✅
- Skip all example code and start with a blank Vue project?: Yes

3. Une fois le projet créé, naviguez dans le dossier du projet et installez les dépendances :
```bash
cd nom-du-projet
npm install
```

4. Pour démarrer le serveur de développement :
```bash
npm run dev
```

## Structure du projet

### Configuration technique
Le projet est configuré avec :
- TypeScript pour un typage statique
- Vue Router pour la gestion des routes (SPA)
- Oxlint comme linter expérimental

### Arborescence des dossiers

```
nom-du-projet/
├── src/
│   ├── assets/        # Ressources statiques (images, styles, etc.)
│   ├── components/    # Composants réutilisables
│   ├── router/        # Configuration des routes
│   ├── services/      # Services et logique métier
│   ├── views/         # Pages de l'application
│   ├── App.vue        # Composant racine de l'application
│   └── main.ts        # Point d'entrée de l'application
```

### Description des dossiers et fichiers

- `assets/` : Contient toutes les ressources statiques du projet (images, styles, etc.)
- `components/` : Composants Vue réutilisables dans l'application
- `router/` : Configuration du système de routage de l'application
- `services/` : Contient la logique métier et les services de l'application
- `views/` : Composants de pages correspondant aux différentes vues de l'application
- `App.vue` : Composant principal qui sert de conteneur racine à l'application
- `main.ts` : Fichier d'initialisation de l'application Vue.js, configuration des plugins et montage de l'application