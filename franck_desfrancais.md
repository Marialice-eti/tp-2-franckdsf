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

`echo $HOME = $HOME`
output = `$HOME = /home/server`
