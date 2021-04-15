
<https://cunchem.github.io/cli-network-cmd/>

# Fiche de référence interface ligne de commande et réseau
Cette fiche contient un ensemble de commandes et d'outils utiles pour l'utilisation de l'interface par ligne de commande (CLI) et les manipulations réseau basiques.

Ce document est destiné à l'enseignement au département FIMI de l'INSA-Lyon et plus particulièrement au P2I-6.

- [L'interface ligne de commande (ILC)](#linterface-ligne-de-commande-ilc)
  - [Qu'est-ce qu'une commande ?](#quest-ce-quune-commande-)
  - [Arborescence et chemin](#arborescence-et-chemin)
  - [Commandes populaires](#commandes-populaires)
  - [Accéder à l'ILC (ouvrir un terminal)](#accder--lilc-ouvrir-un-terminal)
  - [Utilisation avancée du terminal (astuces pour gagner du temps)](#utilisation-avance-du-terminal-astuces-pour-gagner-du-temps)
- [Outils pour le réseau](#outils-pour-le-rseau)
  - [Outils en ligne de commande pour le réseau](#outils-en-ligne-de-commande-pour-le-rseau)
  - [Applications mobiles](#applications-mobiles)
  - [Outils Web](#outils-web)


# L'interface ligne de commande (ILC)
L'interface ligne de commande ou *command line interface* (CLI) est un outil qui permet d'interragir avec la machine via des commandes et des messages textuels.
L'utilisateur transmet des ordres à la machine en entrant des commandes en forme de texte (ex : `ls`) et la machine retourne un résultat sous forme de texte (ex : `image.png rapport.txt program.class`). L'interface en ligne de commande est une alternative aux interfaces graphiques dans lesquels l'utilisateur interragit avec la machine en cliquant avec la souris sur des éléments visuels (ex : icones, menus, boutons, etc.).

## Qu'est-ce qu'une commande ?

Une commande est un ordre écrit destiné à la machine que l'on entre généralement dans un terminal. Une commande suit un format spécifique qui ne supporte généralement pas les approximations (ex : `cd ..` vs `cd..`, `ls fichier1.txt` vs `ls Fichier1.txt`).  
Une commande est généralement composée de trois éléments : `commande` `options` `arguments`
* la `commande`, ou plus précisément le nom de la commande, identifie l'opération à éffectuer ;
* les `options` spécifient le fonctionnement de la commande et sont généralement optionelles ;
* les `arguments` désignent des données ou des fichiers qui seront utilisés par la commande (ne sont pas toujours nécessaires, ex : `ls`) ;

Prenons l'exemple de la commande `ls -l ./` qui permet d'afficher le contenu du répertoir courant en format long. `ls` désigne la commande *list*, `-l` spécifie l'option *long listing format*, et `./` est un argument qui désigne le répertoire courant.  


## Arborescence et chemin

Un système de fichier est une arborescence composée de fichier et de répertoire. Un répertoire peut contenir plusieurs répertoires et fichiers.
Dans l'exemple suivant, le répertoire `Java` contient deux répertoires `Jeudelavie` et `Projet`, tandis que le répertoire `Jeudelavie` contient deux fichiers `JeuDeLaVie.class` et `JeuDeLaVie.java`.

```Java/
├── Jeudelavie
│   ├── JeuDeLaVie.class
│   └── JeuDeLaVie.java
└── Projet
    └── UML.png
```


Un élément de cette arborescence est identifié par son chemin qui est constitué des différents répertoires qu'il faut traverser pour l'atteindre. Dans l'exemple précédent, pour atteindre le fichier `JeuDeLaVie.java` depuis le haut de l'arborescence, il faut traverser les répertoires `Java` puis `Jeudelavie` ; le chemin de ce fichier est donc `Java/Jeudelavie/JeuDeLaVie.java`. Sous GNU/Linux et Mac, les éléments du chemin sont séparés par le symbole `/` tandis que sous Windows on utilisera `\`.


### Le répertoire courant

A tout moment lors de l'utilisation de la ligne de commande, celui-ci se situe dans un répertoire courant. Le répertoire courant désigne celui à partir duquel les commandes sont executés, il est donc important de le prendre en considération (et éventuellement de le changer via la commande `cd`) lorsque l'on utilise la ligne de commande. 

Dans l'exemple précédent, supposons que le répertoire courant est `Java` ; pour atteindre le fichier `JeuDeLaVie.java`, il faudra préciser le chemin à traverser pour atteindre le fichier : `Jeudelavie/JeuDeLaVie.java`. 

### Les raccourcis `.` `..`
Dans le cadre de l'ILC il existe des raccourcis qui permettent de désigner certains répertoires :
* `.` désigne le répertoire courant
* `..` désigne le répertoire parent
* `~` désigne le répertoire "home" de l'utilisateur (celui dans lequel il stocke ses fichiers)
* 
Si je me trouve dans le répertoire `Java/Jeudelavie`, la commande `cd ..` changera le répertoire courant en `Java` (on est remonté d'un cran dans l'arborescence) tandis que `cd .` n'aura aucun effet (on demeure dans le même répertoire). 

## Commandes populaires 

|commande|nom|description| exemple |
|:---------:|-----------|---------------|---------------------------------|
|`cd`| change directory| change the current directory | `cd /home/` |
|`ls`| list  | affiche le contenu d'un repertoire | `ls .`|
|`tree`| tree | affiche le contenu d'un répertoire sous forme d'arbre | `tree /home/`|
|`cp`| copy | copie un fichier | `cp source destination` | 
|`mv`| move | déplace/renome un fichier | `mv fichier1.txt Dir/fichier2.txt`|
| `mkdir`| make directory | créé un répertoire | `mkdir NewDir`|
|`cat`| cat | affiche le contenu d'un fichier | `cat fichier1.txt`|
| `grep` | grep | recherche dans un fichier | `grep "mot" fichier.txt`|
| `zip`| zip | créé une archive au format zip | `zip archive.zip fichier1 fichier2`|
| `unzip`| unzip | extrait le contenu d'une archive zip | `unzip archive.zip` |
| `man`| manual | affiche le manuel d'utilisation d'une commande | `man ls`|
| ...| | | |

### Commandes spécifiques à Windows
...
 
### `man` a.k.a le manuel 
La plupart des commandes sont accompagnées d'un *manuel* d'utilisation qui décrit le fonctionnement de la commande ainsi que les différentes options et arguments possibles. Pour consulter le manuel d'une commande, on peut utiliser la commande `man`. Par exemple pour consulter le manuel de la commande `ls`, on peut utiliser `man ls`.

La commande `man` nous fait entrer dans un mode de consultation de texte au sein duquel il faut naviguer (via les flèches haut et bas) et dont il faudra sortir à un moment (via la touche *q*).



 
 
## Accéder à l'ILC (ouvrir un terminal)
L'accès à l'ILC se fait via un programme dédié que l'on appelle *terminal*. Il existe plusieurs manières de lancer un terminal :
### Ouvrir un terminal sous GNU/Linux
* La combinaison `Ctrl-Alt t` lance le terminal par défaut
* Le sous-menu "Application>Outils Systèmes" contient plusieurs terminaux (ex : "Terminator", "Terminal", etc.)

### Ouvrir un terminal sous Windows
* Dans le champ *recherche* du menu démarrer, tapez `cmd` puis entré.

### Ouvrir un terminal sous MacOS
* Dans spotlight (`CMD+espace`), tapez `terminal`

## Utilisation avancée du terminal (astuces pour gagner du temps)

### Autocomplétion
La touche `Tab ↹` permet de compléter automatiquement une commande. Cela évite de tapper des commandes parfois très longues et donc de gagner du temps.

Exemple : Dans le repertoire courant, il y a un répertoire nommé `Directory` dans lequel l'utilisateur souhaite passer grâce à la commande `cd Directory`.
Au lieu d'entrer la commande complète, l'utilisateur va faire appel à l'autocomplétion en entrant le début de la commande `cd D` puis en appuyant sur la touche Tab ↹ qui complètera automatiquement la fin de la commande pour obtenir `cd Directory`. L'autocomplétion ne lit pas dans les pensées de l'utilisateur, mais devine la commande de l'utilisateur sur la base de ce qui a déjà été entré (`cd D`) et du contexte (il existe un seul répertoire commencant par `D` et c'est `Directory`).

### Historique des commandes
Le terminal conserve généralement un historique des commandes executées et il est possible de naviguer dans cet historique pour y récupérer des commandes antérieurs. Cette navigation s'effectue via les touches flèches haut/bas du clavier. 

Exemple : l'utilisateur vient d'executer une commande longue `cp -rf file Directory/doc/bt/logs/2021-04-01/` et souhaites la modifier ou l'executer à nouveau. Plutôt que de réécrire cette commande une deuxième fois, l'utilisateur peut utiliser la flèche haut pour récupérer la commande précédente. Le gain de temps est significatif 1 touche appuyé contre 46 touches si on devait retapper l'intégralité de la commande.
Les touches 


# Outils
## Outils en ligne de commande pour le réseau

|commande|nom|description| exemple |
|:---------:|-----------|---------------------------------------------|-----------------------------|
|`ping`| ping | envoie d'une requete ICMP echo request à une machine | `ping 127.0.0.1` |
|`traceroute`| traceroute | affiche le chemin réseau pour rejoindre un hote distant | `traceroute example.com`|
|`ifconfig`| ifconfig | affichage et configuration des paramètres réseaux de la machine | `ifconfig` | 
|`telnet`| telnet | outil de communication avec un hote distant| `telnet towel.blinkenlights.nl `|
|`nc`| netcat | creation de connexions TCP ou UDP | `netcat 127.0.0.1 80`|
|`dig`| domain information groper | interrogation des serveurs de nom DNS |`dig insa-lyon.fr`|
|... | | | |

### Commandes réseau spécifiques à Windows
- netcat : <https://joncraton.org/blog/46/netcat-for-windows/>
- git-Bash : <https://gitforwindows.org/>
- network stuff : <http://jacquelin.potier.free.fr/networkstuff/>

## Applications mobiles pour le réseau
- PingTools  (Android) <https://play.google.com/store/apps/details?id=ua.com.streamsoft.pingtools>
- iNetTools (iOS) <https://apps.apple.com/fr/app/inettools-ping-dns-port-scan/id561659975>

## Outils Web
- ping.eu <https://ping.eu/>
-	PingTool.org <https://pingtool.org/>
- GeoTraceroute.com <https://geotraceroute.com/>

## Autres commandes
|Commande|Description| Exemple |
|:---------:|---------------------------------------------|-----------------------------|
|`java`| Exécute un programme Java présent dans le dossier courant  | `java MaClasse` |
|`javac`| Compile un programme Javatraceroute présent dans le dossier courant | `javac MaClasse.java`|

