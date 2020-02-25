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

# Exercice 3 
#!/bin/bash

function is_number()
{
	re='^[+-]?[0-9]+([.][0-9]+)?$'
	if ! [[ $1 =~ $re ]] ; then
		return 1
	else
		return 0
	fi
}

read -p "Saisissez un nombre : " nb
is_number $nb
if [ $? -eq 0 ]; then
	echo "C'est un nombre reel"
else
	echo "Ce n'est pas un nombre reel"
fi

# Exercice 4
#!/bin/bash

if [ -z $1 ];then
	echo "Utilisation : $0 nom_utilisateur"
else
	for user in $(cut -d: -f1 /etc/passwd)
	do
		if [ $user = $1 ];then
			echo "l' utilisateur existe"
			exit
		fi
	done
	echo "l'utilisateur n'existe pas"
fi

# Exercice 5 (marche pas)
#!/bin/bash

function facto()
{
  f=$f*$1
  $1=$1-1
  if ! [ $1 = 1 ]; then
    facto $1
  fi
}

export f=1
facto $1
echo "$f"

# Exercice 6
#!/bin/bash

nb=$(((RANDOM%1000)+1))

fin=-1

while [ $fin -ne $nb ]
do
read fin
if [ $fin -gt $nb ]; then
  echo "C'est moins !"
fi
if [ $fin -lt $nb ]; then
  echo "C'est plus !"
fi
done

echo "Gagné !"

# Exercice 7
## 1)
#!/bin/bash

function is_number()
{
	re='^[+-]?[0-9]+([.][0-9]+)?$'
	if ! [[ $1 =~ $re ]] ; then
		return 1
	else
		return 0
	fi
}

somme=0
nb=0
min=$1
max=$1

while (("$#")); do
    is_number $1
    if [[ $? = 1 ]]; then
        echo "Un des paramètres n'est pas un nombre"
        exit
    fi

    somme=$((somme + $1))
    nb=$((nb + 1))

    if [[ $1 -gt $max ]]; then
        max=$1
    elif [[ $1 -lt $min ]]; then
        min=$1
    fi
    shift
done

echo Min: $min
echo Max: $max
printf 'Moyenne: %.2f\n' $(echo "$somme / $nb" | bc -l)

## 2)
#!/bin/bash

function is_number()
{
	re='^[+-]?[0-9]+([.][0-9]+)?$'
	if ! [[ $1 =~ $re ]] ; then
		return 1
	else
		return 0
	fi
}

values=()
input="0"
index=0

while [ -n "$input" ]; do
    read -p "Entrez un nombre: " input

    if [ -n "$input" ]; then
        is_number $input
        if [[ $? = 1 ]]; then
            echo "Ce n'est pas un nombre"
        else
            values[$index]=$input
            index=$(( $index + 1 ))
        fi
    fi
done

sum=0
min=${values[0]}
max=${values[0]}

for n in ${values[@]}; do
    sum=$((sum + $n))
    count=$((count + 1))

    if [[ $n -gt $max ]]; then
        max=$n
    elif [[ $n -lt $min ]]; then
        min=$n
    fi
done

echo Min: $min
echo Max: $max
printf 'Moyenne: %.2f\n' $(echo "$sum / $index" | bc -l)
