# Git Tutorial

*Submodule of [about-me](https://github.com/MushuLeDragon/about-me "about-me")*

Little tutorial to easily and quickly learn Git and its commands in french

_N.B. : J'utilise le terme Repository, Repositories ou Repo pour dire Dépôt ou Projet en français._

- [Remote GitHub](https://help.github.com/articles/configuring-a-remote-for-a-fork/ 'Remote GitHub') et [Syncing Atlassian](https://www.atlassian.com/git/tutorials/syncing 'Syncing Atlassian')

## TODO

- [ ] Mettre à jour les liens sur la partie submodules `#configuration-des-paramètres-de-git`: [lien](#configuration-des-paramètres-de-git)

## Sommaire

- [Installation](#installation)
- [Hébergeurs git](#hébergeurs-git)
  - [Comparatif](#comparatif-a-venir)
- [Les commandes générales](#les-commandes-générales)
  - [Les commandes utiles](#les-commandes-utiles)
  - [Configuration des paramètres de git](#configuration-des-paramètres-de-git)
  - [Création d'un projet](#création-dun-projet)
- [Le .gitignore](#le-gitignore)
  - [Purger les fichiers et dossiers déjà hébergés mais à ignorer dans le .gitignore](#purger-les-fichiers-et-dossiers-déjà-hébergés-mais-à-ignorer-dans-le-gitignore)
- [Fork (ou Fourcher)](#fork-ou-fourcher)
  - [Mettre à jour le projet Forked](#mettre-à-jour-le-projet-forked)
- [Gestion des branches](#gestion-des-branches)
  - [Commandes générales](#commandes-générales)
    - [Créer des branches](#créer-des-branches)
    - [Lister des branches](#lister-des-branches)
    - [Renommer une branche](#renommer-une-branche)
    - [Supprimer des branches](#supprimer-des-branches)
  - [GitFlow](#gitflow)
- [Annuler un merge sur le Remote](#annuler-un-merge-sur-le-remote)
- [Gestion des submodules (en)](#gestion-des-submodules-en)
  - [Clone a repository that have submodules](#clone-a-repository-that-have-submodules)
  - [Add a submodule to the project](#add-a-submodule-to-the-project)
  - [Convert an existing folder to submodule (DEPRECATED)](#convert-an-existing-folder-to-submodule)
  - [Update a project with submodules](#update-a-project-with-submodules)
    - [Pull submodule](#pull-submodule)
    - [Push modifications for a child folder](#push-modifications-for-a-child-folder)
    - [Delete a submodule](#delete-a-submodule)
- [Génération d'un CHANGELOG](#génération-dun-changelog)
- [Héberger sur Heroku](#héberger-sur-heroku)
- [Lexique](#lexique)
- [Sources](#sources)

## Installation

- Installer git :
  - sur [Windows](https://git-scm.com/download/win 'Installer Git for Windows')
  - sur Linux : `apt-get install git` - [Détail des commandes selon les versions Linus](https://git-scm.com/download/linux 'Installation Git Linux')
  - sur [Mac](https://git-scm.com/download/mac 'Installer Git for Mac')

## Hébergeurs git

Une petite liste des hébergeurs les plus connus :

- [GitHub](https://github.com/ 'GitHub.com') - Repository public gratuit, privé payant et [gratuit pour les étudiants](https://education.github.com/ 'GitHub Education Pack')
- [GitLab](https://gitlab.com/ 'GitLab.com') - Repository public et privé gratuits
- [Bitbucket](https://bitbucket.org/ 'Bitbucket.org') - Une très bonne [documentation git](https://www.atlassian.com/git/tutorials 'Atlassian')

### Comparatif (A venir)

| .                    |                            GitHub                             | GitLab                     | Bitbucket |
| -------------------- | :-----------------------------------------------------------: | -------------------------- | :-------: |
| Repo public          |                            Gratuit                            | Gratuit                    | :-------: |
| Repo privé           |                            Payant                             | Gratuit                    | :-------: |
| Intégration continue | [Travis CI](https://travis-ci.org/ 'Travis CI') `.travis.yml` | GitLab CI `.gitlab-ci.yml` | :-------: |

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

`--global` permet d'étendre les paramètres à **tous les dépôts** git de l'utilisateur, sans le paramètre n'affectera que le dossier où l'on se situe.

- Ajout du nom associé à l'hébergeur git utilisé : `git config --global user.name "MonNom"`
- Ajout du mail associé à l'hébergeur git utilisé : `git config --global user.email "mon.mail@moi.com"`
- **Push** toutes les branches ou une seule :
  - Toutes les branches : `git config --global push.default matching`
  - Seuelement la branche courrante : `git config --global push.default simple`
- Ajout de la liste des commits des submodules (sous-modules) quand on exécute la commande `git diff` dans le dossier parent d'un submodule ([Gestion des submodules](#gestion-des-submodules-en 'Submodules')): `git config --global diff.submodule log`

### Création d'un projet

Les commandes sont à réaliser dans le dossier du projet que vous souhaitez héberger et versionner.

- Initialisation d'un projet, dans le dossier concerné : `git init` qui créera un dossier .git
- Ajout des fichiers du projet au [tracking\*](#lexique) : `git add .`
- Stockage des fichiers dans la pile de modification : `git commit -am "Mon message que le commit effectué`
- Envoi de la pile de modification sur le repo hébergeur : `git push`

## Le .gitignore

Le fichier `.gitignore` permet de ne pas envoyer sur l'hébergeur les fichiers ou dossiers non souhaités, comme les dossiers des paramètres de l'IDE ou les fichiers contenant les variables d'environnement.  
Pour commenter dans le .gitignore il faut ajouter un **#** avant le commentaire.

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

![Fork logo](https://upload.wikimedia.org/wikipedia/commons/3/38/GitHub_Fork_Button.png 'Fork logo')

Le **Fork** est un principe qui permet de _copier_ le projet d'une personne sur l'hébergeur via le bouton `__Fork__`.

- [Doc GitHub Fork](https://help.github.com/articles/fork-a-repo/)
- [Doc GitHub Sync Fork](https://help.github.com/articles/syncing-a-fork/)

### Mettre à jour le projet Forked

- Cloner le repository forked en local : `git clone MonRepoACloner.com`
- Cloner le repository forked en local : `git fetch upstream`
-
- `git clone MonRepoForked.com`
- `git remote -v // pour voir les différents remotes associés au projet`
- `git remote add upstream LienDuRepoForked.com // upstream ou tout autre nom pour de projet remote`
- `git remote add gitlab LienDeMonRepoGitLab.com // gitlab = nom de mon remote sur gitlab`
- `git checkout master`
- `git merge upstream/master`
- `git push origin // pour push sur le repo remote origin GitHub`
- `git push gitlab // pour push sur le remote gitlab sur GitLab`

## Gestion des branches

[Source](https://nickymeuleman.netlify.app/blog/delete-git-branches 'Supprimer des branches')

### Commandes générales

#### Créer des branches

```shell
# Création d'une branche
git branch -b <newBranch>
# Changement de branche
git checkout <branch>
# Créer et aller directement sur la branche créée
git checkout -b <newBranch>
```

#### Lister des branches

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

#### Renommer une branche

Suite à la nouvelle norme mise en place par GitHub, la branche **master** devient la branche **main**. Voici la procédure afin de renommer la branche master des anciens projets ([source](https://github.com/github/renaming), [predédure](https://stevenmortimer.com/5-steps-to-change-github-default-branch-from-master-to-main/)):

```shell
# Step 1 
# create main branch locally, taking the history from master
git branch -m master main

# Step 2 
# push the new local main branch to the remote repo (GitHub) 
git push -u origin main

# Step 3
# switch the current HEAD to the main branch
git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main

# Step 4
# change the default branch on GitHub to main
# https://docs.github.com/en/github/administering-a-repository/setting-the-default-branch

# Step 5
# delete the master branch on the remote
git push origin --delete master
```

#### Supprimer des branches

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

- Installation : [ici](https://github.com/nvie/gitflow/wiki/Installation 'Install GitFlow')
- Articles intéressants :
  - [Tuto et explications](https://nvie.com/posts/a-successful-git-branching-model/)
  - [GitFlow cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/index.fr_FR.html)
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

## Gestion des submodules (en)

Documentation [here](https://git-scm.com/book/fr/v2/Utilitaires-Git-Sous-modules). An kind tutorial [here](https://www.vogella.com/tutorials/GitSubmodules/article.html) by *Vogella*.

### Clone a repository that have submodules

```shell
# Shorter method
git clone --recursive [url_to_my_git_repo]
# Or git clone --recurse-submodules [url_to_my_git_repo]

# Detailed method
git clone [url_to_my_git_repo]
git submodule update --init # If no recursive submodules
git submodule update --init --recursive # If recursive submodules
```

### Add a submodule to the project

```shell
git submodule add -b <branch> [url_to_my_git_repo] <path/to/submodule>
# Options:
# -b <branch>: Branch you want to follow for this submodule. Warning: GitHub master becomes main since Oct. 2020
# <path/to/submodule>: Name of the directory you want or leave empty by default

# To initialize submodule configuration (optional)
git submodule init

# Save the tracked modifications in the parent folder
git add .
git commit -am "add submodule folder to the project"
git push
```

### Convert an existing folder to submodule

:warning::warning::warning: DEPRECATED :warning::warning::warning:

It is not recommanded to do that because there is a difference in the `.git` parent folder with the two versions. See the thread [here](https://stackoverflow.com/a/59575778/7998119).

### Update a project with submodules

1. Configure git parameters for a better vizualisation `git config --global diff.submodule log`, it lists the commits when you execute `git diff`:
2. To add ou change a following branch fora submodule: `git submodule set-branch -b <branch> [path/to/submodule]`
3. To push modifications for the parent folder, do as usual when you commit/push to remote.

```shell
# 1. Git config parameters
git diff
git config --global diff.submodule log
git diff

# 2. Set the following branch for submodule
git submodule set-branch -b <branch> [path/to/submodule]

# 3. Push from the parent folder
git add .
git commit -am "Update branch for the submodule"
git push
```

#### Pull submodule

##### Best option

From the parent folder, you can update submodules folders ([source](https://stackoverflow.com/a/1032653/7998119 "Pull submodule")):

```shell
# For git 1.8.2 or above
# Pull all changes for the submodules
git submodule update --remote <path/to/submodule>
# Add options to the command to:
# - Only update the submodule you want: git submodule update --remote <path/to/submodule>

# For git 1.7.3 or above 
# Pull all changes in the repo including changes in the submodules
git pull --recurse-submodules


# Save the tracked modifications in the parent folder
git add .
git commit -am "update submodules folders"
git push
```

##### Second option

Verify if a submodule had changements since the last pull:

```shell
cd Child_1
# Equivalent to `git pull`
git fetch # To verify modifications on this submodule
git merge # To pull modifications for this submodule (you have to push modifications from the parent folder)

cd ..
git diff
git diff --submodule

# Save the tracked modifications in the parent folder
git add .
git commit -am "update submodules folders"
git push
```

#### Push modifications for a child folder

Activate options of Git to show submodules modifications `git config status.submodulesummary 1`.

This is how to push modifications on a child folder, from the parent folder:

```shell
cd <path/to/submodule>

# Choose the branch to work to
git checkout origin # For the origin/master branch
git checkout <branch> # For a specific branch: <branch>

# Do modifications in submodule and push to the submodule's hosted repository
git add .
git commit -am "make my modifications in submodule"
git push origin HEAD:<name-of-remote-branch>

# Push from the parent folder to update the new tracked commit
cd ../<parent/folder>
git add .
git commit -am "update the submodule tracked folder from parent folder"
git push

# Save the tracked modifications in the parent folder
git add .
git commit -am "update submodules folders"
git push
```
 
### Delete a submodule

[Here](https://stackoverflow.com/a/16162000/7998119) the procedure.

```shell
# Delete the submodule
git submodule deinit <path/to/submodule>
git rm <path/to/submodule>
# Note: <path/to/submodule> (no trailing slash)
rm -rf .git/modules/<path/to/submodule>/

# Save the tracked modifications in the parent folder
git add .
git commit -am "delete submodule folder + tracking"
git push
```

## Génération d'un CHANGELOG

Cette partie est hébergée dans le projet en tant que [submodule](#gestion-des-submodules-en).

Il est possible d'automatiser la génération d'un changelog grâce à un script Node ou d'autres outils en respectant des normes tel que [Conventionnal commits](https://www.conventionalcommits.org/ 'Conventionnal commits'). Repository personnel sur le sujet disponible [ici](https://github.com/Mushu-Tutorials/tuto-git-changelogs 'Automatic CHANGELOG update').

Test lien vers le dossier : [tuto-git-changelogs](./tuto-git-changelogs)

## Héberger sur Heroku

Documentation officielle [ici](https://devcenter.heroku.com/ "Heroku").

Tuto Heroku [ici](https://github.com/MushuLeDragon/tuto-heroku-symfony).

Source pour héberger les sous-dossiers sur Heroku [ici](https://medium.com/@shalandy/deploy-git-subdirectory-to-heroku-ea05e95fce1f).

Héberger une application PHP sur Heroku :

- Vérifier que les dossiers `bin/console` et `bin/phpunit` ne sont pas **gitignore**

```shell
# Step 1
# Installer Heroku en fnction de son OS
sudo snap install heroku --classic

# Step 2
# Log to Heroku
heroku login

# Step 3
# Vérifier les prérequis : PHP, Composer, Git, Heroku
php -v
composer -V
git --version
heroku -v

# Step 4
# Aller dans le dossier du projet
cd <my-project>

# Step 5
# Créer l'application en CLI sur Heroku, le nom <application_name> est facultatif
heroku create <application_name>

# Step 6
# Configure some environments vars
heroku config:set APP_ENV=prod

# Step 7
# Création de la base de données Postgres
heroku addons:create heroku-postgresql:hobby-dev

# Step 8
# Ajout du script de compilation à composer.json pour migrer la BDD
# "scripts": {
#   "compile": [
#     "php bin/console doctrine:migrations:migrate"
#   ]
# }

# Step 9
# Configuration de  la réécriture des URL avec Apache et le fichier .htaccess
cd path/to/the/symfony/project
composer require symfony/apache-pack

# Step 10
# Configuration du fichier Procfile
# Symfony project : `echo 'web: heroku-php-apache2 public/' > Procfile`
echo 'web: heroku-php-apache2 path/to/index/folder' > Procfile
cd path/to/the/root/folder/project

# Step 11
# Sauvegarde des modifications sur le remote
git add .
git commit -am "Add Heroku configs"
git push

# Step 12
# Step 12.1
# Si le projet à host est à la racine (ATTENTION : sur GitHub la branche master est devenu la branche main)
git push heroku main
# Step 12.2
# Si le projet se situe dans un sous dossier
git subtree push --prefix path/to/subdirectory/ heroku main

# Step
# Pour voir les logs
heroku logs
heroku logs --tail
```

## Lexique

- Tracking : lors de la créationd'un fichier dans le projet, ce dernier n'est pas _track_. C'est à dire que lors du commit, il ne sera pas inclut puis envoyé. Pour commit un fichier/dossier, ce dernier doit être _track_.
- Remote : traduit par _distant_. Il fait référence le plus souvent aux projets hébergés. Le projet en local est considéré comme le projet d'origine et les projets hébergés comme les distants.
- Upstream : dénommination du projet hébergé d'origine, le plus souvent le projet d'origine que l'on a fork. Généralement on **Pull** de l'upstream et on **Push** sur le origin (Projet d'origine : upstream | Projet forké : origin).
- Fetch : permet de montrer les commits qui ont été fait depuis le dernier fetch du repository.

## Sources

- [Documentation GitHub](https://help.github.com/ 'Documentation GitHub')
