# Git Tutorial

 Little tutorial to easily and quickly learn Git and its commands in french
 
_N.B. : J'utilise le terme Repository, Repositories ou Repo pour dire Dépôt ou Projet en français._

- [Remote GitHub](https://help.github.com/articles/configuring-a-remote-for-a-fork/ "Remote GitHub") et [Syncing Atlassian](https://www.atlassian.com/git/tutorials/syncing "Syncing Atlassian")

## Sommaire

- [Installation](#installation)
- [Les hébergeurs git](#les-hébergeurs-git)
  - [Comparatif](#comparatif
- [Les commandes générales](#les-commandes-générales)
  - [Les commandes utiles](#les-commandes-utiles)
  - [Configuration des paramètres de git](#configuration-des-parametres-de-git)
- [Le .gitignore](#le-gitignore)
- [Fork (ou Fourcher)](#fork-ou-Fourcher)
- [Annuler un merge sur le Remote](#annuler-un-merge-sur-le-remote)
- [](#)
- [](#)
- [Lexique](#lexique)
- [Sources](#source)

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
Intégration continue | [Travis CI](https://travis-ci.org/ "Travis CI") `.travis.yml` | GitLab CI `.gitlab-ci.yml` |
 | | |
 
 ## Les commandes générales
 
 ### Commandes utiles
 
 
 
 ### Configuration des paramètres de git
 
`--global` permet d'étendre les paramètres à __tous les dépôts__ git de l'utilisateur, sans le paramètre n'affectera que le dossier où l'on se situe.
 
- Ajout du nom associé à l'hébergeur git utilisé : `git config --global user.name "MonNom"`
- Ajout du mail associé à l'hébergeur git utilisé : `git config --global user.email "mon.mail@moi.com"`
- __Push__ toutes les branches ou une seule :
  - Toutes les branches : `git config --global push.default matching`
  - Seuelement la branche courrante : `git config --global push.default simple`
 
 ### Création d'un projet
 
 Les commandes sont à réaliser dans le dossier du projet que vous souhaitez héberger et versionner.  
- Initialisation d'un projet, dans le dossier concerné : `git init` qui créera un dossier .git
- Ajout des fichiers du projet au [tracking*](#lexique) : `git add .`
- Stockage des fichiers dans la pile de modification : `git commit -am "Mon message que le commit effectué`
- Envoi de la pile de modification sur le repo hébergeur : `git push`

## Le .gitignore

Le fichier `.gitignore` permet de ne pas envoyer sur l'hébergeur les fichiers ou dossiers non souhaités, comme les dossiers des paramètres de l'IDE ou les fichiers contenant les variables d'environnement.  
Pour commenter dans le .gitignore il faut ajouter un __#__ avant le commentaire.

Prenons comme exemple cet arborescence :
```
├─ index.html
├─ .env
├─ troll.html
├─ classes
|  ├─ classe1.php
|  └─ classe2.php
├─ Test
|  ├─ test1.txt
|  └─ test1.txt
└─ MonIDE
   ├─ ide.ide
   └─ settings.ide
```

Dans cet exemple voici comment configurer le `.gitignore`pour ne pas tracker et publier certains fichiers/dossiers :
```ini
# Pour ignorer un fichier
.env
troll.html

# Pour ignorer le dossier en entier
MonIDE/

# Pour ignorer les fichiers de mon dossier
# On ajoute une étoile au chemin du dossier
Test/*
```

### Purger les fichiers et dossiers déjà hébergés mais à ignorer dans le .gitignore

Pour supprimer et ignorer un fichier/dossier qui est déjà host sur l'hébergeur et le garder en local :
- Modifier le .gitignore pour prendre en compte le fidhier/dossier à ignorer
- Supprimer le fichier distant sur le remote (vider le cache git) : `git rm -r --cached .` ou `git rm -r --cached nom-du-dossier-ou-fichier`
  - `-r` : recursive, pour spécifier de supprimer les sous-dossiers/fichiers
- Commit les changements : `git commit -am 'Suppression des fichiers du .gitignore'`
- Push sur le repo : `git push origin master`

## Fork (ou Fourcher)

![Fork logo](https://upload.wikimedia.org/wikipedia/commons/3/38/GitHub_Fork_Button.png "Fork logo")

Le __Fork__ est un principe qui permet de _copier_ le projet d'une personne sur l'hébergeur via le bouton `__Fork__`.

- [Doc GitHub Fork](https://help.github.com/articles/fork-a-repo/)
- [Doc GitHub Sync Fork](https://help.github.com/articles/syncing-a-fork/)

### Mettre à jour le projet Forked

- Cloner le repository forked en local : `git clone MonRepoACloner.com`
- Cloner le repository forked en local : `git fetch upstream`
- 
- `git clone MonRepoForked.com`
- `git remote -v	// pour voir les différents remotes associés au projet`
- `git remote add upstream LienDuRepoForked.com	// upstream ou tout autre nom pour de projet remote`
- `git remote add gitlab LienDeMonRepoGitLab.com	// gitlab = nom de mon remote sur gitlab`
- `git checkout master`
- `git merge upstream/master`
- `git push origin		// pour push sur le repo remote origin GitHub`
- `git push gitlab		// pour push sur le remote gitlab sur GitLab`

## Annuler un merge sur le Remote

Si un merge a été effectué sur une branche Remote (hébergée sur la plateforme en ligne) et que l'on souhaite revenir en arrière (au dernier commit de cette branche remote ou un autre), voici la procédure :

```shell
```

## Lexique

- Tracking : lors de la créationd'un fichier dans le projet, ce dernier n'est pas _track_. C'est à dire que lors du commit, il ne sera pas inclut puis envoyé. Pour commit un fichier/dossier, ce dernier doit être _track_.
- Remote : traduit par _distant_. Il fait référence le plus souvent aux projets hébergés. Le projet en local est considéré comme le projet d'origine et les projets hébergés comme les distants.
- Upstream : dénommination du projet hébergé d'origine, le plus souvent le projet d'origine que l'on a fork. Généralement on __Pull__ de l'upstream et on __Push__ sur le origin (Projet d'origine : upstream | Projet forké : origin).
- Fetch : permet de montrer les commits qui ont été fait depuis le dernier fetch du repository.

## Sources

- [Documentation GitHub](https://help.github.com/ "Documentation GitHub")
