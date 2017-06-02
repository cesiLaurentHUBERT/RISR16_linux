# Commandes IPTABLES

## Introduction

`iptables` permet de gérer des règles réseau (filtrage, redirection).

Il est utilisé pour configurer un firewall, un NAT, etc.


## Création
La création se fait de la manière suivante:

`sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`

Ici, on ajoute une nouvelle règle :
* dans la table `nat` : '`-t nat`
* à la chaîne `POSTROUTING` : `-A POSTROUTING`
* avec la spécification suivante: ` -o eth0 -j MASQUERADE`


## Listage

Pour afficher les règles, plusieurs possibilités:

`sudo iptables -L`

va afficher les règles de la table `filter` (table par défaut)

`sudo iptables -t nat -L`

va afficher les règles de la table `nat`

`sudo iptables -t nat -L --line-number`

va afficher les règles de la table `nat` en affichant pour chaque règle son numéro dans la chaîne.

`sudo iptables -t nat -L POSTROUTING`

va afficher les règles de la table `nat` pour la chaîne `POSTROUTING`.

Il est possible de rajouter les options `--line-number`
ou `-v` pour toutes les opérations qui précèdent.

## Suppression

`sudo iptables -t nat -D POSTROUTING 1`

va supprimer la règle numéro 2 (numéro donné par `--line-number`) de la chaîne `POSTROUTING` dans la table `nat`.
