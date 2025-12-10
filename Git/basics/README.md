# 🎯 Git Basics - Configuration et Commandes de Base

Documentation des commandes Git essentielles pour débuter avec le contrôle de version.

![Git](https://img.shields.io/badge/Git-Basics-orange?style=flat-square&logo=git&logoColor=white)

## 🎯 Configuration Initiale

**La configuration initiale** de Git est essentielle pour identifier vos contributions dans l'historique des projets. Ces paramètres sont utilisés pour chaque commit que vous créez et permettent de vous reconnaître en tant qu'auteur des modifications.

### Première configuration
```bash
git config --global user.name "Votre Nom"
```
*Configure votre nom d'utilisateur globalement*

```bash
git config --global user.email "votre.email@example.com"
```
*Configure votre adresse email globalement*

```bash
git config --list
```
*Affiche toutes les configurations actuelles*

## 🆕 Création et Initialisation

**L'initialisation d'un repository** transforme un dossier ordinaire en repository Git, permettant de suivre l'historique des modifications. Vous pouvez soit créer un nouveau projet, soit cloner un projet existant depuis un service comme GitHub.

### Initialiser un repository
```bash
git init
```
*Initialise un nouveau repository Git dans le dossier courant*

```bash
git init nom-du-projet
```
*Crée un nouveau dossier avec un repository Git initialisé*

### Cloner un repository existant
```bash
git clone https://github.com/utilisateur/repo.git
```
*Clone un repository depuis GitHub/GitLab*

```bash
git clone https://github.com/utilisateur/repo.git nom-local
```
*Clone un repository en le renommant localement*

## 📊 État et Suivi

**Le suivi de l'état** vous permet de comprendre quels fichiers ont été modifiés, ajoutés ou supprimés depuis le dernier commit. C'est essentiel pour savoir où vous en êtes dans votre travail et quelles modifications vous voulez inclure dans votre prochain commit.

### Vérifier l'état du repository
```bash
git status
```
*Affiche l'état des fichiers (modifiés, ajoutés, supprimés)*

```bash
git status -s
```
*Affiche un résumé court de l'état des fichiers*

### Voir les différences
```bash
git diff
```
*Affiche les modifications non indexées*

```bash
git diff --staged
```
*Affiche les modifications indexées (prêtes à être commitées)*

```bash
git diff HEAD
```
*Affiche toutes les modifications depuis le dernier commit*

## ➕ Ajout et Indexation

**L'indexation (staging)** est le processus de sélection des modifications que vous voulez inclure dans votre prochain commit. Git utilise une zone intermédiaire appelée "index" ou "staging area" qui vous permet de préparer exactement ce que vous voulez commiter.

### Ajouter des fichiers à l'index
```bash
git add nom-fichier.txt
```
*Ajoute un fichier spécifique à l'index*

```bash
git add .
```
*Ajoute tous les fichiers modifiés à l'index*

```bash
git add *.js
```
*Ajoute tous les fichiers JavaScript à l'index*

```bash
git add -A
```
*Ajoute tous les fichiers (nouveaux, modifiés, supprimés)*

### Retirer des fichiers de l'index
```bash
git reset nom-fichier.txt
```
*Retire un fichier de l'index (garde les modifications)*

```bash
git reset
```
*Retire tous les fichiers de l'index*

## 💾 Commits

**Les commits** sont des instantanés de votre projet à un moment donné. Chaque commit enregistre l'état de tous les fichiers indexés avec un message descriptif. Les commits forment l'historique de votre projet et permettent de revenir à des versions antérieures.

### Créer des commits
```bash
git commit -m "Message de commit"
```
*Crée un commit avec un message*

```bash
git commit -am "Message de commit"
```
*Ajoute tous les fichiers modifiés et crée un commit*

```bash
git commit --amend -m "Nouveau message"
```
*Modifie le message du dernier commit*

```bash
git commit --amend --no-edit
```
*Ajoute des changements au dernier commit sans changer le message*

## 📝 Historique

**L'historique des commits** vous permet de voir l'évolution de votre projet dans le temps. Vous pouvez consulter qui a fait quoi, quand, et comprendre les changements apportés. C'est un outil puissant pour comprendre l'évolution d'un projet.

### Consulter l'historique
```bash
git log
```
*Affiche l'historique complet des commits*

```bash
git log --oneline
```
*Affiche l'historique en format condensé*

```bash
git log --graph --oneline --all
```
*Affiche un graphique de l'historique de toutes les branches*

```bash
git log -p
```
*Affiche l'historique avec les différences de chaque commit*

```bash
git show
```
*Affiche les détails du dernier commit*

```bash
git show commit-hash
```
*Affiche les détails d'un commit spécifique*

## ⏪ Annulation et Correction

**L'annulation de changements** est une fonctionnalité cruciale qui vous permet de corriger des erreurs ou de revenir en arrière. Git offre plusieurs niveaux d'annulation selon que vos changements sont non indexés, indexés, ou déjà commitées.

### Annuler des changements
```bash
git checkout -- nom-fichier.txt
```
*Annule les modifications d'un fichier non indexé*

```bash
git checkout .
```
*Annule toutes les modifications non indexées*

```bash
git restore nom-fichier.txt
```
*Restaure un fichier (Git 2.23+)*

```bash
git restore --staged nom-fichier.txt
```
*Retire un fichier de l'index*

### Revenir en arrière
```bash
git reset --soft HEAD~1
```
*Annule le dernier commit (garde les changements indexés)*

```bash
git reset --mixed HEAD~1
```
*Annule le dernier commit (garde les changements non indexés)*

```bash
git reset --hard HEAD~1
```
*Annule le dernier commit (supprime tous les changements)*

```bash
git revert commit-hash
```
*Crée un nouveau commit qui annule un commit spécifique*

## 🔍 Recherche et Debugging

**Les outils de recherche** vous permettent de trouver des informations spécifiques dans votre projet et son historique. Le debugging aide à identifier qui a modifié quoi et quand, ce qui est essentiel pour comprendre l'origine de bugs ou de changements.

### Rechercher dans l'historique
```bash
git grep "texte-recherché"
```
*Recherche du texte dans les fichiers du repository*

```bash
git log --grep="message"
```
*Recherche dans les messages de commit*

```bash
git log -S "fonction()"
```
*Recherche les commits qui ajoutent/suppriment du code*

### Debugging
```bash
git blame nom-fichier.txt
```
*Affiche qui a modifié chaque ligne d'un fichier*

```bash
git bisect start
```
*Lance une recherche binaire pour trouver un bug*

## ⚙️ Configuration Avancée

**Les alias et configurations** permettent de personnaliser Git selon vos préférences et d'accélérer votre workflow. Vous pouvez créer des raccourcis pour les commandes fréquemment utilisées et configurer le comportement par défaut de Git.

### Alias utiles
```bash
git config --global alias.st status
```
*Crée un alias 'st' pour 'status'*

```bash
git config --global alias.co checkout
```
*Crée un alias 'co' pour 'checkout'*

```bash
git config --global alias.br branch
```
*Crée un alias 'br' pour 'branch'*

```bash
git config --global alias.unstage 'reset HEAD --'
```
*Crée un alias pour désindexer*

### Configuration utile
```bash
git config --global core.editor "code --wait"
```
*Configure VS Code comme éditeur par défaut*

```bash
git config --global init.defaultBranch main
```
*Configure 'main' comme branche par défaut*

```bash
git config --global pull.rebase true
```
*Configure le rebase automatique lors des pulls*

## 💡 Bonnes Pratiques de Base

### Messages de commit efficaces
- **Impératif présent** : "Add feature" plutôt que "Added feature"
- **Première ligne < 50 caractères** : Résumé concis
- **Ligne vide puis description** si nécessaire
- **Soyez spécifique** : Décrivez le "quoi" et le "pourquoi"

### Workflow de base recommandé
1. **Vérifiez l'état** : `git status`
2. **Voir les changements** : `git diff`
3. **Indexez sélectivement** : `git add fichier`
4. **Vérifiez avant commit** : `git diff --staged`
5. **Commitez avec un message clair** : `git commit -m "message"`

### Organisation des fichiers
```bash
# Fichier .gitignore pour exclure des fichiers
*.log
node_modules/
.env
dist/
.DS_Store
```

---
[← Retour au guide principal](../README.md)