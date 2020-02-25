# Exercice 1
## Question 1
### Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
En faisant echo PATH on obtient: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:
/usr/local/cpe/bin:/softwares/bin:/softs/bin


## Question 2
### Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?  
C'est la variable $HOME

## Question 3
### Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
LANG contient  la langue du système, PWD (Print Working Directory) contient le chemin absolu actuel dans bash, OLDPWD contient le
chemin précédent avant d'éxécuter la commande cd, SHELL contient le chemin du bash, _ donne le chemin de la commande printenv.

## Question 4
### Créez une variable locale MY_VAR. Vérifiez que la variable existe.
export MY_VAR="lolo"
printenv MY_VAR

## Question 5
### Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin
### de cette question, tapez la commande exit pour revenir dans votre session initiale.
En tapant bash nous avons ouvert une nouvelle instance où la variable MY_VAR n'existe pas puisqu'elle était temporaire à l'instance précédente.

## Question 7
### Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.
### Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.
export NOMS="grignon grignon"
printenv NOMS

## Question 8
### Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” en utilisant la variable NOMS.
echo Bonjour à vous deux, $NOMS

## Question 9
### Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande
### unset ?
Quand on utilise printenv sur la variable cela la supprimme, sinon elle est vide

## Question 10
### Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin
echo '$HOME = '$HOME


# Exercice 2
#!/bin/bash

VAR1="Linuxize"
VAR2="Linuxize"

if [ "$VAR1" = "$VAR2" ]; then
    echo "Strings are equal."
else
    echo "Strings are not equal."
fi

