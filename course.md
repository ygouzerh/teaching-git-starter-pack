# GIT Lessons

## Faire ses premiers pas

### Modifier ses paramètres

1. Modifier le fichier ~/.gitconfig

*Teacher : explain why*

### Apprendre à créer un répertoire git en local

1. Création d'un dossier lambda

`mkdir nom_dossier`

2. Initialisation d'un repository git

`cd nom_dossier`

` git init `

### Création de notre example

1. Création d'un fichier python

Créer dans le repertoire un fichier : hello.py

```
#! /usr/bin/env python3

print("Hello World !")
``` 

2. Rendre le fichier executable

`chmod +x hello.py`

3. Test du fichier

`./hello.py`, vous devriez avoir la sortie suivante : `Hello World ! `

### Apprendre à sauvegarder ses modifications

#### Créer son premier commit
1. Voir les modifications apportées

`git status`

2. Ajout du fichier à l'index

`git add hello.py` 

3. Voir les modifications apportées

`git status`

4. Créer le commit 

`git commit -m "Mon tout premier commit !"`

5. Voir les modifications de l'index

`git status`

6. Voir l'historique

`git log` (puis `git log --oneline`)

et 

`gitk`
 
#### Faire sa première erreur

1. Rajouter une erreur dans le fichier précédent

```
#! /usr/bin/env python3

print("Hello World
```

2. Executer le fichier

`./hello.py`

Sortie attendue : 

```
  File "./hello.py", line 3
    print("Hello World !
                       ^
SyntaxError: EOL while scanning string literal
```

#### Rattraper sa dernière erreur

1. Voir les modifications apportées

`git status`

2. Supprimer les modifications

`git checkout -- hello.py`


3. Voir les modifications apportées

`git status`

4. Executer le fichier

`./hello.py` Sortie attendue : `Hello World !`

5. Voir le fichier

`cat hello.py`

### Se familiariser avec l'historique git

#### Créer le deuxieme commit
1. Modifier le fichier

Remplacer `print("Hello World")` par

`print("Hello, my name is PUT\_YOUR\_NAME\_HERE")`

2. Voir les modifications apportées 

`git status`

3. Ajout du fichier

`git add hello.py`

4. Créer le commit

`git commit -m "Je me présente maintenant"`

5. Voir l'historique

`gitk`

#### Créer le premier commit
1. Re-modifiez le fichier

Remplacer `print("Hello, my name is PUT\_YOUR\_NAME\_HERE")` par 
```
name = "PUT\_YOUR\_NAME\_HERE"
print("Hello, my name is", name,"and you ?")
```

2. Ajout du fichier

`git add hello.py`

3. Créer le commit

`git commit -m "Je demande quel est ton nom"`

4. Voir l'historique

`gitk`

#### Voir la différence entre les commits

1. Récupérez le hash du tout premier commit

`git log --oneline`

2. Voir la différence

`git diff HASH\_PREMIER\_COMMIT`

#### Revenir à l'avant-dernier commit

1. Voir ce que contient l'avant dernier commit

`git show HEAD^1`

2. Reset (soft)

`git reset HEAD^1`

3. Voir les modifications apportées

`git status`

4. Modifier le fichier python qui devrait être sous la forme:

```
name = "PUT\_YOUR\_NAME\_HERE"
print("Hello, my name is", name,"and you ?")
```
par 

```
name = "PUT\_YOUR\_NAME\_HERE"
print("Hello, my name is", name,". I need to go now, bye !")
```

5. Ajouter la modification à l'index

`git add hello.py`

6. Commiter

`git commit -m "Je dois partir"`

7. Voir les modifications

`gitk`

## Travail à plusieurs

### Mettre son code en ligne

1. Créer un compte GitHub

2. Créer un répertoire GitHub

3. Récupérez l'URL

4. Rajoutez le remote 

`git remote add origin PUT\_URL\_HERE`

5. Voir si tout s'est bien déroulé

`git remote -v`

6. Envoyer son code sur le remote

`git push origin master`

### Récupérez le projet de quelqu'un d'autre

1. Aller dans un autre dossier qui n'est pas un répertoire git

Par exemple : `cd ..`

2. Cloner le repository

`git clone URL local_path_new_folder`

3. Executer le fichier

`./hello.py`

### Ajouter des modifications

1. Player one : modifier le code

```
#! /usr/bin/env python3

name = "..."
print("Hello, my name is", name,". I need to go now, bye !")
print("Oups no, this is not my name")
```

2. Voir les modifications apportées

`git status`

2. Ajouter le fichier

`git add hello.py`

3. Commiter le fichier

`git commit -m "Not my name"`

4. Envoyer les modifications à tout le monde

`git push origin master`

### Récupérer des modifications

1. Player two : récupérer le code

`git pull origin master`

2. Executer le fichier

`./hello.py`

### Coder à plusieurs : mise en pratique d'un conflit

1. Player two : Modification du fichier

Rajouter la ligne : `print("I am the player two")`

2. Player one : Modification du fichier

Rajouter la ligne : `print("I am the player one")`

3. Player one : Envoie ses modifications

`git status`
`git add hello.py`
`git commit -m "Je suis le player one"`
`git push origin master`

4. Player two : Envoie ses modifications

`git status`
`git add hello.py`
`git commit -m "Je suis le player two"`
`git push origin master`

###  Player two : résoudre un conflit

5. Récupération des modifications

`git pull`

6. Voir ce qu'il se passe

`git status`

7. Voir le détail des erreurs

`git diff`

8. Correction des erreurs

Supprimer tout ce qui est entre `<<<< HEAD et >>>>`, sauf `print("I am the player two")`

9. Voir les modifications apportées

`git status`

10. Ajouter les modifications

`git add hello.py`
`git commit` : Sauvegarder le fichier qui va s'ouvrir (Vim : tapez `:wq`)

11. Voir la modification de l'historique

`gitk`

11. Envoyer les modifications

`git push`

### Player one : observer la résolution d'un conflit

1. Récupérer les dernières modifications

`git pull`

2. Voir ce qu'il s'est passé

`gitk`

3. Executer le fichier 

`hello.py`

*Teacher : explain how systems like GitHub's Pull Requests could prevent this.*

## Organiser son développement : les branches

### Player one (ou le créateur du répo) : Sécurisation de la branche master

*Teacher : show him*

### Player two : création d'un fichier (Peut se faire en // de partie suivante)

1. Toujours vérifier les dernières modifications

`git pull origin master`

2. Voir les différentes branches disponibles

`git branch`

3. Créer une nouvelle branche et s'y déplacer 

`git checkout -b branche_of_two`

4. Voir les différentes branches

`git branch`

4. Créer le fichier `main.py`

```
#! /usr/bin/env python3

import one

if __name__ == "__main__":
	one.hello_world()	
```

5. Ajouter le fichier main.py

`git add main.py`

6. Rebasculer sur master

`git checkout master`

7. Voir que le fichier nous a suivit

`git status`

8. Rebasculer sur la branche

`git checkout branche_of_two`

9. Committer le fichier

`git commit -m "Add the main file"`

10. Voir les modifications

`git log --oneline`

11. Envoyer les modifications

`git push`

12. Retourner sur master

`git checkout master`

13. Récupérer la dernière version

`git pull origin master`

14. Voir les fichiers présents sur master

`ls`

### Player one : Mêmes étapes

Changements :
* "main.py" => "one.py"

```
#! /usr/bin/env python3

def hello_world():
    print("Hello world ! We are player two and one !")
```

* branche\_of\_two => branche\_of\_one

* Message du commit =>  "Add the hello\_world feature"

### Faire le merge des deux

1. *Teacher : show how to create pull requests (with the rebase button obviously)*

2. Récupérer les dernières modifications

`git checkout master`
`git pull origin master`

4. Voir l'historique

`gitk`

5. Executer le fichier

`./hello.py`
