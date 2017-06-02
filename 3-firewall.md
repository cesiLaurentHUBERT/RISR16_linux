# Protection des machines

## Introduction

Afin de protéger les machines sur le réseau, il est indispensable d'y ajouter un firewall. Celui-ci peut-être de différent types et configurer avec différents logiciels.

Nous allons voir comment installer un firewall simple (à gérer en ligne de commande) et un outil graphique de gestion de firewall.

## Firewall simple


### Installation
Vous pouvez installer sur vos serveurs (sauf pour l'instant sur le serveur de fichiers `Samba`) les fichiers [firewall](data/firewall) [firewall.conf](data/firewall.conf).

* `firewall` à placer dans `/etc/init.d`
* `firewall.conf` à placer dans `/etc/firewall`

Lancer la commande suivante:
```bash
sudo chmod +x /etc/init.d/firewall
```

C'est le fichier `firewall.conf` qui sert à  configurer le firewall.


### Configuration

La configuration se fait dans le fichier `/etc/firewall/firewall.conf`. Ouvrez ce fichier et essayez de comprendre par vous même comment il fonctionne.

Demandez à l'intervenant si vous êtes bloqués.

### Activation

Nous allons activer ce service avec les commandes décrites ici. Le nouveau système de gestion des services (`systemd`) ne prend pas en compte certaines commandes du firewall car il a été écrit pour `Wheezy`.


#### Avec systemd

On va utiliser les commandes suivantes pour activer ce service:

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl start firewall
```

Attention: pour arrêter le firewall, la commande `stop` va bloquer tous les accès réseau (elle va `droper` toutes les requêtes réseau via `iptables`).

Pour éviter cela, utiliser plutôt la commande suivante:

```bash
$ sudo service firewall clear
```

#### Anciennes versions de Debian
Les commandes pour activer sont différentes sous `Wheezy` et antérieures:

```bash
sudo update-rc.d firewall defaults
sudo update-rc.d firewall enable
sudo service firewall start
sudo service firewall clear
sudo service firewall stop #bloque le réseau
```


## Outil graphique

L'outil graphique choisi ici est `gufw`. Il se lance sous client `X`.

### Installation

Le paquet `gufw` est à installer sur le serveur Samba/FTP.

### Utilisation

En lançant l'outil avec votre compte, vous pouvez appuyer sur le bouton `Unlock`.

Que se passe-t-il ?

Est-ce normal ?

Tentez de lancer l'application en tant que `root`

Regardez dans les annexes si un document pourrait vous aider à résoudre ce problème.


### Configuration

Des blocages devrait apparaître avec `Samba` et `vsFTP`. Faites-en sorte d'ouvrir les ports correspondants après avoir fait une recherche sur Internet sur le sujet.

Pour vsFTP, voici une piste:  https://www.debian-fr.org/t/vsftpd-ssl-iptables/11971
