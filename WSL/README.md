# WSL c'est quoi ?

WSL vous permet d'éxécuter et d'utiliser un environnement Linux sous windows sans avoir la contrainte d'utiliser une machine virtuelle.

# installation de WSL

## Configuration requise

  - Vous devez posséder une version de Windows 10 Home, Pro ou Entreprise en 64bits
  - Vous devez posséder au minimum la mise à jour 2004 de windows

## Activer les fonctionnalité Windows

Pour installer WSL, nous avons d'abord besoins d'activer quelques fonctionalités présentes dans Windows, pour cela :

  - Ouvrez le menu démarrer de Windows
  - Ouvrez le panneau de configuration
  - Rendez-vous dans "Programmes" puis "Programmes et fonctionnalités"
  - Cliquez sur l'onglet "Activer ou désactiver des fonctionnalité Windows" sur la gauche de votre fenêtre
  - Cochez les options "Sous système Windows pour Linux" ainsi que "Plateforme d'ordinateur virtuel"
  - Redémarrez votre ordinateur

## Téléchargement de votre distribution Linux

  - Rendez-vous dans le Microsoft Store
  - Dans la barre de recherche, tapez "WSL"
  - Séléctionnez la distribution "Debian" et téléchargez la
  - Démarrez Debian
  - Ajoutez un nom d'utilisateur comme demandé (en minuscule)
  - Ajoutez votre mot de passe
  - Fermez Debian

## Migration vers WSL2

  - Téléchargez et installez ce package : https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
  - Ouvrez une invite de commande Windows (cmd.exe)
  - Entrez la commande "wsl -l", cette commande vous permet de voir les distributions installées sur votre ordinateur
  - Entrez ensuite la commande "wsl --set-version Debian 2
  - Si vous obtenez l'erreur "assurez-vous que la virtualisation est activée dans le BIOS" allez dans le BIOS de votre ordinateur et activez la virtualisation

Félicitation ! Vous avez installé WSL 2.
