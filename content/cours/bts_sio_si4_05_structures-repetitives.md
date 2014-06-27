---
title: "Structures répétitives"
slug: structures-repetitives
---

L'objectif de ce chapitre est d'apprendre comment ajouter à nos programmes des possibilités d'exécution répétitive.

Définition
==========

Une structure répétitive, également appelée structure itérative ou encore **boucle**, permet de répéter plusieurs fois l'exécution d'une ou plusieurs instructions. Le nombre de répétitions peut :

* être connu à l'avance.
* dépendre de l'évaluation d'une **condition**.

A chaque répétition, les instructions contenues dans la boucle sont exécutées. C'est ce qu'on appelle un tour de boucle ou encore une **itération**.

{{% img repetitives_bart.jpg %}}

Les structures répétitives sont très utilisées en programmation. Leur maîtrise est donc essentielle.

Il existe deux grands types de boucles, supportées par la grande majorité des langages de programmation. Nous allons les étudier successivement.

La boucle `while`
=================

Le programme d'exemple
----------------------

Prenons comme exemple un programme C# qui répète plusieurs fois des instructions.

    Console.WriteLine("Début du programme");
    int compteur = 0;
    while (compteur < 10)
    {
        compteur++;
        Console.WriteLine("Dans la boucle, tour numéro " + compteur);
    }
    Console.WriteLine("Vous avez effectué " + compteur + " tour(s) de boucle");

{{% img while_For.jpg %}}

Syntaxe et fonctionnement
-------------------------

La syntaxe de l'instruction `while` est la suivante.

    while (condition)
    {
        <instructions>
    }

Avant chaque tour de boucle, la condition associée au `while` est évaluée :

* si elle est vraie, les instructions du bloc `while` sont exécutées. Ensuite, la ligne du `while` est à nouveau exécutée et la condition vérifiée.
* si elle est fausse, les instructions du bloc ne sont pas exécutées et le programme continue juste après le bloc `while`.

{{% definition %}}
La boucle `while`, appelée également boucle TantQue, permet de répéter des instructions **tant qu'une condition est vérifiée**.
{{% /definition %}}

Nombre de tours de boucle
-------------------------

Il est important de définir précisement la condition associée à la boucle `while` afin d'effectuer le bon nombre de tours de boucle. Voici l'exemple précédent réécrit en initialisant la variable `compteur à 1 et non plus à 0.

    Console.WriteLine("Début du programme");
    int compteur = 1;
    while (compteur <= 10)  // <= au lieu de <
    {
        Console.WriteLine("Dans la boucle, tour numéro " + compteur);
        compteur++;  // Instruction déplacée après la précédente
    }
    Console.WriteLine("Vous avez effectué " + (compteur - 1) + " tour(s) de boucle");

Il produit exactement le même résultat d'exécution.

{{% remark %}}
Le bloc d'instructions associé au while est appelé **corps de la boucle**. Il doit être placé entre accolades, sauf s'il ne comporte qu'une seule instruction (TODO).
{{% /remark %}}

Il existe aussi des situations où la condition du `while` dépend d'une saisie demandée à l'utilisateur.

    string saisie;
    bool continuer = true;
    while (continuer)
    {
        Console.Write("Pour sortir de la boucle, tapez 0 : ");
        saisie = Console.ReadLine();
        if (saisie == "0")
            continuer = false;
    }

Dans ce cas, il est impossible de prévoir à l'avance le nombre de tours de boucles réalisés.

la boucle `for`
===============

Le programme d'exemple
----------------------

Voici notre programme d'exemple initial réécrit d'une autre manière.

    Console.WriteLine("Début du programme");
    int compteur;
    for (compteur = 0; compteur < 10; compteur++)
    {
        Console.WriteLine("Dans la boucle, tour numéro " + (compteur + 1));
    }
    Console.WriteLine("Vous avez effectué " + compteur + " tour(s) de boucle");

{{% img while_For.jpg %}}

Syntaxe et fonctionnement
-------------------------

La syntaxe de l'instruction `for` est la suivante.

    for (initialisation; condition; étape)
    {
        <instructions>
    }

Voici son fonctionnement :

* L'initialisation (`compteur = 0` dans l'exemple) se produit une seule fois, au début de l'exécution de la boucle.
* La condition (`compteur < 10` dans l'exemple) est évaluée **avant chaque tour de boucle**. Si elle est vraie, un nouveau tour de boucle est effectué. Sinon, la boucle est terminée.
* L'étape (`compteur++` dans l'exemple) est réalisée **après chaque tour de boucle**.

A la fin de l'exécution de l'exemple précédent, la variable `compteur possède donc la valeur *10*.

{{% definition %}}
La boucle `for`, appelée également boucle Pour, permet de répéter des instructions **tant qu'une condition est vérifiée**. Elle permet de définir une initialisation qui a lieu une seule fois et une étape qui a lieu après chaque tour de boucle.
{{% /definition %}}

{{% remark %}}
L'opérateur ``++`` est un raccourci : écrire ``variable++`` équivaut à écrire ``variable = variable + 1``, en plus concis. L'opérateur ``++`` est appelé opérateur de post-incrémentation.
{{% /remark %}}

{{% definition %}}
L'opération qui consiste à ajouter 1 à la valeur d'une variable entière se nomme **l'incrémentation**
([Wikipedia](http://fr.wikipedia.org/wiki/Incr%C3%A9mentation)).
{{% /definition %}}

{{% remark %}}
La variable utilisée dans l'initialisation, la condition et l'étape est appelée le *`compteur* de la boucle. Par convention, on la nomme souvent *i*.
{{% /remark %}}

Nombre de tours de boucle
-------------------------

Comme avec un `while`, l'initialisation et la condition d'une boucle `for` doivent être définies avec précision. Voici l'exemple précédent réécrit en initialisant la variable `compteur` à 1 et non plus à 0.

    Console.WriteLine("Début du programme");
    int compteur;
    for (compteur = 1; compteur <= 10; compteur++)
    {
        Console.WriteLine("Dans la boucle, tour numéro " + compteur);
    }
    Console.WriteLine("Vous avez effectué " + (compteur - 1) + " tour(s) de boucle");

Il produit exactement le même résultat d'exécution, mais la valeur finale de la variable `compteur` est 11 et non plus 10.

Portée du compteur de boucle
----------------------------

Lorsqu'on n'a pas besoin d'utiliser la variable compteur de boucle en dehors du corps de la boucle, on peut déclarer cette variable dans l'initialisation de la boucle `for` qui l'utilise.

    // ...
    for (int compteur = 0; compteur < 10; compteur++)
    {
        // ...
    }
    // Impossible d'utiliser la variable compteur après la boucle

Dans ce cas, sa **portée** se limite au corps de la boucle, entre les accolades.

{{% definition %}}
La **portée** d'une variable est l'ensemble des endroits d'un programme où cette variable est utilisable.
{{% /definition %}}

Choix entre un `while` et un `for`
=================================

Certains contextes sont plus adaptés à l'utilisation d'une boucle `while`, d'autre à celui d'un `for`.

Ces deux structures permettent de répéter plusieurs fois un ensemble d'instructions. La différence essentielle est que le nombre d'itérations d'un `for` est fixé au début de l'exécution de la boucle.

* si on peut prévoir à l'avance le nombre de tours de boucle, le `for` est préférable.
* sinon, il faut utiliser un `while`.

Erreurs à éviter
================

Boucle `while` infinie
----------------------

Le principal risque lié à la boucle `while` est la **boucle infinie**. Il s'agit d'une erreur de programmation très facile à commettre, donc dangereuse.

    Console.WriteLine("Le manège démarre !");
    int tour = 1;
    while (tour <= 10)  // Toujours vraie => boucle infinie
    {
        Console.WriteLine("C'est le tour numéro " + tour);
    }
    Console.WriteLine("Le manège s'arrête");

A l'exécution, on ne sortira jamais du corps de la boucle puisque la variable `tour` vaudra toujours 1.

Pour corriger ce problème, il faut ajouter l'instruction `tour++` dans le corps de la boucle.

    Console.WriteLine("Le manège démarre !");
    int tour = 1;
    while (tour <= 10)  // Deviendra fausse quand tour > 10
    {
        Console.WriteLine("C'est le tour numéro " + tour);
        tour++;
    }
    Console.WriteLine("Le manège s'arrête");

{{% definition %}}
Une boucle infinie est une boucle mal écrite, dont la condition reste toujours vraie.
{{% /definition %}}

Pour éviter de créer une boucle infinie, il faut :

* écrire une condition de boucle correcte.
* initialiser correctement la ou les variables impliquées dans la  condition de la boucle.
* vérifier que ces variables sont modifiées dans le corps de la boucle pour rendre la condition fausse le moment venu.

Manipulation du compteur d'une boucle `for`
-------------------------------------------

Imaginons qu'on ait l'idée (bizarre) de manipuler le compteur d'une boucle `for` dans le corps de la boucle.

    Console.WriteLine("Début du programme");
    for (int i = 1; i <= 10; i++)
    {
         Console.WriteLine("Dans la boucle, tour numéro " + i);
         i = i + 1;  // Danger !
    }

A chaque tour de boucle, le compteur est incrémenté deux fois : une fois dans le corps de la boucle puis une seconde fois dans l'étape.

{{% danger %}}
Quand on emploie une boucle `for`, l'incrémentation du compteur de boucle est automatique après chaque tour de boucle. Sauf exception rarissime, Il ne faut donc surtout pas modifier cette variable à l'intérieur de la boucle.
{{% /danger %}}

