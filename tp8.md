clara salivet - 3ICS
4 octobre 22

# TP 8 - Ansible

## Exercice 1 : Mise en place

### Qustion 1 : Préparation des machines

#### 1. Dans les paramètres de VirtualBox (menu Fichier > Paramètres > Réseau), commencez par créer le réseau NAT correspondant ;

paramétre réseau : adaptateur 2 choisir NAT

#### 2. ajoutez une deuxième interface réseau à la machine, en mode Réseau NAT ;


#### 3. démarrez la machine, puis modifiez le fichier de configuration de Netplan pour attribuer l’IP statique indiquée ci-dessus.
```
sudo nano /etc/netplan/*.yaml
enp0s8: 
    address :
            - 192.0.0.0/24

sudo netplan apply

```

### Question 2
```
sudo nano /etc/hosts
on ajoute : 
    - 192.168.122.11 http1
    - 192.168.122.12 bdd1
```

###  question 3

```
sudo nano :etc/netpla/*.yaml
on modifie l'IP

sudo netplan apply

a réaliser sur http& et bdd&
```
```
hostname.ctl/ hostnam *nom*
reboot

sur les 3 machines
```
```
ping pour vérifier
ping google.fr pour verifier internet
```

## Exercice 2 : 

### Question 5 : 
``` 
methode 1 : création utilisateur
sudo useradd user-ansble #créer l'utilisateur, mais ne demande pas de mdp
sudo passwd user-ansible # permet de créer un mot de passe à l'utilisateur

avec useradd, l'utilisateur utilise sh (un shell) au lieu de bash
pour modifier le shell utilisé pat l'utilisateur on fait 
sudo usermod user-ansible -s /bin/bash

methode 2 : la meilleur
sudo adduser user-ansble #créer l'utilisateur, mais  demande de renseigner un mdp


sudo adduser user-ansible # l'ajoute dans le groupe sudo
```
### Question 6

```
ssh tp@http1 #permet de se connecter en ssh sur la VM tp@http1, depuis le node-manager
ssh tp@bdd1
#choisir yes pour laisser des traces de la connection
```

### Question 7
```
sudo nano inventaire.ini

on rédige : 

#[apache]
#http1

#[bd]
#bdd1
```

## Exercice 3 : première commande Ansible

### question 8 : 
```
chown user-ansible:user-ansible ansible # permet de changer le propriétaire du dossier ansible de root à user-anbsible
-R permet de l'appliquer à tous les sous dossiers et fichier
```

## Exercice 4 : création des comptes utilisateurs user-ansible

### Question 9 : commencez par générer la version chiffé du mot de passe du compte

```
ansible localhost -i inventaire.ini -m debug -a "masg={{'tp' | password_hash('sh512', 'secretsalt')}}"
```

### Question 10
