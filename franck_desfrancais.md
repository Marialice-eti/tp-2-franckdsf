#### 1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
Avec `echo $PATH` on retrouve tous les chemins des commandes. elles sont localisées dans le dossier /usr/local/.

#### 2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?
C'est la variable `$HOME`.

#### 3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
La variable d’environnement _LANG_ détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur la variable d'environnement _PWD_ contient le répertoire de travail courant de l'interpréteur de commande. la variable d'environnement _OLDPWD_ contient le chemin absolu vers le répertoire courant précédent la variable d'environnement _SHELL_ indique l'interpréteur shell utilisé par défaut, ici c'est `/bin/bash`

#### 4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.
Pour créer la variable : `MY_VAR="test"`.<br>
Pour vérifier qu'elle existe : `printenv MY_VAR` .<br>
Output : `test`.

#### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.
Elle ouvre un nouveau niveau sur le shell. La variable MY_VAR n'existe pas dans ce shell car c'est une variable locale à l'autre shell. 

#### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
Pour transformer cette variable en variable d'environnement il faut taper `export MY_VAR="test"`. On peut alors utiliser la commande `printenv MY_VAR` pour récuperer la valeur de la variable (_test_).

#### 7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.
`export NOMS="lucas franck"`
`echo $NOMS`
`output : lucas franck`

#### 8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.
`echo "Bonjour à vous deux, $NOMS"`

#### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?
Quand on donne une valeur vide à une variable, celle-ci reste utilisable. Si on utilise la commande `unset`, la variable est supprimée. Elle n'est plus définie.

#### 10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)

`echo '$HOME' = "$HOME"`
ou
`echo "\$HOME = $HOME"`
output = `$HOME = /home/server`

### Programmation Bash

Il suffit d'utiliser `mkdir script` pour créer un dossier.
Puis de l'ajouter au PATH avec `PATH=$PATH:~/script`.

 #### Exercice 2. Contrôle de mot de passe

pour créer le script il faut effectuer cette commande `nano testpwd.sh`
lui ajouter :<br>
```
#!/bin/bash

PASSWORD="Ak18"
PASS_CHECK=""

echo "entrez un mot de passe"
read -s PASS_CHECK

if[ $PASSWORD = $PASS_CHECK ]; then
   echo "connecté"
else
   echo "mauvais mot de passe"
fi
```

ctrl+S pour sauvegarder
ctrl+X pour quitter
puis lui donner les droits avec `chmod u+x hello.sh`
puis l'executer avec `testpwd.sh`

#### Exercice 3. Expressions rationnelles
```                                            
#!/bin/bash

function is_number(){
 re='^[+-]?[0-9]+([.][0-9]+)?$'
 if ! [[ $1 =~ $re ]] ; then
  return 1
 else
  return 0
 fi
}

is_number $1
if [ "$?" = "0" ]; then
        echo "c'est un float"
else
        echo "ce n'est pas un float"
fi
```
#### Exercice 4. Contrôle d’utilisateur

```
#!/bin/bash

INPUT_USER=$1
FILENAME="${0##*/}"
USERS=$(cut -d: -f1 /etc/passwd)

if [ -z "$INPUT_USER" ]; then
        echo "Utilisation: $FILENAME nom_utilisateur"
else
        EXIST=0
        for user in  $USERS
        do
                if [ "$user" = "$INPUT_USER" ]; then
                        echo "l'utilisateur existe"
                        EXIST=1
                fi
        done
        if [ $EXIST -eq 0 ]; then
                echo "l'utilisateur n'existe pas"
        fi
fi
```

#### Exercice 5. Factorielle

```
#!/bin/sh 
 
fact() { 
        n=$1 
        if [ $n -eq 0 ] 
        then 
                echo 1 
        else 
                echo $(( n * `fact $(( n - 1 ))` )) 
        fi 
} 
 
echo `fact $1`
```

#### Exercice 6. Le juste prix
```
#!/bin/sh 
NOMBRE=$(( ( RANDOM % 100 )  + 1 ))
USER_NB=-1


echo "devinez le nombre que j'ai choisi (entre 1 et 100)"
while [ $NOMBRE != $USER_NB ]
do
        echo $NOMBRE
        read USER_NB

        if [ $NOMBRE -lt $USER_NB ]; then
                echo "il est plus petit, recommencez"
        elif [ $NOMBRE -gt $USER_NB ]; then
                echo "il est plus grand, recommencez"
        fi
done

echo "bravo vous avez trouvé !"
```
#### Exercice 7. Statistiques
```
#!/bin/sh

function reelounon()
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $nb =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

keep=1
nb=0
i=0
marks=()

while [ $keep != 0 ]
do
        echo "entrez une note"
        read nb

        reelounon $nb
        if [ "$?" != "0" ]; then
                echo "merci d'entrer que des réels"
        else
                marks[$i]=$nb
        fi

        echo "continuer ? o / n"
        read answer
        if [ "$answer" = "n" ]; then
                keep=0;
        fi

        ((i++))
done

mini=${marks[0]}
maxi=${marks[0]}
moy=0
longueurtableau=${#marks[@]}
for mark in "${marks[@]}"
do
        if [[ $mark < $mini ]]; then
                mini=$mark
        fi
        if [[ $mark > $maxi ]]; then
                maxi=$mark
        fi
        ((moy=moy+mark))
done
moy=$((moy / longueurtableau))
echo "le max est $maxi, le min est $mini et la moyenne est de $moy"
```
