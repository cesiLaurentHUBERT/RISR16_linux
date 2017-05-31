# Passage de proxy sur une machine sans client graphique

## Introduction
Sur certains réseaux, il est nécessaire de passer un serveur proxy pour se connecter à Internet.

Dans ce cas, il faut ouvrir un navigateur et saisir son login et son mot de passe. Cependant, sur une machine installée comme serveur, c'est-à-dire sans interface graphique, cela demande une configuration supplémentaire.

## Pré-requis

Il faut avoir installé un client `X` (`VcXsrv`, `Xming`, `XQuartz` ou un autre) sur votre machine physique.

Il faut lancer `ssh` avec l'option X11-forwarding (`-X` ou `-Y`).

## Installation d'un navigateur

### Midori

Télécharger le paquet depuis l'adresse suivante: http://midori-browser.org/download/debian/

```bash

wget -O midori_0.5.11-0_amd64_.deb http://midori-browser.org/downloads/midori_0.5.11-0_amd64_.deb#!sha1!57ebbbd567be07e9e6d31dbf39052cbee0d91fa8
```

En général, le paquet 64 bits (amd64) est celui adapté à votre système.

Installer le paquet avec la commande `dpkg` :

```bash
sudo dpkg -i midori_0.5.11-0_amd64_.deb
```

Le navigateur étant installé, pour le lancer:

```bash
midori
```

### Xombrero

L'installation se fait par le gestionnaire de paquet:


```bash

sudo apt-get install xombrero
```


#### Configuration

```bash
gunzip -c  /usr/share/doc/xombrero/examples/xombrero.conf.gz > ~/.xombrero.conf
```
Et modifier:

```
# Normal browser operation (default).
browser_mode            = normal

#...

# Classic GUI (default).
gui_mode                = classic


```

Pour éviter d'avoir un texte blanc sur fond blanc, il faut faire les opérations suivantes.


Modifier:
```bash
sudo ne /usr/share/xombrero/xombrero.css
```

Et trouver la classe `entry`:
```css
.entry {
        padding: 2px;
        color: black;
}
```

Puis chercher `select`

```css
.entry:selected,
.entry:selected#red,
.entry:selected#yellow,
.entry:selected#green,
.entry:selected#blue,
.entry.progressbar,
.entry.progressbar#red,
.entry.progressbar#yellow,
.entry.progressbar#green,
.entry.progressbar#blue,
#statusbar .entry:selected,
#statusbar .entry:selected#red,
#statusbar .entry:selected#yellow,
#statusbar .entry:selected#green,
#statusbar .entry:selected#blue,
#statusbar .entry.progressbar,
#statusbar .entry.progressbar#red,
#statusbar .entry.progressbar#yellow,
#statusbar .entry.progressbar#green,
#statusbar .entry.progressbar#blue {
        background-image: none;
        background-color: blue; /* MODIFIER CETTE LIGNE*/
        color: @selected_fg_color;
}
```

##### Référence

https://unix.stackexchange.com/questions/227667/fvwm-gtk-and-xombrero-input-fields-are-white-text-on-white-background
