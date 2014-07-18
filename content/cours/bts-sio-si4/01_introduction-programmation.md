---
title: Introduction à la programmation
url: /cours/introduction-programmation
---

L'objectif de ce chapitre est de découvrir les notions fondamentales
liées à la programmation.

{{% img evolution.jpg %}}

# Un programme, c'est quoi ?

## Le rôle d'un programme

Depuis son invention dans les années 1950, l'informatique a révolutionné bien des domaines de notre vie quotidienne. Le calcul d'un itinéraire depuis un site Internet ou un GPS, la réservation à distance d'un billet de train ou d'avion, ou encore la possibilité de voir et de parler avec des amis à l'autre bout du monde : tous ces actes courants sont possibles grâce aux **ordinateurs**.

{{% remark %}}
Le terme **ordinateur** est ici à prendre dans son sens le plus général, celui d'une "machine électronique capable d'exécuter des opérations arithmétiques et logiques" ([Wikipedia](http://fr.wikipedia.org/wiki/Ordinateur)). Il peut désigner aussi bien un ordinateur de bureau classique (PC, Mac) qu'un serveur de calcul ou encore un terminal mobile (tablette, *smartphone*).
{{% /remark %}}

Cependant un ordinateur, même très performant, n'est qu'une **machine** capable d'exécuter automatiquement une série d'opérations simples qu'on lui a demandées. Il ne dispose par lui-même d'aucune capacité d'apprentissage, de jugement, d'improvisation, bref d'aucune "intelligence". Il se contente de **faire ce qu'on lui dit de faire**. L'intérêt des ordinateurs est de savoir manipuler très rapidement et sans erreur d'énormes quantités d'informations.

Une intervention humaine est nécessaire pour qu'un ordinateur puisse accomplir des tâches utiles. C'est le rôle du **programmeur** (appelé également **développeur**). Il va fournir les ordres que la machine doit exécuter en écrivant des programmes. De manière générale, un programme sert à **automatiser un traitement sur des données**. Son résultat dépend des données qui lui sont fournies. On peut schématiser un programme de manière suivante : **E-T-R** (Entrées–Traitements-Résultats). L'objectif du programmeur est donc d'écrire un programme qui, une fois exécuté par l'ordinateur, donnera les résultats attendus en fonction des données d'entrée.

{{% definition %}}
Un **programme informatique** est une liste d'ordres indiquant à un ordinateur ce qu'il doit faire ([Wikipedia](http://fr.wikipedia.org/wiki/Programme_informatique)).
{{% /definition %}}

## Création d'un programme

Pour créer des programmes informatiques, le programmeur utilise un **langage de programmation**. Il en existe un grand nombre, par exemple C++, C\#, Java, Python ou encore PHP. Un programme informatique se présente concrètement sous la forme d'un (ou le plus souvent plusieurs) fichiers texte, contenant des commandes spécifiques au langage : ce sont les ordres données à la machine, qu'on appelle également **instructions**. L'ensemble des fichiers représente le **code source** du programme. Chaque langage de programmation dispose de sa propre syntaxe et d'instructions spécifiques.

Voici un exemple de programme très simple écrit en utilisant le langage
Python.

    print("Bonjour le monde.")

On peut écrire le même programme en utilisant le langage PHP.

    <?php
    echo("Bonjour le monde.");
    ?>

Même exemple avec le langage C#.

    class Program {
        static void Main(string[] args) {
            Console.WriteLine("Bonjour le monde.");
        }
    }

Et voici le même programme, écrit cette fois en langage Java.

    public class Program {
        public static void main(String[] args) {
            System.out.println("Bonjour le monde.");
        }
    }

Tout éditeur de texte peut a priori permettre d'écrire des programmes. Pour gagner du temps lors de l'écriture du code source, les langages disposent de plate-formes d'édition très abouties appelées IDE (*Integrated Development Environment*), comme par exemple Visual Studio ou Eclipse.

## Exécution d'un programme

Le seul langage directement compréhensible par un ordinateur est le langage machine (ou **assembleur**). Il s'agit d'instructions élémentaires liées à un type de processeur et qui permettent de manipuler directement la mémoire de la machine.

Voici le programme précédent, réécrit en assembleur ([Wikipedia](http://fr.wikipedia.org/wiki/Assembleur#Afficher_Bonjour)).

    str:
     .ascii "Bonjour le monde.\n"
     .global _start
    
    _start:
    movl $4, %eax
    movl $1, %ebx
    movl $str, %ecx
    movl $19, %edx
    int $0x80
    movl $1, %eax
    movl $0, %ebx
    int $0x80

L'écriture de programmes en langage machine offre une rapidité maximale mais représente une tâche très complexe. Toute erreur peut se traduire par la corruption d'une zone mémoire, avec des conséquences parfois graves. Il s'agit donc d'un langage à réserver à des usages très spécifiques (écriture de pilotes pour un matériel, etc).

Tout programme écrit dans un autre langage devra être **traduit** en langage machine pour être exécuté par le processeur. Ce processus de traduction peut se faire de trois manières différentes et dépend du langage choisi.

Par exemple, le programme Python précédent s'exécute en lançant la commande ci-dessous (on suppose que le fichier `bonjour.py` contient les instructions du code source) :

    $ python bonjour.py

Lors de l'appel de la commande ci-dessus, les instructions Python contenues dans ce fichier sont traduites en langage machine. Chaque ligne est exécutée au fur et à mesure de sa lecture : on dit que Python est un langage
[interprété](http://fr.wikipedia.org/wiki/Interpr%C3%A8te_(informatique)#Principe).

Une autre possibilité consiste à créer à partir du code source un fichier directement exécutable (extension **.exe** sous Windows), en utilisant un programme intermédiaire appelé [compilateur](http://fr.wikipedia.org/wiki/Compilateur). Exemples de langages utilisant un compilateur : C, C++.

Une troisième option consiste à utiliser un **pseudo-compilateur** pour générer à partir du code source un ensemble de fichiers pouvant être exécutés sur n'importe quelle plate-forme supportant l'environnement. C'est le cas du langage Java et des langages de la plate-forme Microsoft .NET (VB.NET, C\#).

# Apprendre à écrire des programmes

## La démarche

Sauf dans des cas très simples, on ne crée pas un programme en se lançant directement dans l'écriture du code source. En se précipitant sur sa machine, on court plusieurs risques :

* ne pas traiter le problème dans son intégralité, en se concentrant sur une seule partie.
* se laisser guider par les contraintes du langage utilisé.
* aboutir à un programme fonctionnel mais peu lisible, peu performant et comportant beaucoup d'erreurs (**bogues**). Dans ce cas, le temps gagné initialement sera perdu plusieurs fois à corriger ses défauts.

Il est donc d'abord nécessaire d'analyser le problème pour trouver la suite d'opérations à réaliser pour le résoudre. Cette analyse a pour objectif de décomposer le problème en plusieurs sous-problèmes plus simples.

Prenons un exemple concret tiré de la vie courante (source : A. Tarlowski) : je souhaite me préparer un plat de pâtes. Quelles sont les étapes qui vont me permettre d'atteindre mon objectif ? On peut imaginer la solution ci-dessous.

**Début**

1.  Sortir une casserole
2.  Mettre de l'eau dans la casserole
3.  Ajouter du sel
4.  Mettre la casserole sur le feu
5.  Tant que l'eau ne bout pas : attendre
6.  Sortir les pâtes du placard
7.  Verser les pâtes dans la casserole
8.  Tant que les pâtes ne sont pas cuites : attendre
9.  Verser les pâtes dans une passoire
10. Egoutter les pâtes
11. Verser les pâtes dans un plat
12. Si les pâtes sont trop fades : ajouter du sel

**Fin**

{{% img recette.jpg %}}

On constate qu'on arrive à l'objectif visé en déroulant un ensemble d'actions dans un ordre précis. On peut distinguer différents types d'actions : les **actions simples** (`Sortir une casserole`), des **actions conditionnelles** (`Si`) et des **actions répétitives** (`Tant que`). Nous avons employé une notation simple, compréhensible et indépendante de tout langage de programmation. En fait, nous venons d'écrire ce qu'on appelle un **algorithme**.

{{% definition %}}
Un **algorithme** est une une suite ordonnée d'opérations permettant de résoudre un problème donné ([Wikipedia](http://fr.wikipedia.org/wiki/Algorithme)).
{{% /definition %}}

## L'algorithmique

L'avantage de la représentation d'un problème sous forme d'un algorithme est que cette représentation est compréhensible par un être humain et indépendante d'un quelconque langage. En revanche, elle ne permet pas
d'employer les particularités de tel ou tel langage.

Un algorithme n'est pas directement exécutable par un ordinateur. Pour cela, il faut le traduire dans le langage de programmation choisi. C'est ce qu'on appelle la phase de **codage** ou **d'implémentation**.
Cependant, on peut très bien simuler l'exécution d'un algorithme par une sorte de "pseudo-machine" sachant exécuter ses opérations.

Résoudre un problème sous la forme d'un algorithme permet de se détacher des particularités d'un langage informatique pour aboutir à une solution générale, qui pourra très bien être ensuite exprimée dans un (ou
plusieurs) langages. **Apprendre à (bien) écrire des algorithmes est le moyen le plus efficace pour apprendre à (bien) programmer**, quel que soit le langage utilisé.

Plus le problème à résoudre est complexe, plus la phase de recherche d'un l'algorithme adapté prend d'importance (et de temps !).

