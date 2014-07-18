---
title: "Passage de paramètres"
url: /cours/passage-parametres
---

L'objectif de ce chapitre est d'apprendre à échanger des données avec un sous-programme.

Introduction
============

Intérêt du passage de paramètres
--------------------------------

Supposons qu'on souhaite écrire un programme qui dise bonjour à son utilisateur dans différentes langues. Une première solution consiste à écrire un sous-programme par langue.

    static void Main(string[] args)
    {
        DireBonjour();
        SayHello();
        DecirHola();
    }

    static void DireBonjour()
    {
        Console.WriteLine("Bonjour !");
    }

    static void SayHello()
    {
        Console.WriteLine("Hello !");
    }

    static void DecirHola()
    {
        Console.WriteLine("Hola !");
    }

Cette solution n'est pas très satisfaisante : même s'il se limite ici à une ligne, le code d'affichage est dupliqué dans tous les sous-programmes. Il serait préférable de **centraliser** cette opération dans un seul sous-programme, en faisant changer uniquement le message affiché.

Jusqu'à présent, la seule solution que nous connaissons pour échanger des données entre le programme principal et le sous-programme repose sur l'utilisation de variables globales.

    static string messageBonjour;

    static void Main(string[] args)
    {
         messageBonjour = "Bonjour !";
         DireBonjour();
         messageBonjour = "Hello !";
         DireBonjour();
         messageBonjour = "Hola !";
         DireBonjour();
    }

    static void DireBonjour()
    {
         Console.WriteLine(messageBonjour);
    }

Le code d'affichage est centralisé, ce qui est un progrès par rapport à la solution précédente. Cependant, le sous-programme `DireBonjour` ne peut plus fonctionner si une variable globale nommée `messageBonjour` n'est pas déclarée et affectée à la bonne valeur avant chaque appel. Cela limite la **modularité** du code et la réutilisation du sous-programme dans un autre contexte.

On aimerait pouvoir écrire un sous-programme qui puisse échanger des informations avec le programme appelant tout en restant indépendant. Une solution existe : le passage de paramètres.

Un premier exemple
------------------

Voici une adaptation du contexte précédent.

    static void Main(string[] args)
    {
        string messageBonjour = "Bonjour !";
        DireBonjour(messageBonjour);

        messageBonjour = "Hello !";
        DireBonjour(messageBonjour);

        messageBonjour = "Hola !";
        DireBonjour(messageBonjour);
    }

    static void DireBonjour(string message)  // message est un paramètre de DireBonjour
    {
        Console.WriteLine(message);
    }

{{% img passage_parametre.jpg %}}

La définition du sous-programme comporte de nouveaux éléments. Elle inclut à présent un **paramètre** nommé `message` dont le type est `string`. A l'intérieur du sous-programme, `message` est utilisée comme une variable locale classique. Mais `message` n'est déclarée nulle part. Il s'agit d'une variable fictive appelée parfois variable formelle ou encore paramètre formel.

{{% definition %}}
On appelle **paramètre** une donnée attendue par un
sous-programme qui doit lui être fournie lors de chaque appel. La liste
des paramètres d'un sous-programme est définie entre parenthèses après
le nom du sous-programme.
{{% /definition %}}

Au moment de l'appel du sous-programme `DireBonjour`, le paramètre `message` prend la valeur de la variable utilisée dans l'appel, c'est-à-dire `messageBonjour`. Puisque la variable `messageBonjour` est celle dont la valeur est concrètement utilisée, elle est appelée paramètre effectif du sous-programme ou encore **argument**.

{{% definition %}}
On appelle **argument** la valeur fournie pour un paramètre au moment d'un appel du sous-programme.
{{% /definition %}}

A présent, le sous-programme `DireBonjour` n'est plus lié au programme appelant. On pourrait très bien le recopier tel quel dans un autre programme.

Fonctionnement du passage de paramètres
---------------------------------------

L'ajout de **paramètres** à un sous-programme permet d'échanger des données avec le programme appelant, tout en maintenant le sous-programme indépendant (ce qui n'est plus le cas quand le sous-programme utilise des variables globales).

Au moment de l'appel au sous-programme, la valeur des données utilisés pour l'appel, appelées **arguments** (paramètres effectifs), est affectée aux **paramètres** (formels) du sous-programme. A l'intérieur d'un sous-programme, un paramètre se comporte comme une variable locale.

{{% remark %}}
Les paramètres et les arguments peuvent avoir des **noms** différents mais doivent partager le même **type**.
{{% /remark %}}

Possibilités d'utilisation
--------------------------

Un sous-programme peut comporter les mêmes éléments qu'un programme classique : tests, boucles, etc. Il peut être appelé plusieurs fois depuis le programme principal. A chaque appel, les paramètres prennent la valeur des arguments pendant l'exécution du sous-programme. Voici un nouvel exemple.

    static void Main(string[] args)
    {
         int nb1 = 6;
         int nb2 = 4;
         AfficherMax(nb1, nb2);   // 1er appel
         AfficherMax(2, 9);       // 2ème appel
         AfficherMax(nb1, nb1);   // 3ème appel
    }

    static void AfficherMax(int x, int y)
    {
        if (x > y)
        {
            Console.WriteLine(x + " est plus grand que " + y);
        }
        else
        {
            if (x < y)
                Console.WriteLine(x + " est plus petit que " + y);
            else
                Console.WriteLine(x + " et " + y + " sont égaux");
        }
    }

{{% img afficher_max.jpg %}}

Le tableau ci-dessous rassemble les informations sur les différents appels du sous-programme.

Appel | Valeur de x | Valeur de y | Message affiché
------|-------------|-------------|----------------
1er appel | 6 | 4 | 6 est plus grand que 4 |
2ème appel | 2 | 9 | 2 est plus petit que 9 |
3ème appel | 6 | 6 | 6 et 6 sont égaux |

Aspects avancés
===============

Mode de passage des paramètres
------------------------------

L'exemple suivant va nous permettre de découvrir un aspect délicat du passage de paramètres.

    static void Main(string[] args)
    {
        int x = 6;
        AugmenterDeUn(x);
        Console.WriteLine("Programme principal : x vaut " + x);
    }

    static void AugmenterDeUn(int y)
    {
        y = y + 1;
        Console.WriteLine("Sous-programme : y vaut " + y);
    }

{{% img augmenter_de_un.jpg %}}

Pour comprendre ce résultat, il faut savoir que lorsqu'une variable est passée en paramètre à un sous-programme, la valeur de l'argument est **copiée** dans un nouvel emplacement mémoire correspondant au paramètre. La même valeur (ici *6*) est donc stockée à *deux* emplacements mémoire différents, celui de l'argument *x* et celui du paramètre *y*. Toute modification du paramètre dans le sous-programme n'a aucun impact sur la valeur de l'argument dans le programme principal.

On appelle **passage par valeur** ce mode de passage des paramètres. C'est le mode par défaut en C#, ainsi qu'en Java.

Nommage des paramètres
----------------------

L'exemple ci-dessous va illustrer une subtilité liée au nommage des paramètres d'un sous-programme.

    static void Main(string[] args)
    {
        int x = 6;
        AugmenterD Un(x);
        Console.WriteLine("Programme principal : x vaut " + x);
    }

    static void AugmenterDeUn(int x)
    {
        x = x + 1;
        Console.WriteLine("Sous-programme : x vaut " + x);
    }
}

Il s'agit du même exemple que précédemment, à une différence près : le paramètre du sous-programme a été renommé et porte le même nom que l'argument du programme principal.

Ce programme est compilable sans erreur et son exécution donne le résultat ci-dessous.

{{% img nommage_parametre.jpg %}}

Ce résultat s'explique exactement de la même manière que le précédent : au moment de l'appel, la valeur de l'argument est copiée dans la zone mémoire du paramètre. La modification au niveau du sous-programme n'a donc pas d'effet sur la variable du programme principal. La seule différence concerne ici le programmeur, et non la machine : paramètre et argument portent le même nom *x*, ce qui ne provoque pas d'erreur mais affecte la lisibilité du code, surtout pour un programmeur débutant.

{{% tip %}}
En phase d'apprentissage, il est conseillé de donner aux arguments des noms différents de ceux des paramètres.
{{% /tip %}}

