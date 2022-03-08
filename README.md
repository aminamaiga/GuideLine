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
________________________________________________________________________________________________________________________________________________________________________________

  3. ## Architecture globale
   
   ![architecture globale](https://github.com/aminamaiga/GuideLine/blob/main/image.png)
         
### 3.1  Client
    1. Architecture
        ![architecture client](https://github.com/aminamaiga/GuideLine/blob/main/imageclient.png)

Le cœur du logiciel, divisé en plusieurs modules, ne propose pas directement de fonctionnalités à
l'utilisateur, mais fournit des services aux plugins.<br>
Certains de ces plugins sont statiques. Ils fournissent à l'utilisateur les fonctionnalités essentielles du
logiciel (la file de lecture ou les lecteurs audio par exemple). Ils sont indissociables du cœur du logiciel.<br>
Au contraire, les plugins dynamiques fournissent des fonctionnalités supplémentaires qui n'intéresseront
peut-être pas tous les utilisateurs.<br>
Ils peuvent être (dé)chargés à la volée suivant les besoins, à l'aide du
gestionnaire de plugins.
Enfin, les plugins linguistiques sont des fichiers binaires contenant les traductions des éléments textuels.<br<
   
## 3.2 - Technologies utilisées
Le logiciel client est codé en C++ et utilise le framework Qt de Nokia.<br>
Qt fournit tous les éléments nécessaires à la réalisation de notre application, et apporte plusieurs<br>
éléments essentiels :<br>

   * La portabilité : un code Qt compile indifféremment sous les trois systèmes d'exploitation ciblés, à
savoir Windows, Linux et Mac OS X.

    * Soutenu par Nokia, Qt est utilisé dans des projets professionnels de grande envergure (tels KDE
        ou Meego). Il est en développement perpétuel et possède une communauté active. Cela nous
        assure la viabilité à long terme de ce framework.

    * Nokia et Qt fournissent depuis peu de nouveaux modules Qt ciblés sur une utilisation mobile et
            tactile. La version allégée du logiciel client utilise donc des technologies très récentes.
            Parmi les nombreux éléments du framework Qt, certains sont particulièrement importants dans
            l'architecture mise en place :

   * Qt Plugins <br>
        Nous utilisons l'API bas niveau de Qt permettant d'ajouter des fonctionnalités aux applications.
        Ces plugins sont soit statiques, soit dynamiques (sous forme de bibliothèques dynamiques SO ou
        DLL). Les plugins interagissent avec l'application via une interface C++.
        Les Qt Plugins permettent ainsi à l'architecture d'être modulaire.
  
   * Qt Linguist
Qt Linguist est un outil incorporé au framework Qt qui permet de créer facilement une application
multilingue. Il permet en effet de séparer le texte affiché du code (via l'utilisation de clés). La
traduction peut alors être effectuée séparément grâce à l'outil graphique fourni, puis rendu
disponible via des fichiers binaires .qm. Ces binaires peuvent être chargés à la volée par
l'application Qt.
De plus, Qt peut détecter la langue du système de l'utilisateur et charger automatiquement le
binaire .qm le plus adapté.
   * Qt Mobility - Multimedia
Qt Mobility – Multimedia est un add-on à Qt fournissant une interface de programmation
permettant la lecture et l'enregistrement audio, la gestion de contenu multimédia (listes de
lectures) et donnant un accès bas niveau aux flux audio, permettant ainsi leur modification pour
appliquer des effets et des filtres. Les technologies hors-Qt utilisées sont relatives à la base de données.
     * SQLite (via QtSQL)
        SQLite a été choisi comme SGDB du logiciel client pour sa simplicité. En effet, cette application
        ne sollicite qu'assez peu la base, et ne requiert pas d'opération complexe.
        L'utilisation d'un SGDB plus complexe (utilisant par exemple une architecture client/serveur)
        n'est pas nécessaire.
        L'application accède à la base de données via le module QtSQL du framework Qt, qui fournit une
        interface objet simple.
## 3.3 Diagramme de classes

        ![architecture globale](https://github.com/aminamaiga/GuideLine/blob/main/image.png)


     
