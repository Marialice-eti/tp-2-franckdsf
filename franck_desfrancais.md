#### 1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
avec `echo $PATH` on retrouve tous les chemins des commandes. elles sont localisées dans le dossier /usr/local/.
#### 2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?
c'est la variable `$HOME`.
#### 3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
la variable d’environnement _LANG_ détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur la variable d'environnement _PWD_ contient le répertoire de travail courant de l'interpréteur de commande. la variable d'environnement _OLDPWD_ contient le chemin absolu vers le répertoire courant précédent la variable d'environnement _SHELL_ indique l'interpréteur shell utilisé par défaut, ici c'est `/bin/bash`
#### 4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.
pour créer la variable : `export MY_VAR="test"`.
pour vérifier qu'elle existe : `printenv MY_VAR` .
résultat : `test`.
#### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.

#### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.

#### 7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.

#### 8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.

#### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?

#### 10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)
