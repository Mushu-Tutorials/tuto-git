# Git Tutorial

 Little tutorial to easily and quickly learn Git and its commands in french
 
_N.B. : J'utilise le terme Repository, Repositories ou Repo pour dire Dépôt ou Projet en français._

- [Remote GitHub](https://help.github.com/articles/configuring-a-remote-for-a-fork/ "Remote GitHub") et [Syncing Atlassian](https://www.atlassian.com/git/tutorials/syncing "Syncing Atlassian")

## Sommaire

- [Installation](#installation)
- [Les hébergeurs git](#les-hébergeurs-git)
  - [Comparatif](#comparatif-a-venir)
- [Les commandes générales](#les-commandes-générales)
  - [Les commandes utiles](#les-commandes-utiles)
  - [Configuration des paramètres de git](#configuration-des-paramètres-de-git)
- [Le .gitignore](#le-gitignore)
- [Fork (ou Fourcher)](#fork-ou-fourcher)
- [Annuler un merge sur le Remote](#annuler-un-merge-sur-le-remote)
- [Gestion des branches](#gestion-des-branches)
  - [GitFlow](#gitflow)
- [Génération d'un CHANGELOG](#génération-d-un-changelog)
- [](#)
- [](#)
- [Lexique](#lexique)
- [Sources](#sources)

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
 
 ### Les commandes utiles
 
 - Pour voir en CLI l'arborescence des commits ([source](https://stackoverflow.com/a/7623363/7998119)) : `git log --all --graph --decorate --oneline --simplify-by-decoration`
 
 Exemple :
 
 ```git
* ae038ad (HEAD, branch2-1) add content to tmp1
| * f5a0029 (branch2-1-1) Add another
|/  
* 3e56666 (branch1) Second wave of commits
| * 6c9af2a (branch1-2) add thing
|/  
* bfcf30a (master) commit 1
 ```
 
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

## Gestion des branches

[Source](https://nickymeuleman.netlify.app/blog/delete-git-branches "Supprimer des branches")

Créer des branches :

```shell
# Création d'une branche
git branch -b <newBranch>
# Changement de branche
git checkout <branch>
# Créer et aller directement sur la branche créée
git checkout -b <newBranch>
```

Lister des branches :

```shell
# Lister l'ensemble des branches en local
git branch
# Lister l'ensemble des branches en remote
git branch -r
# Lister l'ensemble des branches en local et en remote
git branch -a

# Lister l'ensemble des branches mergées
git branch --merged
# Lister l'ensemble des branches non-mergées
git branch --no-merged
# Lister l'ensemble des branches mergées en remote
git branch -r --merged
# Lister l'ensemble des branches non-mergées en remote
git branch -r --no-merged
```

Supprimer des branches :

```shell
## En local
# Supprimer une branche mergée en local
git branch -d <branch>
# Supprimer une branche non-mergée en local
git branch -D <branch>

# Supprimer plusieurs branches en local
#   - git branch --merged            Liste toutes les branches mergées (fonctionne avec --no-merged ou sans attribut)
#   - egrep -v "(^\*|master|dev)"    Ecxlu les branches nommées "master" et "dev"
#   - xargs git branch -d            Supprime toutes les branches git restantes
git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d
git branch --no-merged | egrep -v "(^\*|master|dev)" | xargs git branch -D
git branch | egrep -v "(^\*|master|dev)" | xargs git branch -D


## En remote
# Supprimer les branches qui ne sont plus trackées et qui n'ont plus de ref entre le remote et le local
git fetch --prune
git remote prune <remote> --dry-run (commande à tester voir si elle donne le même résultat que celle au-dessus)
# Supprimer une branche en remote
git push <remote> --delete <branch>

# Supprimer plusieurs branches en remote
#   - git branch -r --merged                 Liste toutes les branches mergées (fonctionne avec --no-merged ou sans attribut)
#   - egrep -v "(^\*|master|dev)"            Ecxlu les branches nommées "master" et "dev"
#   - sed 's/origin\///'                     Cette commande renvoie des chaînes de caractères de la forme "origin/<branch>". Cela permet de filtrer "origin/"
#   - xargs -n 1 git push origin --delete    Supprime toutes les branches git restantes
git branch -r --merged | egrep -v "(^\*|master|dev)" | sed 's/origin\///' | xargs -n 1 git push origin --delete
git branch -r --no-merged | egrep -v "(^\*|master|dev)" | sed 's/origin\///' | xargs -n 1 git push origin --delete
git branch -r | egrep -v "(^\*|master|dev)" | sed 's/origin\///' | xargs -n 1 git push origin --delete
```

### GitFlow

GitFlow est une philosophie de développement utilisée par beaucoup d'entreprises permettant de gérer la gestion Git d'un Repository de manière simplifiée. Les commandes sont harmonisées et abrégées permettant un gain de temps.

- Installation : [ici](https://github.com/nvie/gitflow/wiki/Installation "Install GitFlow")

## Annuler un merge sur le Remote

Si un merge a été effectué sur une branche Remote (hébergée sur la plateforme en ligne) et que l'on souhaite revenir en arrière (au dernier commit de cette branche remote ou un autre commit), voici la procédure :

```shell
# Afin de voir l'arborescence
git log --all --graph --decorate --oneline --simplify-by-decoration
# Revenir au commit souhaité en local
git reset --hard <numero commit>
# Appliquer les changements au dépôt distant (origin)
git push origin HEAD --force
```

## Génération d'un CHANGELOG

Il est possible d'automatiser la génération d'un changelog grâce à un script Node ou d'autres outils en respectant des normes tel que [Conventionnal commits](https://www.conventionalcommits.org/ "Conventionnal commits"). Repository personnel sur le sujet disponible [ici](https://github.com/Mushu-Tutorials/tuto-git-changelogs "Automatic CHANGELOG update").

## Lexique

- Tracking : lors de la créationd'un fichier dans le projet, ce dernier n'est pas _track_. C'est à dire que lors du commit, il ne sera pas inclut puis envoyé. Pour commit un fichier/dossier, ce dernier doit être _track_.
- Remote : traduit par _distant_. Il fait référence le plus souvent aux projets hébergés. Le projet en local est considéré comme le projet d'origine et les projets hébergés comme les distants.
- Upstream : dénommination du projet hébergé d'origine, le plus souvent le projet d'origine que l'on a fork. Généralement on __Pull__ de l'upstream et on __Push__ sur le origin (Projet d'origine : upstream | Projet forké : origin).
- Fetch : permet de montrer les commits qui ont été fait depuis le dernier fetch du repository.

## Sources

- [Documentation GitHub](https://help.github.com/ "Documentation GitHub")
