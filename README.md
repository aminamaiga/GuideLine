### Informations

| Nom du projet | GuideLine |
|-----------|-----------|
| Type de document | Documentation technique | 
| Date           |   07/03/2022        |          
|  Version         |   1.0        |    
|  Mots-clès         |   Architecture – Fonctionnement – Technologies – Diagrammes – Bugs - Interactions |
|Auteurs| Aminata Maiga- amaiga|

### Rédaction et modifications

| Vesrion | Date | Nom | Description |
|-----------|-----------|-----------|-----------|
| 1.0 | 01/01/1991 | Maiga | Première version |      
| 1.1 | 01/01/1991 | Diop | * Détails sur la base serveur * Mise à jour API mobile * Détails sur la partie * Audio Qt Mobility - Multimedia |      
| 1.2 | 01/01/1991 | Fall | *Mise à jour des diagrammes |      

### Table des matières

1. Résumé du document
2. Rappel sur le fonctionnement de l'application
    1. Description du logiciel
    2. Décomposition du projet
    3. Architecture globale
3. Client
    1. Architecture
    2. Technologies utilisées
    3. Diagramme de classes
    4. Modèle de données
    5. Particularités de l'application allégée
4. Serveur
    1. Architecture
    2. Technologies utilisées
    3. Modèle de données
    4. Interactions extérieures
    5. API Client
    6. API Publique 
5. Application Mobile
    1. Architecture
    2. Technologies utilisées
    3. Interactions
    4. API
6. Bugs connus
6.1 Site web
Annexes

________________________________________________________________________________________________________________________________________________________________________________

### 1. Résumé du document

Ce document est la documentation technique officielle de la suite applicative defuze.me. Il est divisé en
quatre parties :<br>
 – La documentation technique du client : l'application bureau ;<br>
 – La documentation technique du serveur: site internet et APIs ;<br>
 – La documentation technique de l'application mobile fonctionnant sur Android et iOS ;<br>
 – Les bugs connus au sein de la suite logicielle<br>.
 
 ________________________________________________________________________________________________________________________________________________________________________________

2. ### Rappel sur le fonctionnement de l'application
    1. ## Description du logiciel
Notre EIP a pour but la création d'un logiciel de diffusion de radio destiné aux professionnels : defuze.me.
Plus que la diffusion de musique, il permet aux stations de radio de gérer un maximum d'éléments de
leur quotidien, notamment les contrats publicitaires, les jingles, la récupération et l'exportation de flux de
données.<br>

Le logiciel a une interface moderne et ergonomique, permettant de gérer efficacement et simplement la
diffusion tout en proposant de nombreuses manipulations avancées. Il est utilisable aussi bien sur des
surfaces classiques que tactiles, et ce quel que soit le nombre d'écrans à disposition.
Enfin, un fort accent est mis sur l'interaction avec un service web conçu par nos soins, permettant aux
radios d'interagir facilement avec leurs auditeurs, au travers d'Internet.

    2. ## Décomposition du projet
    
Notre projet se décompose en différentes parties : <br>
* Le logiciel client, qui est une application bureau fonctionnant sur Windows, Linux et MacOS,
permettant la gestion du son, des pistes audio, de la bibliothèque musicale et du planning ;<br>

* Une application fonctionnant sur les tablettes tactiles équipées d'iOS ou d'Android, dialoguant
avec le logiciel client et implémentant les fonctions de base, telles que la gestion de la
bibliothèque et l'organisation du planning ;<br>

* Un service web et un site web, qui sont hébergés sur un serveur applicatif distant et qui
communiquent en permanence avec le logiciel client, pour assurer de multiples fonctions comme
le contrôle de la licence du logiciel et la gestion du planning à distance.<br>
<br>
Dans la suite de ce document, chacune de ces différentes parties sera développée.

  3. ## Architecture globale
    ![archit](https://github.com/aminamaiga/GuideLine/blob/main/image.png)
                        ### Architecture globale
3. ### Client
    1. Architecture
       
5.                        
   
