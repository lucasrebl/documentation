# 🌿 Git Branches - Gestion des Branches et Développement Parallèle

Documentation complète sur la gestion des branches Git pour le développement collaboratif et les fonctionnalités parallèles.

![Git](https://img.shields.io/badge/Git-Branches-green?style=flat-square&logo=git&logoColor=white)

## 🌿 Concept des Branches

**Les branches** sont des lignes de développement indépendantes qui permettent de travailler sur différentes fonctionnalités ou corrections en parallèle sans affecter le code principal. Chaque branche représente un historique de commits distinct qui peut être fusionné avec d'autres branches. C'est un concept fondamental pour le travail en équipe et la gestion de versions.

### Pourquoi utiliser des branches ?
- **Isolation** : Développer des fonctionnalités sans casser le code principal
- **Collaboration** : Plusieurs développeurs peuvent travailler simultanément
- **Expérimentation** : Tester des idées sans risque
- **Organisation** : Séparer les corrections de bugs des nouvelles fonctionnalités
- **Historique clair** : Maintenir un historique de projet propre

## 📋 Gestion des Branches

**La gestion des branches** comprend leur création, navigation, et organisation. Une bonne stratégie de branches améliore significativement la productivité de l'équipe et la qualité du code.

### Lister et naviguer
```bash
git branch
```
*Liste toutes les branches locales*

```bash
git branch -a
```
*Liste toutes les branches (locales et distantes)*

```bash
git branch -r
```
*Liste uniquement les branches distantes*

```bash
git checkout nom-branche
```
*Bascule vers une branche existante*

```bash
git switch nom-branche
```
*Bascule vers une branche existante (Git 2.23+)*

### Créer des branches
```bash
git branch nouvelle-branche
```
*Crée une nouvelle branche (reste sur la branche courante)*

```bash
git checkout -b nouvelle-branche
```
*Crée et bascule vers une nouvelle branche*

```bash
git switch -c nouvelle-branche
```
*Crée et bascule vers une nouvelle branche (Git 2.23+)*

```bash
git checkout -b feature/user-auth
```
*Crée une branche avec un nom descriptif*

## 🔄 Fusion de Branches (Merge)

**La fusion (merge)** combine l'historique de deux branches en intégrant les changements d'une branche dans une autre. Il existe différents types de merge selon la situation et le résultat souhaité pour l'historique.

### Types de merge
```bash
git merge nom-branche
```
*Fusionne une branche dans la branche courante*

```bash
git merge --no-ff nom-branche
```
*Force la création d'un commit de merge (garde l'historique des branches)*

```bash
git merge --squash nom-branche
```
*Combine tous les commits de la branche en un seul commit*

```bash
git merge --ff-only nom-branche
```
*Merge seulement si possible en fast-forward*

### Gestion des conflits
```bash
# Quand un conflit survient lors d'un merge :
git status
# Éditer les fichiers en conflit manuellement
git add fichier-resolu
git commit
```
*Processus de résolution de conflits*

```bash
git merge --abort
```
*Annule un merge en cours de résolution*

```bash
git mergetool
```
*Lance un outil graphique pour résoudre les conflits*

## 🔧 Rebase - Réécriture d'Historique

**Le rebase** permet de réécrire l'historique des commits en rejouant les commits d'une branche sur une autre base. Contrairement au merge, le rebase crée un historique linéaire et plus propre, mais modifie les commits existants.

### Rebase basique
```bash
git rebase main
```
*Rebase la branche courante sur main*

```bash
git rebase main feature-branch
```
*Rebase feature-branch sur main*

```bash
git rebase --continue
```
*Continue un rebase après résolution de conflits*

```bash
git rebase --skip
```
*Ignore le commit courant lors du rebase*

```bash
git rebase --abort
```
*Annule un rebase en cours*

### Rebase interactif
```bash
git rebase -i HEAD~3
```
*Lance un rebase interactif sur les 3 derniers commits*

```bash
git rebase -i main
```
*Rebase interactif depuis main*

**Options dans le rebase interactif :**
- `pick` : Garder le commit tel quel
- `reword` : Modifier le message du commit
- `edit` : Modifier le commit (pause pour modifications)
- `squash` : Fusionner avec le commit précédent
- `drop` : Supprimer le commit

## 🗑️ Suppression de Branches

**La suppression de branches** permet de nettoyer les branches qui ne sont plus nécessaires après fusion. C'est important pour maintenir un repository organisé et éviter l'accumulation de branches obsolètes.

### Supprimer des branches locales
```bash
git branch -d nom-branche
```
*Supprime une branche locale (seulement si fusionnée)*

```bash
git branch -D nom-branche
```
*Force la suppression d'une branche locale*

```bash
git branch -d $(git branch --merged | grep -v main)
```
*Supprime toutes les branches fusionnées*

### Supprimer des branches distantes
```bash
git push origin --delete nom-branche
```
*Supprime une branche distante*

```bash
git push origin :nom-branche
```
*Syntaxe alternative pour supprimer une branche distante*

```bash
git remote prune origin
```
*Nettoie les références aux branches distantes supprimées*

## 🏷️ Tags - Marquage de Versions

**Les tags** permettent de marquer des points spécifiques dans l'historique, généralement utilisés pour les versions de release. Contrairement aux branches, les tags sont statiques et ne bougent pas.

### Créer des tags
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
git tag -a v1.0.0 commit-hash -m "Version 1.0.0"
```
*Crée un tag sur un commit spécifique*

### Gérer les tags
```bash
git show v1.0.0
```
*Affiche les informations d'un tag*

```bash
git tag -d v1.0.0
```
*Supprime un tag local*

```bash
git push origin v1.0.0
```
*Envoie un tag vers le remote*

```bash
git push origin --tags
```
*Envoie tous les tags*

```bash
git push origin --delete v1.0.0
```
*Supprime un tag distant*

## 💾 Stash - Remisage Temporaire

**Le stash** permet de sauvegarder temporairement des modifications non commitées pour pouvoir changer de branche ou effectuer d'autres opérations. C'est utile quand vous devez interrompre votre travail pour traiter quelque chose d'urgent.

### Utiliser le stash
```bash
git stash
```
*Sauvegarde les changements en cours*

```bash
git stash push -m "Message descriptif"
```
*Sauvegarde avec un message*

```bash
git stash -u
```
*Sauvegarde en incluant les fichiers non suivis*

```bash
git stash list
```
*Liste tous les stash*

### Récupérer du stash
```bash
git stash apply
```
*Applique le stash le plus récent (le garde)*

```bash
git stash pop
```
*Applique et supprime le stash le plus récent*

```bash
git stash apply stash@{2}
```
*Applique un stash spécifique*

```bash
git stash drop stash@{0}
```
*Supprime un stash spécifique*

```bash
git stash clear
```
*Supprime tous les stash*

## 🌐 Worktrees - Espaces de Travail Multiples

**Les worktrees** permettent d'avoir plusieurs copies de travail du même repository, chacune sur une branche différente. C'est utile pour travailler sur plusieurs branches simultanément sans avoir à changer de branche constamment.

### Gérer les worktrees
```bash
git worktree add ../feature-branch feature-branch
```
*Crée un nouveau worktree pour une branche*

```bash
git worktree add -b nouvelle-branche ../nouvelle-feature
```
*Crée un worktree avec une nouvelle branche*

```bash
git worktree list
```
*Liste tous les worktrees*

```bash
git worktree remove ../feature-branch
```
*Supprime un worktree*

```bash
git worktree prune
```
*Nettoie les références aux worktrees supprimés*

## 📊 Stratégies de Branches

### Git Flow
**Modèle de branches structuré pour les projets avec releases planifiées**

- `main` : Code de production stable
- `develop` : Branche d'intégration pour le développement
- `feature/*` : Nouvelles fonctionnalités
- `release/*` : Préparation des releases
- `hotfix/*` : Corrections urgentes sur la production

### GitHub Flow
**Modèle simplifié pour le déploiement continu**

- `main` : Toujours déployable
- `feature/*` : Branches de fonctionnalités courtes
- Pull Requests pour la review et merge

### GitLab Flow
**Modèle avec branches d'environnement**

- `main` : Développement
- `production` : Code en production
- `feature/*` : Fonctionnalités
- Branches par environnement (staging, production)

## 🆘 Commandes d'Urgence pour les Branches

### Récupération de commits perdus
```bash
git reflog
```
*Affiche l'historique de toutes les actions Git*

```bash
git cherry-pick commit-hash
```
*Applique un commit spécifique à la branche courante*

```bash
git branch recovery-branch commit-hash
```
*Crée une branche à partir d'un commit spécifique*

### Nettoyage et maintenance
```bash
git gc
```
*Nettoie et optimise le repository*

```bash
git fsck
```
*Vérifie l'intégrité du repository*

```bash
git branch --merged | grep -v main | xargs git branch -d
```
*Supprime toutes les branches fusionnées*

## 💡 Bonnes Pratiques pour les Branches

### Nommage des branches
```bash
# Bonnes conventions :
feature/user-authentication
bugfix/login-error
hotfix/security-patch
release/v2.1.0
experiment/new-algorithm
```

### Workflow recommandé
1. **Créer une branche** pour chaque fonctionnalité/correction
2. **Commits fréquents** avec des messages clairs
3. **Push régulier** pour sauvegarder le travail
4. **Pull Request/Merge Request** pour la review
5. **Supprimer** les branches après fusion
6. **Garder main/develop à jour** avec des pulls fréquents

### Conseils de performance
- **Branches courtes** : Évitez les branches qui vivent trop longtemps
- **Rebase régulier** : Gardez l'historique propre
- **Squash les commits** : Pour les petites corrections
- **Tests automatisés** : Sur toutes les branches importantes

---
[← Retour au guide principal](../README.md)