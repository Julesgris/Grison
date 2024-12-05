Voici la correction de votre texte, avec des améliorations de grammaire, de syntaxe, et de structure pour le rendre plus fluide et clair :

---

# Documentation SQL

### Cette documentation vous permettra de :

* Installer un serveur avec le SGBD MariaDB de manière autonome.
* Créer une base de données.
* Importer une structure et des données à partir d'un script SQL déjà réalisé.

### 1 - Installation du Serveur

Avant d’installer le SGBD, il est nécessaire d’installer un serveur avec un système d’exploitation. Le serveur sera une machine virtuelle sur VirtualBox.

### Installation de l'image ISO

Lorsque vous souhaitez installer un nouveau système d’exploitation sur une VM VirtualBox, il est nécessaire dans la plupart des cas d’utiliser un fichier d’image disque au format ISO.

L'image que nous souhaitons installer se trouve sur ce site : [https://www.debian.org/CD/netinst/](https://www.debian.org/CD/netinst/).

- Téléchargez l'image ISO pour l'installation par le réseau `amd64`.

Une fois l'image ISO téléchargée, vous pouvez la monter sur VirtualBox.

### Création de la machine virtuelle

Une fois sur VirtualBox, cliquez sur "Nouvelle", puis donnez un nom à la machine virtuelle. Ensuite, dans "Image ISO", recherchez l'image ISO téléchargée précédemment.

**Cochez la case "Skip Unattended Installation".**

Ensuite, après avoir cliqué sur "Suivant", assurez-vous que les paramètres correspondent à ceux des images (les images sont dans l'ordre du processus).

L'installation de la machine virtuelle est maintenant terminée.

### Configuration de la machine virtuelle

Maintenant, nous allons configurer Debian.

Démarrez la machine virtuelle en cliquant sur "Démarrer".

Vous arriverez alors sur le menu de démarrage Debian. Choisissez "Advanced options". Nous allons configurer la machine.

Ensuite, sélectionnez "Expert Install".

Lancez l'installation de base en choisissant les options que vous préférez.

## Arrivée sur le menu principal du programme d'installation de Debian

Le matériel réseau sera détecté. Configurez ensuite le réseau.

Appuyez sur "Oui" pour activer le serveur DHCP.

Ensuite, choisissez un nom pour la machine et un nom de domaine.

Vous allez ensuite créer des utilisateurs et choisir des mots de passe. Cliquez sur "Non" pour l'utilisateur root.

Créez un utilisateur opérateur et choisissez un mot de passe (par exemple, P@ssw0rd).

Ensuite, vous pouvez directement sélectionner "Installer le programme de démarrage GRUB". Il vous sera demandé de choisir la méthode de partitionnement, choisissez "Assisté - utiliser un disque entier".

Cliquez sur "Oui".

Ensuite, vous allez installer le noyau `linux-image-amd64`.

Sélectionnez l'image générique.

Cliquez sur "Non", puis "Oui" pour installer le système d'exploitation sur la machine virtuelle. Sélectionnez ensuite la case en rouge.

Une fois tout cela terminé, vous pouvez finir l'installation.

### Configuration réseau

Exécutez la commande suivante pour reconfigurer le réseau :

```bash
sudo ifdown enp0s8 && sudo ifup enp0s8
```

Ensuite, éditez le fichier de configuration du réseau :

```bash
sudo nano /etc/network/interfaces
```

Modifiez le fichier comme indiqué sur l'image ci-dessous (en fonction de votre configuration).

Vous êtes maintenant sur une autre adresse IP et vous pouvez accéder à Internet. Par exemple, faites un ping vers 8.8.8.8 pour vérifier :

```bash
ping 8.8.8.8
```

### Installation de SSH

Pour installer SSH, exécutez les commandes suivantes :

```bash
sudo apt update
sudo apt install openssh-server -y
```

Si le SSH rencontre un problème, éditez le fichier des sources de APT :

```bash
sudo nano /etc/apt/sources.list
```

Ajoutez cette ligne dans le fichier :

```
deb http://deb.debian.org/debian bookworm main non-free-firmware
```

Mettez ensuite à jour les sources et réexécutez la commande d'installation de `openssh-server` :

```bash
sudo apt update
sudo apt install openssh-server -y
```

Ensuite, sur votre machine Windows, ouvrez l'invite de commandes et connectez-vous à votre SSH. Cela vous permettra d'accéder à votre Debian depuis votre machine Windows.

### Installation de MariaDB

Pour installer MariaDB, utilisez la commande suivante :

```bash
sudo apt install mariadb-server -y
```

Ensuite, apportez les modifications nécessaires à la configuration de MariaDB en éditant le fichier suivant :

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```