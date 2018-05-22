# Git Tutorial

 Little tutorial to easily and quickly learn Git and its commands in french
 
_N.B. : J'utilise le terme Repository ou Repo pour dire Dépôt en français._

## Sommaire

- [Installation](#installation)
- [Les hébergeurs git](#les-hébergeurs-git)
- [](#)
- [](#)
- [](#)
- [](#)

## Installation

- Installer git :
  - sur [Windows](https://git-scm.com/download/win "Installer Git for Windows")
  - sur Linux : `apt-get install git` - [Détail des commandes selon les versions Linus](https://git-scm.com/download/linux "Installation Git Linux")
  - sur [Mac](https://git-scm.com/download/mac "Installer Git for Mac")

## Les hébergeurs git

Une petite liste des hébergeurs les plus connus :  
- [GitHub](https://github.com/ "GitHub.com") - Repository public gratuit, privé payant et [gratuit pour les étudiants](https://education.github.com/ "GitHub Education Pack")
- [GitLab](https://gitlab.com/ "GitLab.com") - Repository public et privé gratuits
- [Bitbucket](https://bitbucket.org/ "Bitbucket.org") - Une très bonne [documentation git](https://www.atlassian.com/git/tutorials "Atlassian")

### Comparatif (A venir)

. | GitHub | GitLab | Bitbucket
--- | :---: | --- | :---:
Repo public | Gratuit | Gratuit |
Repo privé | Payant | Gratuit |
Intégration continue | | |
 | | |
 
 ## Les commandes
 
 ### Création d'un projet
 
 Les commandes sont à réaliser dans le dossier du projet que vous souhaitez héberger et versionner.
 - Initialisation d'un projet, dans le dossier concerné : `git init` qui créera un dossier .git
 - Configuration des paramètres de git (le --global permet d'étendre ces paramètres sur tous les repo git de l'utilisateur, sans cela n'affectera que le dossier où l'on se situe):
   - Ajout du nom associé à l'hébergeur git utilisé : `git config --global user.name "MonNom"`
   - Ajout du mail associé à l'hébergeur git utilisé : `git config --global user.email "mon.mail@moi.com"`
 - Ajout des fichiers du projet au [tracking*](#lexique) : `git add .`
 - Stockage des fichiers dans la pile de modification : `git commit -am "Mon message que le commit effectué`
 - Envoi de la pile de modification sur le repo hébergeur : `git push`

## Fork (ou Fourcher)

![Fork logo](https://upload.wikimedia.org/wikipedia/commons/3/38/GitHub_Fork_Button.png "Fork logo")

Le __Fork__ est un principe qui permet de _copier_ le projet d'une personne sur l'hébergeur via le bouton `__Fork__`

### Mettre à jour le projet Forked



## Lexique

- Tracking : Lors de la créationd'un fichier dans le projet, ce dernier n'est pas _track_. C'est à dire que lors du commit, il ne sera pas inclut puis envoyé. Pour commit un fichier/dossier, ce dernier doit être _track_.
