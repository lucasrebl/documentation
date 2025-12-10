# 🔧 Git Advanced - Techniques Avancées et Optimisation

Documentation des fonctionnalités Git avancées pour les utilisateurs expérimentés et l'optimisation des workflows.

![Git](https://img.shields.io/badge/Git-Advanced-red?style=flat-square&logo=git&logoColor=white)

## 🔍 Recherche et Filtrage Avancés

**Les outils de recherche avancés** permettent d'analyser l'historique du projet en profondeur, de trouver des informations spécifiques et de comprendre l'évolution du code. Ces techniques sont essentielles pour le debugging, l'audit de code et la maintenance de projets complexes.

### Recherche dans l'historique
```bash
git log --grep="bug fix"
```
*Recherche dans les messages de commit*

```bash
git log --author="John Doe"
```
*Commits d'un auteur spécifique*

```bash
git log --since="2024-01-01" --until="2024-12-31"
```
*Commits dans une période donnée*

```bash
git log --oneline --graph --all --since="1 week ago"
```
*Historique graphique de la dernière semaine*

### Recherche dans le code
```bash
git log -S "function_name"
```
*Commits qui ajoutent/suppriment une chaîne de caractères (pickaxe)*

```bash
git log -G "regex_pattern"
```
*Commits qui ajoutent/suppriment selon un pattern regex*

```bash
git log -p -- file.txt
```
*Historique complet d'un fichier avec les changements*

```bash
git log --follow -- old_name.txt
```
*Suit un fichier même s'il a été renommé*

### Blame et annotation
```bash
git blame file.txt
```
*Affiche qui a modifié chaque ligne*

```bash
git blame -L 10,20 file.txt
```
*Blame sur une plage de lignes spécifique*

```bash
git blame -w file.txt
```
*Ignore les changements d'espacement*

```bash
git annotate file.txt
```
*Alternative à blame avec format différent*

## 🔄 Rebase Interactif Avancé

**Le rebase interactif** est un outil puissant pour réécrire l'historique des commits. Il permet de nettoyer, organiser et optimiser l'historique avant de le partager, créant un historique de projet plus lisible et maintenir.

### Commandes de rebase interactif
```bash
git rebase -i HEAD~5
```
*Rebase interactif sur les 5 derniers commits*

```bash
git rebase -i --root
```
*Rebase depuis le premier commit*

**Actions disponibles dans le rebase interactif :**
- `pick` (p) : Utiliser le commit tel quel
- `reword` (r) : Utiliser le commit mais modifier le message
- `edit` (e) : Utiliser le commit mais s'arrêter pour modifications
- `squash` (s) : Fusionner avec le commit précédent
- `fixup` (f) : Comme squash mais ignore le message
- `exec` (x) : Exécuter une commande shell
- `break` (b) : S'arrêter ici (pour continuer plus tard)
- `drop` (d) : Supprimer le commit
- `label` (l) : Marquer la révision courante
- `reset` (t) : Reset HEAD à un label
- `merge` (m) : Créer un commit de merge

### Techniques avancées de rebase
```bash
git rebase -i HEAD~3 --exec "npm test"
```
*Execute une commande après chaque commit*

```bash
git rebase --onto main feature~3 feature
```
*Rebase seulement les 3 derniers commits de feature sur main*

```bash
git rebase -i --autosquash HEAD~5
```
*Auto-squash les commits marqués fixup!/squash!*

## 🔧 Hooks - Automatisation

**Les hooks Git** sont des scripts qui s'exécutent automatiquement lors d'événements Git spécifiques. Ils permettent d'automatiser des tâches comme les tests, la validation de format, ou les notifications.

### Hooks côté client
```bash
# .git/hooks/pre-commit
#!/bin/sh
npm test
if [ $? -ne 0 ]; then
  echo "Tests failed. Commit aborted."
  exit 1
fi
```
*Hook pré-commit pour exécuter des tests*

```bash
# .git/hooks/commit-msg
#!/bin/sh
if ! grep -qE "^(feat|fix|docs|style|refactor|test|chore): " "$1"; then
  echo "Invalid commit message format"
  exit 1
fi
```
*Validation du format des messages de commit*

```bash
# .git/hooks/pre-push
#!/bin/sh
protected_branch='main'
current_branch=$(git symbolic-ref HEAD | sed -e 's,.*/\(.*\),\1,')

if [ $protected_branch = $current_branch ]; then
  echo "Push to main branch is not allowed"
  exit 1
fi
```
*Protection contre les push directs sur main*

### Hooks côté serveur
```bash
# hooks/update (sur le serveur)
#!/bin/sh
if [ "$1" = "refs/heads/main" ]; then
  # Vérifications supplémentaires pour main
  echo "Validating push to main..."
fi
```

## 🎭 Worktrees Avancés

**Les worktrees avancés** permettent de gérer plusieurs espaces de travail simultanés de manière plus sophistiquée, optimisant les workflows pour les projets complexes avec plusieurs branches actives.

### Gestion avancée des worktrees
```bash
git worktree add --checkout ../hotfix hotfix/critical-bug
```
*Crée un worktree avec checkout immédiat*

```bash
git worktree add --lock ../production production
```
*Crée un worktree verrouillé*

```bash
git worktree add --no-checkout ../bare-worktree main
```
*Crée un worktree sans checkout*

```bash
git worktree list --porcelain
```
*Liste détaillée des worktrees*

```bash
git worktree lock ../production
git worktree unlock ../production
```
*Verrouillage/déverrouillage d'un worktree*

### Scripts d'automatisation pour worktrees
```bash
#!/bin/bash
# Script pour créer automatiquement un worktree de feature
BRANCH_NAME=$1
WORKTREE_PATH="../worktrees/$BRANCH_NAME"

git worktree add -b "$BRANCH_NAME" "$WORKTREE_PATH" main
cd "$WORKTREE_PATH"
echo "Worktree créé dans $WORKTREE_PATH"
```

## 📊 Git Attributes et Configuration Avancée

**Les Git attributes** permettent de configurer le comportement de Git pour des fichiers ou types de fichiers spécifiques. C'est crucial pour les projets avec des besoins particuliers de traitement des fichiers.

### Fichier .gitattributes
```bash
# .gitattributes
*.txt text
*.jpg binary
*.png binary

# Normalisation des fins de ligne
* text=auto
*.bat text eol=crlf
*.sh text eol=lf

# Filters personnalisés
*.secret filter=encrypt

# Export-ignore (exclusion des archives)
tests/ export-ignore
*.test export-ignore

# Language detection override
*.m linguist-language=Objective-C
docs/* linguist-documentation
```

### Configuration avancée
```bash
git config --global core.autocrlf input
```
*Configuration des fins de ligne (Linux/Mac)*

```bash
git config --global core.autocrlf true
```
*Configuration des fins de ligne (Windows)*

```bash
git config --global merge.tool vimdiff
```
*Configuration de l'outil de merge*

```bash
git config --global rerere.enabled true
```
*Active la réutilisation automatique des résolutions de conflits*

```bash
git config --global help.autocorrect 1
```
*Auto-correction des commandes (avec délai)*

## 🔍 Debugging et Analyse Forensique

**Les techniques de debugging avancées** permettent d'identifier précisément quand et comment des bugs ont été introduits, facilitant leur résolution et la prévention de problèmes similaires.

### Git Bisect - Recherche binaire
```bash
git bisect start
git bisect bad
git bisect good v1.0
```
*Démarre une recherche binaire pour trouver un bug*

```bash
git bisect run ./test.sh
```
*Automatise le bisect avec un script de test*

```bash
git bisect reset
```
*Termine la session de bisect*

### Analyse des performances
```bash
git count-objects -vH
```
*Statistiques sur les objets du repository*

```bash
git rev-list --objects --all | sort -k 2 | uniq | grep -v "^$"
```
*Liste tous les objets dans le repository*

```bash
git verify-pack -v .git/objects/pack/pack-*.idx | sort -k 3 -nr | head -10
```
*Trouve les plus gros objets dans les packs*

### Log avancé et statistiques
```bash
git shortlog -sn
```
*Statistiques de commits par auteur*

```bash
git log --pretty=format:"%h - %an, %ar : %s" --graph
```
*Log personnalisé avec format spécifique*

```bash
git log --stat --since="1 month ago"
```
*Statistiques de changements du dernier mois*

```bash
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short
```
*Format de log personnalisé avancé*

## 🔐 Sécurité et Signature

**La signature des commits** garantit l'authenticité et l'intégrité des contributions. C'est essentiel pour les projets sensibles et la conformité aux standards de sécurité.

### Configuration GPG
```bash
gpg --gen-key
```
*Génère une nouvelle clé GPG*

```bash
gpg --list-secret-keys --keyid-format LONG
```
*Liste les clés avec leurs IDs*

```bash
git config --global user.signingkey YOUR_KEY_ID
```
*Configure la clé de signature*

```bash
git config --global commit.gpgsign true
```
*Active la signature automatique des commits*

### Signature des commits
```bash
git commit -S -m "Signed commit"
```
*Crée un commit signé*

```bash
git tag -s v1.0 -m "Signed version 1.0"
```
*Crée un tag signé*

```bash
git verify-commit HEAD
```
*Vérifie la signature d'un commit*

```bash
git log --show-signature
```
*Affiche les signatures dans le log*

## ⚡ Optimisation et Performance

**L'optimisation du repository** améliore les performances et réduit l'espace disque utilisé. C'est particulièrement important pour les gros projets avec un long historique.

### Nettoyage et optimisation
```bash
git gc --aggressive --prune=now
```
*Nettoyage agressif du repository*

```bash
git repack -ad
```
*Repack tous les objets*

```bash
git prune --expire=now
```
*Supprime les objets non référencés*

```bash
git fsck --full
```
*Vérification complète de l'intégrité*

### Optimisation des gros repositories
```bash
git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```
*Supprime un fichier de tout l'historique (⚠️ Réécrit l'historique)*

```bash
git filter-repo --path big-file.zip --invert-paths
```
*Alternative moderne à filter-branch (plus rapide)*

```bash
git clone --depth 1 https://github.com/user/repo.git
```
*Clone shallow pour économiser de l'espace*

## 🔧 Scripts et Automatisation

### Scripts utiles
```bash
#!/bin/bash
# Script de backup automatique
REPO_PATH="/path/to/repo"
BACKUP_PATH="/path/to/backup"

cd "$REPO_PATH"
git bundle create "$BACKUP_PATH/repo-$(date +%Y%m%d).bundle" --all
```

```bash
#!/bin/bash
# Script de nettoyage des branches fusionnées
git branch --merged | grep -v "\*\|main\|develop" | xargs -n 1 git branch -d
git remote prune origin
```

```bash
#!/bin/bash
# Script de déploiement automatique
if [[ $(git log HEAD..origin/main --oneline) ]]; then
    git pull origin main
    npm install
    npm run build
    systemctl restart app
fi
```

### Alias avancés
```bash
git config --global alias.graph 'log --graph --pretty=format:"%h -%d %s (%cr) <%an>"'
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

## 🆘 Récupération de Données et Situations Critiques

### Récupération avancée
```bash
git fsck --lost-found
```
*Trouve les objets perdus*

```bash
git show-branch --all
```
*Affiche toutes les branches et leurs relations*

```bash
git reflog expire --expire-unreachable=now --all
git gc --prune=now
```
*Nettoyage immédiat des objets inaccessibles*

### Reconstruction d'historique
```bash
git replace --graft <commit> <parent>
```
*Crée une relation parent-enfant artificielle*

```bash
git filter-repo --commit-callback '
  if commit.message.startswith(b"SECRET"):
    commit.message = b"REDACTED"
'
```
*Réécriture d'historique avec script Python*

---
[← Retour au guide principal](../README.md)