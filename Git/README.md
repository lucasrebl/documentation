# 🚀 Git - Guide des Commandes

Une documentation complète des commandes Git essentielles pour le développement quotidien.

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Version Control](https://img.shields.io/badge/Version_Control-Essential-blue?style=flat-square)

## 📖 Description

Git est un système de contrôle de version distribué qui permet de :
- Suivre l'historique des modifications de votre code
- Collaborer efficacement en équipe
- Gérer les branches et les versions de votre projet
- Revenir à des versions antérieures en cas de problème

## 🎯 Configuration Initiale

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

## 🌿 Branches

### Gestion des branches
```bash
git branch
```
*Liste toutes les branches locales*

```bash
git branch -a
```
*Liste toutes les branches (locales et distantes)*

```bash
git branch nouvelle-branche
```
*Crée une nouvelle branche*

```bash
git checkout -b nouvelle-branche
```
*Crée et bascule vers une nouvelle branche*

```bash
git switch nouvelle-branche
```
*Bascule vers une branche existante (Git 2.23+)*

```bash
git switch -c nouvelle-branche
```
*Crée et bascule vers une nouvelle branche (Git 2.23+)*

### Fusionner les branches
```bash
git merge nom-branche
```
*Fusionne une branche dans la branche courante*

```bash
git merge --no-ff nom-branche
```
*Force la création d'un commit de merge*

### Supprimer les branches
```bash
git branch -d nom-branche
```
*Supprime une branche locale (seulement si fusionnée)*

```bash
git branch -D nom-branche
```
*Force la suppression d'une branche locale*

```bash
git push origin --delete nom-branche
```
*Supprime une branche distante*

## 🔄 Synchronisation Distante

### Configurer les remotes
```bash
git remote add origin https://github.com/utilisateur/repo.git
```
*Ajoute un repository distant*

```bash
git remote -v
```
*Affiche la liste des repositories distants*

```bash
git remote rename origin nouveau-nom
```
*Renomme un remote*

### Push (envoyer)
```bash
git push
```
*Envoie les commits vers le repository distant*

```bash
git push origin main
```
*Envoie une branche spécifique vers le remote*

```bash
git push -u origin main
```
*Envoie et configure le tracking de la branche*

```bash
git push --force
```
*Force l'envoi (⚠️ Dangereux, écrase l'historique distant)*

### Pull/Fetch (récupérer)
```bash
git pull
```
*Récupère et fusionne les changements du repository distant*

```bash
git pull --rebase
```
*Récupère et rebase au lieu de merger*

```bash
git fetch
```
*Récupère les changements sans les fusionner*

```bash
git fetch origin
```
*Récupère depuis un remote spécifique*

## ⏪ Annulation et Correction

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

## 🏷️ Tags

### Gestion des tags
```bash
git tag
```
*Liste tous les tags*

```bash
git tag v1.0.0
```
*Crée un tag léger*

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```
*Crée un tag annoté avec un message*

```bash
git push origin v1.0.0
```
*Envoie un tag vers le remote*

```bash
git push origin --tags
```
*Envoie tous les tags*

## 💾 Stash (Remisage)

### Sauvegarder temporairement
```bash
git stash
```
*Sauvegarde les changements en cours*

```bash
git stash push -m "Message descriptif"
```
*Sauvegarde avec un message*

```bash
git stash list
```
*Liste tous les stash*

```bash
git stash apply
```
*Applique le stash le plus récent*

```bash
git stash pop
```
*Applique et supprime le stash le plus récent*

```bash
git stash drop stash@{0}
```
*Supprime un stash spécifique*

## 🔧 Rebase

### Rebase interactif
```bash
git rebase -i HEAD~3
```
*Lance un rebase interactif sur les 3 derniers commits*

```bash
git rebase main
```
*Rebase la branche courante sur main*

```bash
git rebase --continue
```
*Continue un rebase après résolution de conflits*

```bash
git rebase --abort
```
*Annule un rebase en cours*

## ⚙️ Configuration Avancée

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

## 🆘 Commandes d'Urgence

### En cas de problème
```bash
git reflog
```
*Affiche l'historique de toutes les actions Git (pour récupérer des commits perdus)*

```bash
git cherry-pick commit-hash
```
*Applique un commit spécifique à la branche courante*

```bash
git clean -fd
```
*Supprime tous les fichiers non suivis*

```bash
git fsck --lost-found
```
*Vérifie l'intégrité du repository*

## 📚 Bonnes Pratiques

1. **Messages de commit** : Utilisez des messages clairs et descriptifs
2. **Commits atomiques** : Un commit = une fonctionnalité/correction
3. **Branches** : Utilisez des branches pour chaque fonctionnalité
4. **Pull avant Push** : Toujours faire `git pull` avant `git push`
5. **Évitez --force** : Sauf si vous savez exactement ce que vous faites

## 🔗 Workflows Courants

### Workflow basique
```bash
git pull                    # Récupérer les derniers changements
git checkout -b feature     # Créer une branche pour votre fonctionnalité
# ... faire vos modifications ...
git add .                   # Indexer les changements
git commit -m "Add feature" # Créer un commit
git push -u origin feature  # Envoyer la branche
# ... créer une Pull Request ...
git checkout main           # Revenir sur main
git pull                    # Récupérer les derniers changements
git branch -d feature       # Supprimer la branche locale
```

### Résolution de conflits
```bash
git merge branch-name       # Conflits détectés
# ... résoudre manuellement les conflits ...
git add .                   # Marquer les conflits comme résolus
git commit                  # Finaliser le merge
```

---
*Cette documentation couvre les commandes Git les plus utilisées. N'hésitez pas à consulter `git help <commande>` pour plus de détails sur une commande spécifique.*
