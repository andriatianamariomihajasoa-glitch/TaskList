# 🐳 Guide Complet Docker : De la Théorie à la Pratique

Ce document est un condensé des commandes essentielles pour maîtriser le cycle de vie des conteneurs, la persistance des données et la gestion des images.

---

##  1. Construction de l'Image (Build)
L'image est un "instantané" (snapshot) immuable de votre application. Elle contient le code, les bibliothèques et la configuration.

* **Build standard :**
    ```bash
    sudo docker build -t nom_image:tag .
    ```
    > **Note :** Le `.`à la fin est crucial. Il définit le **contexte de build** (le dossier où Docker va chercher les fichiers à inclure).
* **Build avec un fichier spécifique :**
    ```bash
    sudo docker build -t nom_image:tag -f chemin/vers/fichier/Dockerfile .
    ```


### Pour voir les images :
```bash
    sudo docker images 

```
### Pour les supprimés :
```bash
    sudo docker rmi  id_ou_nom_img

```
---


##  2. Lancement et Persistance (Run)

Le "Run" crée une instance modifiable de votre image appelée **Conteneur**.

### A. Mode Éphémère (Sans volume)
Tout fichier créé à l'intérieur du conteneur est supprimé en même temps que lui.
```bash
sudo docker run -d -p 8080:80 --name nom_conteneur nom_image:tag
```
### B. Avec volume :
les données sont conserveés si vous essayez de lancer à nouveau ou créer le conteneur avec le même nom de la volume vous recupererz vos données si jamais il y en a la suppression .

```bash
sudo docker run -d -p 8080:80 --name nom_conteneur:tag(facultatif) -v nom_volume:/chemin/dans/l/image  nom_image
``` 

### C. Avec bind Mount : 
le Bind Mount c'est de lancer un conteneur a partir de l'image avec developpement en temps réels , en liant un dossier local ou votre répertoire avec le workdir de l'image . 
```bash
sudo docker run -d -p 8080:80 --name nom_conteneur:tag(facultatif) -v $(pwd):/chemin/dans/l/image  nom_image
``` 
ou 
```bash
sudo docker run -d -p 8080:80 --name nom_conteneur:tag(facultatif) -v chemin/de/vos/projet:/chemin/dans/l/image  nom_image
``` 
## 3.  Gestion des conteneurs : 


### Pour relancer ou lancer
```bash
sudo docker start id_ou_nom_conteneur
```
### Pour vérifier si le conteneur est en cours .
```bash
sudo docker ps
```

### Pour voir tout les conteneurs qui existent
```bash
sudo docker ps -a
```

### Pour arrêter un conteneur de tourner
```bash
sudo docker stop id_ou_nom_conteneur
``` 


### Pour supprimer
```bash

sudo docker rm id_ou_nom_conteneur

```

## 4 Gestion de volumes : 
## Lister tout les volumes :

```bash

sudo docker volumes ls

```
## Supprimer une volume :
```bash

sudo docker volume rm nom_volume

```
