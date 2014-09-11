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

# Le processeur

## Introduction

Le processeur, appelé en anglais CPU (*Central Processing Unit*) est à la
fois le cerveau et le coeur de l'ordinateur :

* Le cerveau, car son rôle est d'exécuter les instructions qui composent les programmes informatiques.

* Le coeur, parce qu'il exécute ces instructions au rythme (très rapide) de son horloge interne, appelé sa fréquence.

Il est le plus souvent construit en un seul composant électronique (ou puce électronique) appelé **circuit intégré**. On l'appelle alors microprocesseur. Sur ce circuit sont assemblés un nombre énorme (actuellement plus d'un milliard) de composants électroniques semi-conducteurs appelés des transistors.

{{% image src="processeur.jpg" class="centered" %}}

## Histoire des processeurs

Les premiers processeurs sont apparus en même temps que les premiers ordinateurs, dans les années 1940. A l'époque, ils étaient prévus spécifiquement pour une machine donnée. Dans les années 1970 sont apparus les premiers processeurs capables de fonctionner sur plusieurs machines (la société Intel a fabriqué son premier processeur en 1971). Cette standardisation s'est accélérée avec l'apparition des circuits intégrés, qui ont permis la miniaturisation des processeurs.

Depuis, les progrès scientifiques et industriels ont conduit à une augmentation constante de la densité de transistors sur un même circuit intégré. Le co-fondateur d'Intel, Gordon Moore, a formulé en 1965 une prédiction célèbre appelée depuis **loi de Moore** : "le nombre de transistors sur un microprocesseur doublera approximativement tous les deux ans".

A l'époque, le circuit le plus performant comportant 64 transistors. De nos jours, un processeur Core i7 comporte plus d'un milliard de transistors !

{{% img processeur_nombre_transistors.jpg %}}

{{% question %}}
Trouvez les noms des principaux fabricants de processeurs.
{{% /question %}}

## Types de processeur

### Pour ordinateur de bureau

Les ordinateurs de bureau permettent généralement d’exécuter des applications telles que des logiciels de traitement de texte, des feuilles de calcul et des applications réseau de type messagerie et navigation Web.

Exemples de processeurs de bureau récents pour Intel et AMD : Celeron, Pentium, Core i3, i5, i7, Phenom, Athlon, Sempron.

### Pour ordinateur portable

Les processeurs pour ordinateur portable sont conçus pour avoir une consommation d’énergie réduite. L’autonomie d’un ordinateur portable lorsqu’il fonctionne sur batterie est une caractéristique importante. Pour obtenir une consommation moindre, les processeurs d’ordinateurs portables sont alimentés par une tension plus faible et fonctionnent généralement à des fréquences moins élevées que les ordinateurs de bureau.

AMD et Intel déclinent pour les ordinateurs portables des versions de leurs processeurs pour ordinateur de bureau.

### Pour station de travail

Les stations de travail sont de puissants ordinateurs d’entreprise. Elles sont conçues pour exécuter des applications de pointe, spécialisées, comme les programmes d’ingénierie, par exemple la CAO (Conception Assistée par Ordinateur). Les stations de travail sont utilisées dans la conception d’images 3D, l’animation vidéo. Elles peuvent également servir de stations de gestion d’équipements médicaux ou de télécommunications.

{{% image src="station-travail.png" class="centered" %}}

Les stations de travail possèdent plusieurs processeurs qui doivent gérer une importante quantité de mémoire vive et plusieurs disques durs haute capacité, très rapides.

Exemples pour Intel et AMD : Xeon, Itanium, Opteron + séries E et C.

### Pour serveur

Le matériel serveur est optimisé afin de fournir des réponses rapides à différentes requêtes réseau. Les serveurs peuvent être sollicités par plusieurs dizaines à plusieurs milliers de logiciels clients à la fois.

Il existe plusieurs formats de serveurs :

* Serveurs tour : adaptés aux plus petites entreprises.
* Serveur rack : empilables dans des baies dédiées.
* Serveurs lame (*blade*) : concentrent le maximum de puissance et d’évolutivité

{{% image src="format-serveurs.jpg" class="centered" %}}

Les serveurs sont dotés de plusieurs processeurs qui accèdent à une quantité importante de mémoire vive.

Exemples pour Intel et AMD : Xeon, Opteron série 4000 et 6000.

## Caractéristiques des processeurs

### La fréquence

La fréquence ou vitesse d'horloge est un concept relativement simple à
comprendre. Elle se mesure actuellement en GigaHertz (GHz) et correspond
au nombre d’opérations élémentaires que le processeur est capable
d’effectuer en une seconde.

Ainsi, un processeur fonctionnant à une fréquence de 3 Ghz peut traiter 3 milliards d'opérations élémentaires à la seconde.

### Les registres

Lorsque le processeur exécute des instructions, les données sont temporairement stockées dans de petites mémoires rapides de 8, 16, 32 ou 64 bits que l'on appelle registres.

Un registre est un emplacement de mémoire interne à un processeur. Les registres se situent au sommet de la hiérarchie mémoire : il s'agit de la mémoire au meilleur temps d'accès, mais dont le coût de fabrication est le plus élevé.

La largeur d’un processeur est un concept plus complexe, car trois caractéristiques du processeur s’expriment sous la forme d’une largeur :

* le bus d’entrées/sorties de données;
* le bus d’adresses;
* les registres internes.

{{% img processeur-largeur-registres.png %}}

Le bus de données du processeur se nomme également FSB (*Front-Side Bus*), PSB (*Processor Side Bus*) ou simplement bus processeur. Tous ces termes font référence au bus qui se trouve entre le processeur et le pont nord (North Bridge).

### Les instructions

Une instruction est l'opération élémentaire que le processeur peut
accomplir. Les instructions sont stockées dans la mémoire principale, en
vue d'être traitée par le processeur.

Une instruction est composée de deux champs :

* le code opération, représentant l'action que le processeur doit accomplir ;
* le code opérande, définissant les paramètres de l'action. Le code opérande dépend de l'opération. Il peut s'agir d'une donnée ou bien d'une adresse mémoire.

Par exemple, l'opération A = B + C peut être traduite par la séquence suivante :

* **LOAD B R1** copie le contenu de l'adresse B dans le registre R1
* **ADD C R1** ajoute le contenu de l'adresse C dans ce registre
* **STORE R1 A** stocke le contenu du registre à l'adresse A

{{% image src="processeur-instructions.png" class="centered" %}}

Chaque type de processeur gère un ensemble d’instructions appelé jeu d’instructions.

Le jeu d'instructions est l'ensemble des opérations qu'un processeur peut exécuter,c'est-à-dire l'ensemble des circuits logiques qui y sont câblés. Ces circuits permettent d'effectuer des opérations élémentaires (addition, ET logique…) ou plus complexes (division, puissance…).

De ce point de vue, il existe deux familles : les processeurs **CISC** (*Complex Instruction Set Computer*) et les processeurs **RISC** (R pour *Reduced*).

* Les processeurs CISC embarquent de nombreuses instructions souvent très complexes mais prenant plusieurs cycles d'horloge.

* À l'opposé, les processeurs RISC ont un jeu d'instructions plus réduit mais chaque instruction n'utilise que quelques cycles d'horloge.

Chaque nouvelle génération de processeur étend le jeu d’instructions standard pour permettre d'améliorer les performances dans des domaines spécifiques (3D, multimédia, etc). Voici quelques exemples : instructions MMX (1997), SSE (1999), SSE4 (2007).

### La mémoire cache

La mémoire cache est une mémoire très rapide permettant de réduire les délais d'attente des informations stockées en mémoire vive. En effet, la mémoire centrale (RAM) de l'ordinateur possède une vitesse bien moins importante que le processeur.

Les processeurs modernes utilisent plusieurs mémoires caches s’intercalant entre le processeur et la mémoire centrale. On parle alors de niveau de cache : L1, L2 et L3 (L = Level). Le cache L1 est le plus rapide et le plus proche du microprocesseur, tandis que le cache L3 est le plus lent et plus proche de la mémoire vive.

{{% image src="processeur-memoire-cache.png" class="centered" %}}

### Le type de support (socket)

Chaque processeur est conçu pour être monté sur un support de carte mère précis, appelé **socket**.

### La finesse de gravure

La finesse de gravure d’un processeur correspond au procédé de fabrication utilisé pour fabriquer le cœur du processeur. Le procédé de fabrication consiste à "écrire" le plus finement possible les transistors qui sont la base de tout processeur pour assembler un plus grand nombre de transistors dans un espace plus réduit.

La finesse de gravure est exprimée en nanomètres (nm, 10-9 m). Elle représente le diamètre (en nanomètres) du plus petit fil reliant deux composantes du microprocesseur. En comparaison, l'épaisseur d'un cheveu humain est de 100 microns = 100 000 nm.

Plus la gravure est fine, plus le processeur va pouvoir :

* fonctionner rapidement.
* dissiper moins de chaleur.
* consommer moins de courant électrique.

Trouvez la finesse de gravure des processeurs PC récents.

### La consommation électrique

La consommation d’un processeur est exprimée en Watts. Elle dépend de nombreux facteurs et en particulier de la vitesse d'horloge.

Depuis quelques années, les préoccupations économiques et environnementales, ainsi que l'explosion du marché de la mobilité, ont conduit les fabricants de CPU à tenter de minimiser cette consommation, en particulier dans les versions mobiles de leurs processeurs.

## Technologies des processeurs

### La technologie du pipeline

Afin d'optimiser le rendement, la technique du pipeline est apparue sur les processeurs 80386 d'Intel en 1985. Le pipeline permet de commencer à traiter l'instruction suivante avant d'avoir terminé la précédente via un mécanisme de "travail à la chaîne".

Cette technologie permet d'économiser de nombreux cycles d'horloge et donc d'augmenter les performances.

### La technologie Hyper-Threading

L'hyperthreading consiste à émuler au sein d'un seul processeur physique deux processeurs logiques, ce qui permet d’occuper le processeur de plus d'instructions et améliore son rendement. Ces deux processeurs logiques partagent les éléments du cœur de processeur, le cache et le bus système. Ainsi, deux processus peuvent être traités simultanément par le même processeur.

{{% img processeur-hyperthreading.png %}}

{{% definition %}}
Un *thread* (ou fil) est une tâche élémentaire d'un programme en cours d'exécution. Les threads d'un programme peuvent s'exécuter en parallèle.
{{% /definition %}}

Sous Windows, on peut observer le nombre de threads grâce au
gestionnaire de tâches.

### La technologie multicœurs

Un processeur multicoeurs contient en réalité deux noyaux de processeur, ou plus, sur la même puce. De l’extérieur, il ressemble à un seul processeur. Un processeur multicoeurs possède tous les avantages d’un ensemble de processeurs physiques séparés, pour un coût moindre.

{{% img processeur-multicoeur.png %}}

# La mémoire                                                              

{{% remark %}}
Ce paragraphe s'inspire d'un cours de mon collègue Pascal Chemin.
{{% /remark %}}

## Généralités

Dans un ordinateur, la mémoire sert à stocker les informations manipulées par le processeur. Il existe plusieurs catégories de mémoire, adaptées à des usages différents. On peut les classifier en fonction de l’éloignement par rapport au processeur.

{{% img memoire-triangle-vitesse.png %}}

Plus la mémoire est proche du processeur, plus elle est rapide, de faible capacité et chère.

## La mémoire vive (RAM)

### Définition

La mémoire vive ou RAM (*Random Access Memory*) est la principale mémoire de travail de l'ordinateur. Elle est **volatile** : les données stockées en mémoire vive sont perdues à l'extinction de la machine. En contrepartie, la RAM est très rapide.

{{% question %}}
Estimez le débit des mémoires RAM actuelles.
{{% /question %}}

Les informations sont stockés dans les composants de mémoire vive, sous forme de charges électriques dans de minuscules condensateurs. Un condensateur chargé représente un 1 et un condensateur non chargé représente un 0. Les condensateurs se décharger naturellement, il faut entretenir la charge périodiquement. Ce processus est appelé **rafraîchissement de la mémoire**. La mémoire de ce type (nécessitant un rafraîchissement périodique) est appelée mémoire dynamique ou DRAM.

 : le débit de la mémoire vive actuelle est d'environ 15 Go/s.

### Echanges avec le processeur

On peut envisager la mémoire vive comme un gigantesque ensemble de cases, que le processeur utilise pour stocker des informations. Les échanges entre RAM et processeur se font au travers de différents bus : commandes, adresses, données. 

{{% img memoire-echanges-proc.png %}}

### Format des barrettes de RAM

Il existe de nombreux types de mémoires vives. Celles-ci se présentent toutes sous la forme de barrettes de mémoire enfichables sur la carte-mère. 

{{% image src="memoire-ram.png" class="centered" %}}

Les premières DRAM étaient de type asynchrone. Depuis 1997, elles sont synchrones(SD-RAM), elles échangent des données en se synchronisant avec le signal d’horloge. Depuis 2000, un nouveau standard est mis au point par Nec, Samsung et Toshiba : le DDR (*Double Data Rate*). Cette technologie permet de **doubler le taux de transfert** des DRAM. La technologie DDR2 est apparue en 2003, c’est une amélioration de DDR (débit plus important, consommation électrique réduite, dissipation thermique moins importante). La **technologie DDR3** est apparue en 2007. Les améliorations apportées sont de la même nature que DDR2.

La **dénomination** d’une mémoire DDR est fonction de son type DDR,
DDR2, DDR3 et de sa fréquence. Par exemple une mémoire DDR fonctionnant
à 333 MHz aura comme dénomination DDR333.

### Quantité de RAM

La capacité des mémoires vives actuelles est exprimée en GigaOctets (Go). PLus cette capacité est importante, plus l'ordinateur peut exécuter d'applications en parallèle ou lancer des logiciels gourmands en RAM (retouche photo ou vidéo, jeux, etc).

**Windows XP** nécessite un minimum de 256 Mo, de 512 Mo à 1 Go pour un usage bureautique, de 1 Go à 2 Go pour un usage avancé (retouche photo, montage vidéo, jeux). 

**Windows 7** nécessite plus de mémoire, 1 Go minimum, de 1 Go à 2 Go pour un usage bureautique, de 2 Go à 4 Go pour un usage avancé (retouche photo, montage vidéo, jeux).

{{% img w7-proprietes-syst.png %}}

### Fréquence de la RAM

Comme nous l’avons vu dans le chapitre sur la carte mère, la mémoire RAM est synchronisée sur la vitesse du bus (le FSB : *Front Side Bus*) de la carte mère dépendant du processeur qui l’équipe. Il convient donc d’utiliser des RAM se rapprochant le plus de cette fréquence sous peine que les performances soient diminuées. Pour un fonctionnement optimal, la RAM doit être "synchronisée" avec le processeur. 

### Temps de latence

La latence d’une mémoire est le temps nécessaire pour réaliser une opération de lecture ou d’écriture. Plus la latence est faible plus la mémoire est réactive... et plus son prix est élevé. La latence CAS (en anglais CAS Latence) permet d’évaluer les performances d’une mémoire. Le CAS Latence correspond au nombre de
cycles d’horloge nécessaires entre deux accès.

Sur le marché, vous trouverez des barrettes mémoires avec les
appellations (CL2, CL2.5, CL3, CL4 ou CL5). CL est l’abréviation de CAS
Latence suivi du nombre de cycles d’horloge.

{{% img memoire-latence.png %}}

### Crrection d’erreurs

Les mémoires standard, installées dans nos PC sont des mémoires non-ECC. Cette abréviation précise qu’elles ne contiennent aucun système de correction d’erreur. Il existe sur le marché des barrettes mémoires de type ECC (*Error-Correcting Code*) intégrant une technologie de correction d’erreur. Le mécanisme ECC détecte et corrige les erreurs ou les données corrompues. Ce type de mémoire est surtout utilisé pour les serveurs d’entreprise où la fiabilité et l’intégrité des données en mémoire vive sont très importantes.

Il existe des barrettes de mémoire de 32 bits ou 36 bits. Une barrette de mémoire de 32 bits contient exactement la même quantité de données qu'une barrette de 36 bits. Les quatre bits supplémentaires ne servent qu'à contrôler la validité des huit bits qui les précèdent (un **bit de parité** par groupe de huit bits). Le principe consiste à faire la somme des huit bits de données, puis à donner au neuvième la valeur 1 si le résultat est pair, et 0 si le résultat est impair. (On peut également faire le contraire. On parlera de **parité paire** dans le premier cas, et de **parité impaire** dans le second.)

De cette façon, si un des bits change de valeur par accident, l'erreur sera repérable car le bit de parité ne correspondra plus au résultat. Il peut sembler que la sécurité ainsi obtenue ne soit pas de très haut niveau. En effet, si un deuxième bit change de valeur, la parité est de nouveau correcte. Cependant, s'il y a une chance sur mille (par exemple) qu'une erreur se produise sur un bit, il y aura une chance sur un million pour que deux bits soient erronés. La sécurité obtenue n'est donc pas négligeable. Toutefois, le bit de parité ne permet pas de retrouver le bit erroné.

### Technologie Dual Channel

Les processeurs modernes ont des besoins très élevés en bande passante. La technologie Dual Channel est une réponse à ces nouveaux besoins. Le principe est d’associer deux canaux à deux barrettes de mémoires DDR pour doubler le débit entre la mémoire et le processeur.

Pour bénéficier de cette technologie, il faut que votre carte mère la supporte et installer deux barrettes de mémoire identiques dans les emplacements appropriés. Les emplacements Dual Channel sont d’une couleur différente du noir

{{% img memoire-dual-channel.png %}}

## La mémoire morte (ROM)

Ce type de mémoire est non volatile mais plus lente que la mémoire vive. Elle est utilisée pour stocker les données indispensables au démarrage de l’ordinateur :

* Le **BIOS**, Basic Input/Output System, programme permettant de piloter les interfaces d'entrée-sortie principales du système

* Le **Power-On Self Test** (POST), programme exécuté automatiquement à l'amorçage du système permettant de faire un test du système (comptage de la RAM par exemple).

{{% img memoire-rom.png %}}

Les ROM ont évolué de mémoires mortes figées à des mémoires programmables, puis reprogrammables :

* ROM : **Read Only Memory**
* PROM : **Programmable ROM**,
* EPROM : **Erasable PROM**,
* EEPROM : **Electrically EPROM, effaçables par un courant électrique d’où le terme de flash**,
* Flash qui est devenu un intermédiaire entre la mémoire morte initiale et la mémoire vive. Nous la reverrons avec les disques SSD (*Solid State Drive*).

## Le disque dur

### Description

Le disque dur est un type de mémoire de masse (non volatile) encore très répandu. 

{{% image src="disque-dur-exterieur.png" class="centered" %}}

Il est constitué d'un ou plusieurs plateaux et d'un bras mobile sur lequel se trouvent les têtes de lecture. Chaque face du plateau est divisée en pistes circulaires concentriques. Chaque piste se divise en secteurs qui sont des portions de pistes limitées par deux rayons. En général, un secteur contient 512 octets.

{{% image src="disque-dur-interieur.png" class="centered" %}}

Les disques durs sont des mécanismes de haute précision, sensibles au choc. L’électronique, aussi appelée **contrôleur disque dur**, est chargée de piloter la rotation des plateaux ainsi que l’ensemble bras/tête pour
effectuer les lectures et les écritures. Son autre rôle est d’interpréter les signaux électriques reçus par les têtes pour les convertir en bits (0 ou 1) ou de réaliser l’opération dans le sens inverse pour les opérations d’écriture.

Le nombre de plateaux varie de 1 à 5. Un nombre de plateaux important
est généralement nécessaire pour les disques durs de fortes capacités.

### Format

Il existe plusieurs formats de disques durs :

* Format 1,8" : pour les ordinateurs ultraportables. Ses performances sont souvent modestes à cause de faibles vitesses de rotation : 4200 ou 5400 tours/min.

* Format 2,5" : le format le plus courant pour les ordinateurs portables : 4200, 5400 et 7200 tours/min.

* Format 3,5" : pour les ordinateurs de bureau et les serveurs. Ce sont les plus performants : 7200, 10000,15000 tours/min.

### Mémoire cache

Cette mémoire de faible capacité permet d’améliorer les performances d’un disque dur en stockant les informations les plus souvent utilisées.

{{% question %}}
Quelle est la taille des mémoires cache embarquées sur les disques durs actuels ?
{{% /question %}}

### Interfaces avec l'ordinateur

Les interfaces internes (connexion à l'intérieur du boîtier de l'ordinateur) peuvent être :

* ATA, également nommée PATA ou IDE. N’existe plus sur les DD récents.

* SATA (*Serial ATA*). Standard actuel.

* SCSI (*Small Computer System Interface*). Surtout utilisée pour les serveurs d’entreprise.

Les interfaces externes (connexion à l'extérieur du boîtier) sont :

* USB : les disques durs externes proposés sur le marché sont compatibles avec la norme 3.0.

* eSATA : version externe de la technologie SATA utilisée pour les disques internes.

## Le disque SSD 

À la différence d’un disque dur utilisant le principe magnétique, un disque SSD (*Solid State Drive*) est constitué de **puces de mémoires flash,** qui sont des puces électroniques possédant les caractéristiques d’une mémoire vive, mais dont les données ne disparaissent pas lors d’une mise hors tension. Ils ne contiennent donc aucune pièce mécanique.

{{% image src="ssd.jpeg" class="centered" %}}

Les SSD présentent de nombreux avantages par rapport à un disque dur traditionnel :

* Insensibilité aux chocs.
* Temps d’accès plus rapide.
* Fonctionnement totalement silencieux.
* Débits importants et stables.
* probabilité de panne beaucoup plus faible, liée à l’absence de pièces mécaniques en mouvements.

Le principal inconvénient de ces disques est leur prix beaucoup plus élevé que celui d’un disque dur à capacité égale. Les capacités des SSD sont aussi inférieures aux disques durs avec une capacité maximale autour de 1 To.

{{% question %}}
Combien coûte un SSD de 500 Go ? Et un disque dur de même capacité ?
{{% /question %}}

Les SSD sont vraisemblablement appelés à remplacer les disques durs dans un proche avenir.

