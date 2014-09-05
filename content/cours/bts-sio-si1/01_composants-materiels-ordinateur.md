---
title: "Composants matériels de l'ordinateur"
url: /cours/composants-materiels-ordinateur
---

L'objectif de ce chapitre est de vous présenter ce qu'est un ordinateur
ainsi que les bases de son fonctionnement.

{{% image src="calvin_computer.jpg" class="centered" %}}

# Généralités sur les ordinateurs

## Qu'est-ce qu'un ordinateur ?

Le dictionnaire Larousse définit l'ordinateur de la manière suivante :

> Un ordinateur est une machine automatique de traitement de l'information, obéissant à des programmes formés par des suites d'opérations arithmétiques et logiques.

L'ordinateur n'est donc rien de plus qu'une machine qui effectue des opérations logiques et arithmétiques à la chaîne.

{{% remark %}}
Le terme "ordinateur" est générique. Il peut désigner aussi bien un ordinateur de bureau classique qu'un serveur de calcul ou encore un terminal mobile.
{{% /remark %}}

{{% question %}}
Trouvez des exemples d'ordinateurs.
{{% /question %}}

Tout ordinateur, même très performant, n'est qu'une **machine** capable d'exécuter automatiquement une série d'opérations qu'on lui a demandées. Il ne dispose par lui-même d'aucune capacité d'apprentissage, de jugement, d'improvisation, bref d'aucune "intelligence". Il se contente de **faire ce qu'on lui dit de faire**. L'intérêt des ordinateurs est de savoir manipuler très rapidement et sans erreur d'énormes quantités d'informations.

Tout ordinateur est composé de plusieurs types d'éléments en interaction :

* Des éléments matériels : processeur, mémoire, etc.
* Un système d'exploitation qui permet d'exploiter les éléments matériels.
* Des applications, logiciels utilisant le système d'exploitation pour offrir des fonctionnalités à l'utilisateur de l'ordinateur.

## Un peu d'histoire

Même si l'histoire ancienne a vu l'apparition de diverses machines à compter et à calculer (boulier, Pascaline, etc), l'informatique est une science très récente dont voici les principales étapes.

### 1945-1956 : les ordinateurs mécaniques

Les ordinateurs de cette génération sont surtout caractérisés par le fait que les instructions qu'ils comprennent correspondent spécialement à la tâche pour laquelle l'ordinateur a été conçu. Ils n'avaient aucune souplesse et des possibilités très limitées, concentrées sur une seule tâche précise. Ils utilisent également des tubes à vide (également appelées des lampes), ce qui explique leur taille, leur poids et leur consommation immense.

**ENIAC** (*Electronic Numerical Integrator And Computer*) est un très bon exemple d'ordinateur de première génération. Il n'était qu'une gigantesque et rapide calculatrice. On définissait un "programme" en branchant tout un ensemble de câbles.

{{% img eniac.jpg %}}

### 1956-1963 : les ordinateurs à transistors

L'invention du **transistor** en 1947 bouleverse le développement des ordinateurs. Remplaçant les tubes à vide un peu partout (télévisions, radios), il a été utilisé dans un ordinateur pour la première fois en 1956, par Bell.

{{% img premier_transistor.jpg %}}

Cette même année, IBM (*International Business Machines*, société fondée en 1940) met au point le premier disque dur, constitué d'une pile de 50 plateaux de 61 cm de diamètre. Il peut stocker 5 Mo.

{{% img premier_disque_dur.jpg %}}

À partir de 1960, les ordinateurs à transistors commençaient à incorporer efficacement des périphériques que l'on considère maintenant comme courants: disques magnétiques, enregistreurs à bandes magnétiques, imprimantes, mémoire. Ils avaient également des systèmes d'exploitation rudimentaires et on pouvait stocker des programmes en mémoire.

Ces programmes stockés en mémoire et la possibilité d'aller modifier ces programmes pour leur faire réaliser d'autres fonctions ont donné à l'ordinateur la flexibilité qui leur manquait. Ils permettaient d'utiliser des mots, des phrases et des formules mathématiques plus proches du langage humain.  L'industrie du logiciel a commencé à se développer.

### 1964-1971 : les ordinateurs à circuits intégrés

Le transistor était un bon pas en avant par rapport aux tubes à vide, mais il générait beaucoup de chaleur et endommageait souvent les parties internes sensibles de l'ordinateur. L'apparition du circuit intégré en 1964 a révolutionné le monde de l'informatique. Le premier circuit intégré réunissait trois composants électroniques sur un même (petit) support. Son arrivée a permis de diminuer encore la taille des ordinateurs, ainsi que leur consommation et leur émission de chaleur.

En 1967, IBM construit le premier lecteur de disquettes, qui devient un moyen populaire de stocker des données temporairement beaucoup plus pratique que les bandes magnétiques.

Un autre développement propre à la troisième génération: l'amélioration et l'utilisation courante des systèmes d'exploitation, un programme central qui gérait la mémoire de l'ordinateur et permettait de faire
tourner plusieurs programmes sur un même ordinateur – les ancêtres de Windows !

### Depuis 1971 : la micro-informatique

Avec l'apparition des circuits intégrés, la tendance est allée vers la miniaturisation. Depuis les années 80, on est capable de mettre plusieurs centaines de milliers, voire des millions de composants sur un support de la même surface. Tout ceci permis de réduire considérablement la taille et le coût des ordinateurs, tout en améliorant leur puissance et leur fiabilité. Le microprocesseur est né.

Sa généralisation pousse des compagnies comme Tandy, Commodore et Apple à commercialiser les premiers ordinateurs personnels. En 1981, IBM lance son premier ordinateur personnel: l'IBM PC (il crée du même coup officiellement le terme). IBM donnant le droit à n'importe qui de copier son architecture : les clones de PC apparaissent partout, faisant baisser grandement les prix et rendant le PC le choix de millions d'utilisateurs.

{{% img ibm_pc.jpg %}}

En 1984, le premier concurrent direct du PC d'IBM fait son entrée sur le marché: le MacIntosh d'Apple. Il est le premier à offrir un système d'exploitation graphique, laissant l'usager déplacer des icônes et des fenêtres avec une souris plutôt que de taper des commandes étranges avec un clavier.

{{% image src="apple_macintosh.jpg" class="centered" %}}

C'est à cette époque qu'apparaissent les premiers ordinateurs portables, ou plutôt transportables tant leur poids (plus de 10 kg) et leur prix étaient dissuasifs.

{{% img premier_transportable.jpg %}}

### De nos jours : des ordinateurs partout

L'époque actuelle se caractérise par une course à la puissance et à la miniaturisation des composants de l'ordinateur, liée à la concurrence que se livrent les fabricants de matériel.

Cette évolution, ainsi que la généralisation de l'accès aux réseaux, a eu pour conséquence l'explosion de l'informatique mobile, avec des terminaux (smartphones, tablettes) disposant de la même puissance que les ordinateurs de bureau d'il y a quelques années...

{{% image src="familles_ordinateurs.jpg" class="centered" %}}

# Généralités sur les logiciels

## Définition

{{% question %}}
Faites une liste de logiciels que vous connaissez.
{{% /question %}}

Chaque logiciel assure une tâche particulière pour répondre à un besoin précis.

> Un logiciel est un programme qui permet à un système informatique d'assurer une tâche particulière (Wikipédia).

Pour fonctionner, un logiciel exploite les ressources matérielles du système informatique qui l'héberge.

## Les différents types de logiciels

On distingue deux grandes familles de logiciels :

* Les logiciels système, appelés égalements **systèmes d'exploitation**.
* Les logiciels d'application

{{% question %}}
Trouvez des exemples de logiciels système.
{{% /question %}}

On peut catégoriser les logiciels d'application selon le type de tâche qu'ils réalisent.

{{% question %}}
Trouvez des catégories de logiciels d'application.
{{% /question %}}

Les logiciels d'application utilisent les services offerts par le logiciel système qui les accueille.

{{% image src="imbrication_logiciels.jpg" class="centered" %}}

## La création d'un logiciel

### Le processus de création

L'origine d'un logiciel est un ensemble de fichiers appelé **code source**. Ces fichiers sont écrits par un ou plusieurs programmeurs dans un langage particulier. En fonction du langage choisi, les fichiers source sont :

* transformés par un logiciel appelé **compilateur** en un ou plusieurs fichiers exécutables (extension *.exe* sous Windows).
* directement exécutés par un **interpréteur**.

De nos jours, de nombreux outils aident les programmeurs à créer des logiciels plus rapidement (génération d'une partie du code source, création de l'interface graphique...).

### Les erreurs (bogues)

Plus le logiciel créé est complexe, plus il est difficile d'éviter les bogues (*bugs*) dans sa conception.

{{% definition %}}
Un bogue est une erreur dans le code source du logiciel qui provoque un effet inattendu pendant son exécution.
{{% /definition %}}

## La distribution d'un logiciel

Le logiciel, création de l'esprit, est protégé par le droit. Son auteur est libre de choisir son mode de distribution à travers le choix d'une licence. On peut classer les logiciels en quatre catégories principales selon leur mode de distribution :

* Les **logiciels commerciaux** sont propriétaires et payants.
* Les **partagiciels** (*sharewares*) sont gratuits pour une période donnée, puis payants.
* Les **graticiels** (*freewares*) sont disponibles gratuitement, parfois en version bridée.
* Les **logiciels libres** donnent à toute personne qui en possède une copie le droit de les utiliser, de les étudier, de les modifier et de les redistribuer. Ils sont fournis avec leur code source, et on rencontre parfois l'expression "open source" pour qualifier ces logiciels.

{{% image src="copyleft.png" class="centered" %}}

{{% question %}}
Trouvez des exemples de logiciels pour chaque mode de distribution.
{{% /question %}}

Il existe d'autres modes de distribution plus "exotiques" (carticiel, abandogiciel...).

# Architecture d'un ordinateur

Même si un ordinateur peut prendre des formes très différentes, du serveur au smartphone en passant par le PC du bureau, son architecture de base est identique d'un modèle à l'autre. Seule la taille (et les performances) de ses éléments changent.

Un ordinateur se compose de plusieurs éléments matériels en interaction. L'image ci-dessous illustre l'architecture d'un PC de bureau (source : Wikipedia).

{{% image src="eclate_ordinateur.png" class="centered" %}}

# La carte mère

{{% remark %}}
Ce paragraphe reprend un cours de mon collègue Pascal Chemin.
{{% /remark %}}

## Le rôle de la carte mère

La carte mère est l’élément central d’un ordinateur. 

{{% img carte_mere.png %}}

Elle assure l'interconnexion entre tous les autres composants.

## Le format (ou facteur d’encombrement)

Le format d’une carte mère définit :

* ses dimensions,
* les emplacements des points de fixation,
* le type d’alimentation à utiliser.

Les formats des cartes mère sont fortement liés aux formats des boîtiers.

On trouve essentiellement trois types de formats pour une carte mère récente.

  **Format**  | **Format de boitier**          | **Dimensions**
  ------------|--------------------------------|----------------
  ATX         | Ordinateur de bureau           | 305x244 mm
  Micro ATX   | Ordinateurs de bureau compacts | 244x244 mm
  ITX         | Mini PC                        | 177x177mm

{{% image src="form_factors.png" class="centered" %}}

* **Le format ATX**. Ce sont les cartes mères de plus grande taille. Il faudra généralement un boîtier spacieux pour l’accueillir, muni d’une alimentation ATX. C’est le format de carte mère le plus répandu.

* **Le format micro ATX**. Format de carte compact. Il convient généralement aux boîtiers de type munis d’une alimentation ATX.

* **Le format ITX**. Format de carte mère ultracompact destiné exclusivement aux PC munis d’une alimentation ITX.

## Le support processeur (socket)

{{% definition %}}
Le socket est le support qui permet au processeur d'être branché sur la carte mère.
{{% /definition %}}

{{% image src="socket.png" class="centered" %}}

Le socket est un réceptacle couvert de contacts. Le processeur va s’emboîter dans le réceptacle, les différents contacts vont s’établir par une pression sur un levier.

Le type de support de votre carte mère peut être identifié grâce à des logiciels de diagnostic comme [AIDA64](http://www.aida64.com/) ou [Sandra](http://www.sisoftware.net)  

La [page Wikipedia associée au socket](http://fr.wikipedia.org/wiki/Socket_\(processeur\)) donne toutes les informations nécessaires.

## Le support mémoire

Les cartes mères disposent de plusieurs supports mémoire permettant de connecter de la **mémoire vive** (RAM, *Random Access Memory*) sous la forme de barrettes.

{{% img carte_mere_ram.jpg %}}

Avant un achat, il est important de vérifier la compatibilité des barrettes avec la carte mère.

## Les *chipsets*

Les chipsets sont des **composants** de la carte mère chargés de gérer les flux entre les différents composants de l’ordinateur.

On trouve deux composants essentiels à la carte mère qui se partagent les communications en fonction de la vitesse de communication et du nombre d’informations échangés :

* Le *northbridge* ("pont nord") gère les échanges de données entre les composants ayant besoin d’échanger un très grand nombre d’informations dans un laps de temps très faible :

    * Processeur,
    * Mémoire vive
    * Carte graphique

\

* Le *southbridge* ("pont sud") gére les échanges de données entre les composants ayant besoin d’échanger un nombre plus faible d’informations : les périphériques d’entrée et sortie.

{{% image src="schema_bus_CM.png" class="centered" %}}

Les chipsets déterminent quels composants sont supportés :

* le processeur,
* les mémoires,
* les types de ports gérés (USB, PCI Express, AGP, SATA, etc.).

{{% question %}}
Trouvez les noms des principaux constructeurs de *chipsets*.
{{% /question %}}

Evolutions récentes :

* Le northbridge traditionnel est destiné à disparaître. 

* Le contrôleur mémoire, qui assure la communication entre le processeur et la RAM, a été intégré dans le cœur des processeurs AMD64 ou Intel Core i7.

## Les ports internes

Parmi les ports interne d'une carte mère, les **ports d’extension** permettent de connecter des cartes supplémentaires dans votre PC. Les cartes les plus courantes sont :

* les cartes graphiques,
* les cartes son,
* les cartes réseau.

### Les port PCI et PCI Express

Le port PCI se trouve encore sur les cartes mères, mais ce type de port est en perte de vitesse. Il propose des débits trop faibles pour supporter certaines cartes. Il est remplacé par les ports PCI Express. Le débit de ces ports est beaucoup plus important.

{{% img ports_pciexpress.jpg %}}

Ces ports sont différents physiquement comme le montre ce schéma. Plus l’indice multiplicateur est élevé plus le débit proposé est important.

### Le port ATA

Il est destiné à la connexion de disques durs ou de lecteurs optiques. Il s'agit d'une ancienne norme en voie de disparition. La connexion du composant se fait grâce à une nappe plate de 40 à 80 fils munie de 3 connecteurs.

{{% img port_pata.png %}}

Les connecteurs ATA sur les cartes mères sont encore largement répandus, mais leur nombre a diminué : la plupart des cartes mères n’offrent plus qu’un seul port ATA.

### Les ports SATA (SATA2, SATA3)

Cette norme vient remplacer l’ancien standard ATA. Cette technologie propose des débits plus importants que la norme ATA particulièrement pour les normes SATA2 et SATA3 qui offrent un débit théorique plusieurs fois supérieur au SATA1.

{{% img port_sata.png %}}

La norme SATA présente d’autres avantages :

* Les câbles Serial ATA peuvent mesurer jusqu’à 1 mètre de long (contre 45 cm pour les nappes ATA).
* Le faible nombre de fils dans la gaine donne plus de souplesse au câble et contribue à une meilleure circulation de l’air dans le boîtier.
* Les périphériques SATA sont seuls sur chaque câble et il n’est plus nécessaire de définir des périphériques ATA maîtres et esclaves.

## Les ports externes

{{% image src="ports_externes_CM.png" class="centered" %}}

### Le port USB

C’est un port extrêmement connu pour son caractère universel. On peut connecter une multitude de périphériques sur ce type de port (imprimante, scanner, disque dur, clavier, webcam, clé...).

Il existe trois types de port USB, les types USB1, USB2 et USB3. Le type USB2 est deux fois plus rapide que le type USB1 en termes de débit. Le type USB3 est encore plus rapide que l’USB2.

### Le port eSata

Ce type de port est apparu récemment sur les cartes mères. C'est une version externe des ports SATA.

{{% img port_esata.png %}}

Le débit proposé par cette technologie est très rapide, les taux de transfert sont identiques à la version interne. Ce type de port est donc particulièrement adapté pour des disques durs externes.

### Les ports PS2, parallèle, série

L’ensemble de ces ports a quasiment disparu des cartes mères actuelles.

* Le port PS2 est destiné à connecter un clavier ou une souris.
* Les ports parallèles autorisent l’utilisation d’une imprimante.
* Les ports série (ports RS-232) sont fréquemment utilisées dans l'industrie pour connecter différents appareils électroniques (automate, appareil de mesure, etc.) et des actifs réseau (routeurs).

Les ports série sont souvent désignés par les noms COM1, COM2, etc. Cela leur a valu le surnom de « ports COM », encore utilisé de nos jours.

## Le réseau

### Réseau filaire

La quasi-totalité des cartes mères possède une voire plusieurs prises réseaux (RJ45). Ces connecteurs supportent différents taux de transfert, les plus courants sont 100 Mbit/s ou 1 Gbit/s (1000 Mbit/s).

{{% img port_rj45.png %}}

### Réseau sans fil

Certaines cartes mères récentes intègrent les fonctionnalités des cartes Wi-Fi. Elles prennent en charge la plupart des normes actuelles à savoir 802.11b et 802.11g. Ces cartes mères sont généralement pourvues d’un connecteur pour une antenne Wi-Fi.

## Le multimédia

### Audio

Les cartes mères intègrent depuis de nombreuses années des cartes son. Autrefois de piètre qualité et limitées à la stéréo, les cartes son intégrées ont beaucoup progressé en qualité et délivrent désormais un son multicanal (5.1, 7.1). Néanmoins, elles n’arrivent pas au degré de qualité et de performance que peut offrir une carte son séparée connectée sur un port PCI ou PCI Express.

### Vidéo

Les cartes mères récentes intègrent souvent un circuit graphique intégré qui joue le rôle de carte graphique. Les performances de ces circuits sont souvent modestes et peu en adéquation avec une utilisation ludique du PC (jeux !).

Une carte mère récente propose maintenant :

* un connecteur VGA (signal analogique) et
* un connecteur DVI (Digital Visual Interface, signal numérique)) et/ou
* un connecteur HDMI (High Definition Multimedia Interface, signal numérique qui délivre à la fois l’image et le son).

## Le BIOS

{{% definition %}}
Le BIOS est le programme chargé d’initialiser l’ordinateur avant le démarrage du système d’exploitation.
{{% /definition %}}

Les informations de base concernant la configuration du matériel d’un ordinateur sont stockées dans une puce appelé CMOS (Complementary Metal Oxide Semiconductor) qui est gardée sous alimentation constante par la batterie de sauvegarde (pile ou accumulateur) de l'ordinateur. L’utilisateur peut paramétrer le BIOS selon ses besoins.

Les BIOS varient d’un constructeur à l’autre, par le nombre d’options et l’ergonomie. Des mises à jour du BIOS sont régulièrement disponibles sur le site du constructeur. Ceci pour corriger des problèmes de conception du programme ou proposer des fonctionnalités ou des technologies supplémentaires

{{% img bios.png %}}

Pour accéder au paramétrage du BIOS, il faut souvent au démarrage du PC utiliser une touche ou une combinaison de touches : `DEL`, `F2`, `F10`...

## La notion de bus

{{% definition %}}
Un bus informatique est un système de communication partagé entre plusieurs composants d'un système numérique. Il s'agit d'un ensemble de liaisons physiques (câbles, pistes de circuits imprimés, etc.) pouvant être exploitées en commun par plusieurs éléments matériels afin de communiquer.
{{% /definition %}}

Au sein d'une carte mère coexistent différents **bus**.

* **Bus mémoire** (ou **bus processeur** ou *front-side-bus*, noté **FSB**) : permet au processeur de communiquer avec la mémoire vive du système.

* **Bus de données interne** : véhicule les instructions en provenance ou
à destination du processeur.

* **DMA** (*Direct Memory Access*) : bus qui permet l'accès direct à la mémoire vive sans passer par le
processeur (permet ainsi une accélération importante des performances).

Le rôle d'un bus est le transport de données. Sa vitesse, appelée débit binaire, est la quantité de bits pouvant y transiter par unité de temps. Il se calculera en bits par seconde, ou en octets par seconde.

La vitesse d'un bus dépend du nombre de lignes physiques sur lesquelles les données sont envoyées de manière simultanée. Une nappe de 32 fils permet ainsi de transmettre 32 bits en parallèle. On parle ainsi de
largeur pour désigner le nombre de bits qu'un bus peut transmettre simultanément.

D'autre part, la vitesse du bus est également définie par sa fréquence (exprimée en Hertz), c'est-à-dire le nombre de paquets de données envoyés ou reçus par seconde. On parle de cycle pour désigner chaque envoi ou réception de données.

Lorsque les bits sont convoyés les uns à la suite des autres sur une seule et même ligne, on parle alors de **bus série* (*serial bus*). Exemples : USB, SATA.

Lorsque les bits sont véhiculés simultanément sur plusieurs lignes parallèles, on parle alors, ô surprise, de **bus parallèle** (*parallel bus*). Exemple : PATA.

{{% image src="bus_serie_parallele.png" class="centered" %}}
