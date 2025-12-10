# 🚀 Git Workflow - Méthodes et Bonnes Pratiques

Documentation des workflows Git et méthodologies pour une collaboration efficace en équipe.

![Git](https://img.shields.io/badge/Git-Workflow-purple?style=flat-square&logo=git&logoColor=white)

## 🚀 Workflows Git Populaires

**Les workflows Git** sont des méthodologies qui définissent comment une équipe utilise Git pour collaborer efficacement. Chaque workflow a ses avantages selon la taille de l'équipe, la fréquence des releases, et la complexité du projet.

### Pourquoi choisir un workflow ?
- **Structure** : Organise le travail en équipe
- **Qualité** : Impose des processus de review
- **Stabilité** : Protège les branches importantes
- **Traçabilité** : Maintient un historique clair
- **Automatisation** : Facilite l'intégration CI/CD

## 🌊 Git Flow

**Git Flow** est un workflow structuré adapté aux projets avec des cycles de release planifiés. Il utilise plusieurs types de branches pour organiser le développement, les releases et les corrections d'urgence.

### Structure des branches
```bash
main          # Production stable
develop       # Intégration du développement
feature/*     # Nouvelles fonctionnalités
release/*     # Préparation des releases
hotfix/*      # Corrections urgentes
```

### Installation et utilisation
```bash
# Installation (si non inclus avec Git)
git flow init
```
*Initialise git-flow dans le repository*

```bash
git flow feature start nouvelle-feature
```
*Crée une branche feature/nouvelle-feature*

```bash
git flow feature finish nouvelle-feature
```
*Fusionne la feature dans develop et supprime la branche*

```bash
git flow release start 1.0.0
```
*Crée une branche release/1.0.0*

```bash
git flow release finish 1.0.0
```
*Fusionne dans main et develop, crée un tag*

```bash
git flow hotfix start critical-bug
git flow hotfix finish critical-bug
```
*Workflow pour les corrections d'urgence*

### Exemple complet Git Flow
```bash
# Développement d'une nouvelle fonctionnalité
git flow feature start user-authentication
# Développement...
git add .
git commit -m "Add login form"
git commit -m "Add password validation"
git flow feature finish user-authentication

# Préparation d'une release
git flow release start 2.1.0
# Tests, corrections mineures, mise à jour de version...
git commit -m "Bump version to 2.1.0"
git flow release finish 2.1.0

# Correction d'urgence en production
git flow hotfix start security-patch
# Correction...
git commit -m "Fix security vulnerability"
git flow hotfix finish security-patch
```

## 🌐 GitHub Flow

**GitHub Flow** est un workflow simplifié basé sur les Pull Requests. Il convient aux équipes pratiquant le déploiement continu avec une branche principale toujours déployable.

### Principes de GitHub Flow
1. `main` est toujours déployable
2. Créer des branches descriptives depuis `main`
3. Push régulièrement vers la branche
4. Ouvrir une Pull Request pour discussion
5. Merger après review et tests
6. Déployer immédiatement après merge

### Workflow GitHub Flow
```bash
# 1. Créer une branche depuis main
git checkout main
git pull origin main
git checkout -b add-user-dashboard

# 2. Développement avec commits fréquents
git add .
git commit -m "Add dashboard layout"
git push -u origin add-user-dashboard

git add .
git commit -m "Add user statistics"
git push origin add-user-dashboard

# 3. Ouvrir une Pull Request sur GitHub
# (via l'interface web)

# 4. Après review et merge
git checkout main
git pull origin main
git branch -d add-user-dashboard
git push origin --delete add-user-dashboard
```

### Avantages GitHub Flow
- **Simplicité** : Facile à comprendre et adopter
- **Flexibilité** : Adapté au déploiement continu
- **Review** : Processus de review intégré
- **Historique** : Historique clair avec les PRs

## 🦊 GitLab Flow

**GitLab Flow** combine les avantages de Git Flow et GitHub Flow en ajoutant des branches d'environnement pour gérer différents stades de déploiement.

### Variantes de GitLab Flow

#### 1. GitLab Flow avec environnements
```bash
main          # Développement
staging       # Environnement de test
production    # Production
```

```bash
# Développement sur main
git checkout main
git pull origin main
git checkout -b feature/new-api
# Développement...
git push -u origin feature/new-api
# Merge Request vers main

# Déploiement vers staging
git checkout staging
git merge main
git push origin staging

# Déploiement vers production (après tests)
git checkout production
git merge staging
git push origin production
```

#### 2. GitLab Flow avec releases
```bash
main          # Développement
1-0-stable    # Branche de release
1-1-stable    # Nouvelle version
```

```bash
# Création d'une branche de release
git checkout -b 1-0-stable main
git push -u origin 1-0-stable

# Cherry-pick de corrections
git cherry-pick commit-hash
git push origin 1-0-stable
```

## 🔄 Forking Workflow

**Le Forking Workflow** est idéal pour les projets open source où les contributeurs n'ont pas d'accès direct au repository principal. Chaque développeur a son propre fork du projet.

### Configuration du Forking Workflow
```bash
# 1. Fork sur GitHub/GitLab (via l'interface)

# 2. Cloner votre fork
git clone https://github.com/votre-username/projet.git
cd projet

# 3. Ajouter le repository original comme upstream
git remote add upstream https://github.com/original-owner/projet.git

# 4. Vérifier les remotes
git remote -v
# origin    https://github.com/votre-username/projet.git (fetch)
# origin    https://github.com/votre-username/projet.git (push)
# upstream  https://github.com/original-owner/projet.git (fetch)
# upstream  https://github.com/original-owner/projet.git (push)
```

### Workflow de contribution
```bash
# 1. Synchroniser avec upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# 2. Créer une branche de feature
git checkout -b feature/improvement

# 3. Développement et push vers votre fork
git add .
git commit -m "Add improvement"
git push origin feature/improvement

# 4. Créer une Pull Request depuis votre fork
# (via l'interface web)

# 5. Maintenir la synchronisation
git fetch upstream
git checkout feature/improvement
git rebase upstream/main
git push --force-with-lease origin feature/improvement
```

## 🔄 Workflow de Release

**Les workflows de release** organisent la création et la gestion des versions de votre logiciel. Ils définissent comment passer du code en développement à une version stable déployée.

### Semantic Versioning
```bash
# Format: MAJOR.MINOR.PATCH
1.0.0   # Version initiale
1.0.1   # Correction de bug
1.1.0   # Nouvelle fonctionnalité compatible
2.0.0   # Changement majeur incompatible
```

### Workflow de release avec tags
```bash
# 1. Finaliser le développement
git checkout main
git pull origin main

# 2. Créer une branche de release
git checkout -b release/1.2.0

# 3. Préparer la release
# - Mettre à jour les numéros de version
# - Mettre à jour CHANGELOG.md
# - Tests finaux
git add .
git commit -m "Prepare release 1.2.0"

# 4. Merger dans main et develop
git checkout main
git merge release/1.2.0
git tag -a v1.2.0 -m "Release version 1.2.0"
git push origin main --tags

git checkout develop
git merge release/1.2.0
git push origin develop

# 5. Nettoyer
git branch -d release/1.2.0
git push origin --delete release/1.2.0
```

### Automated Release avec GitHub Actions
```yaml
# .github/workflows/release.yml
name: Release
on:
  push:
    tags: ['v*']

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Create Release
        uses: actions/create-release@v1
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          draft: false
          prerelease: false
```

## 🔧 Configuration d'Équipe

**La configuration d'équipe** standardise les outils et processus pour assurer une collaboration harmonieuse et maintenir la qualité du code.

### Fichiers de configuration partagés

#### .gitignore projet
```bash
# .gitignore
# Dépendances
node_modules/
__pycache__/
*.pyc

# Build
dist/
build/
*.o
*.exe

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Secrets
.env
*.key
*.pem
```

#### .editorconfig
```bash
# .editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = space
indent_size = 2

[*.py]
indent_size = 4

[*.md]
trim_trailing_whitespace = false
```

#### .gitmessage (template de commit)
```bash
# .gitmessage
# <type>(<scope>): <subject>
#
# <body>
#
# <footer>
#
# Types: feat, fix, docs, style, refactor, test, chore
# Example: feat(auth): add OAuth2 integration
```

```bash
git config --global commit.template ~/.gitmessage
```

### Hooks d'équipe partagés
```bash
# scripts/setup-hooks.sh
#!/bin/bash
ln -sf ../../scripts/pre-commit .git/hooks/pre-commit
ln -sf ../../scripts/commit-msg .git/hooks/commit-msg
chmod +x .git/hooks/pre-commit .git/hooks/commit-msg
```

## 📋 Code Review et Pull Requests

**Le processus de code review** garantit la qualité du code et facilite le partage de connaissances au sein de l'équipe. Les Pull/Merge Requests sont l'outil principal pour organiser ces reviews.

### Bonnes pratiques pour les Pull Requests

#### Création d'une PR efficace
```bash
# 1. Branche focalisée
git checkout -b fix/login-validation
# Une seule fonctionnalité ou correction par branche

# 2. Commits atomiques
git commit -m "Add email validation"
git commit -m "Add password strength check"
git commit -m "Update error messages"

# 3. Description claire
# Title: Fix login validation issues
# Description:
# - Add email format validation
# - Implement password strength requirements
# - Improve error message clarity
# - Add unit tests for validation functions
```

#### Template de Pull Request
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No console errors
```

### Processus de review
```bash
# Reviewer
git fetch origin
git checkout pr-branch-name
# Review local, tests, feedback

# Auteur (corrections après review)
git add .
git commit -m "Address review feedback"
git push origin feature-branch

# Merge après approbation
git checkout main
git pull origin main
git merge --no-ff feature-branch
git push origin main
git branch -d feature-branch
```

## 🛠️ Outils et Intégrations

### Pre-commit hooks avec tools
```bash
# Installation de pre-commit
pip install pre-commit

# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files

  - repo: https://github.com/psf/black
    rev: 23.1.0
    hooks:
      - id: black

# Installation
pre-commit install
```

### Intégration CI/CD
```yaml
# GitHub Actions example
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: |
          npm install
          npm test
          npm run build
```

## 📊 Métriques et Monitoring

### Statistiques de projet
```bash
# Contributions par auteur
git shortlog -sn

# Activité par mois
git log --format='%aN %ad' --date=format:'%Y-%m' | sort | uniq -c

# Fichiers les plus modifiés
git log --pretty=format: --name-only | sort | uniq -c | sort -rg

# Taille des commits
git log --oneline | wc -l
```

### Scripts de monitoring
```bash
#!/bin/bash
# check-repo-health.sh
echo "Repository Health Check"
echo "======================"
echo "Branches: $(git branch -a | wc -l)"
echo "Tags: $(git tag | wc -l)"
echo "Contributors: $(git shortlog -sn | wc -l)"
echo "Total commits: $(git log --oneline | wc -l)"
echo "Repository size: $(du -sh .git)"
```

## 💡 Recommandations par Type de Projet

### Projet personnel/petit équipe (1-3 devs)
- **GitHub Flow** : Simple et efficace
- **Branches courtes** : Features petites et fréquentes
- **Review optionnelle** : Selon les besoins

### Équipe moyenne (4-10 devs)
- **GitLab Flow** : Balance entre simplicité et structure
- **PR obligatoires** : Toujours reviewer le code
- **CI/CD intégré** : Tests automatiques

### Grande équipe/entreprise (10+ devs)
- **Git Flow** : Structure claire pour coordination
- **Branches par équipe** : Isolation du travail
- **Processus stricts** : Reviews multiples, tests complets

### Projet open source
- **Forking Workflow** : Contributions externes
- **Documentation** : Guidelines de contribution
- **Maintainer review** : Contrôle de qualité strict

---
[← Retour au guide principal](../README.md)