---
title: "Tableaux et listes"
url: /cours/tableaux-listes
---

L'objectif de ce chapitre est de présenter deux manières de regrouper des données en mémoire : les tableaux et les listes (appelées parfois collections).

Introduction
============

Jusqu'à présent, nos programmes ont utilisé uniquement des variables stockant une seule valeur, appelées parfois des variables *scalaires* ([Wikipedia](http://fr.wikipedia.org/wiki/Scalaire#Informatique)).

On souhaite écrire un programme qui fait saisir 5 valeurs à l'utilisateur, puis calcule et affiche leur somme. Une solution pourrait être la suivante.

    Console.Write("Entrez le nombre 1 : ");
    int nb1 = Convert.ToInt32(Console.ReadLine());
    Console.Write("Entrez le nombre 2 : ");
    int nb2 = Convert.ToInt32(Console.ReadLine());
    Console.Write("Entrez le nombre 3 : ");
    int nb3 = Convert.ToInt32(Console.ReadLine());
    Console.Write("Entrez le nombre 4 : ");
    int nb4 = Convert.ToInt32(Console.ReadLine());
    Console.Write("Entrez le nombre 5 : ");
    int nb5 = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Le nombre 1 est " + nb1);
    Console.WriteLine("Le nombre 2 est " + nb2);
    Console.WriteLine("Le nombre 3 est " + nb3);
    Console.WriteLine("Le nombre 4 est " + nb4);
    Console.WriteLine("Le nombre 5 est " + nb5);

    int somme = nb1 + nb2 + nb3 + nb4 + nb5;
    Console.WriteLine("Leur somme vaut " + somme);

Dans cet exemple, il est nécessaire de créer une variable par nombre saisi. Mais comment faire si on veut gérer non pas 5, mais 50 ou même 500 nombres ? Déclarer et saisir autant de nombres ferait exploser la taille de notre programme, avec des traitements (saisie, affichage, calcul) très répétitifs. On doit pouvoir faire mieux.

Les tableaux
============

Définition
----------

{{% definition %}}
Un **tableau** regroupe un ensemble d'éléments de même nature. Une variable de type "tableau" permet de stocker plusieurs éléments partageant le même **type**.
{{% /definition %}}

On pourra donc utiliser des tableaux d'entiers, des tableaux de chaînes, voire même des tableaux de tableaux...

On peut représenter graphiquement un tableau sous la forme d'un ensemble de cases. Chaque case permet de stocker une valeur spécifique. Cette représentation peut être horizontale ou verticale.

-   Exemple de représentation horizontale (*tableau 1*).

| **Indice** | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
-------------|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
| *`valeur`* | 2 | 3 | 5 | 7 | 11 | 13 | 17 | 19 | 23 | 29 | 31 | 37 | 41 | 43 | 47 | 53 | 59 | 61 | 67 | 71 

-   Exemple de représentation verticale (*tableau 2*).

Indice | Valeur |
-------|---------
| 0 | Annie ZETTE |
| 1 | Léon DIT |
| 2 | Ali GATOR | 
| 3 | Sam GRATE |
| 4 | Pierre KIROUL |

Le numéro d'une case d'un tableau est appelée son **indice**. Pour accéder à un élément du tableau, il faut donc connaître son indice.

{{% warning %}}
En C# et dans la plupart des autres langages, les tableaux sont indicés à partir de 0 et non de 1.
{{% /warning %}}

Caractéristiques
----------------

Un tableau se caractérise par :

* le type des éléments qu'il stocke.
* le nombre des éléments qu'il stocke, appelé sa **taille**.

| Tableau | Type des éléments stockés | Taille |
----------|---------------------------|---------
| Tableau 1 | Entier | 20 | 
| Tableau 2 | Chaîne | 5 |

{{% remark %}}
* En C#, tous les éléments d'un tableau doivent avoir le même type. On ne peut pas mélanger des entiers, des réels ou des chaînes dans un même tableau.
* La taille d'un tableau est fixe, même si certains langages de programmation permettent de la modifier dynamiquement (pendant l'exécution du programme).
{{% /remark %}}


Exemple d'utilisation
---------------------

Voici notre exemple de début de chapitre, réécrit en utilisant un tableau.

    int[] nombres;
    nombres = new int[5];

    for (int i = 0; i < nombres.Length; i++)
    {
        Console.Write("Entrez le nombre " + (i + 1) + " : ");
        int nombreSaisi = Convert.ToInt32(Console.ReadLine());
        nombres[i] = nombreSaisi;
    }

    int somme = 0;
    for (int i = 0; i < nombres.Length; i++)
    {
        Console.WriteLine("Le nombre " + (i + 1) + " est " + nombres[i]);
        somme = somme + nombres[i];
    }
    Console.WriteLine("Leur somme vaut " + somme);

{{% img tableau.jpg %}}

Nous allons détailler tous les éléments nouveaux de ce programme.

Déclaration d'un tableau
------------------------

On manipule un tableau grâce à une variable de type spécifique.

    int[] nombres;
    // ...

Les **crochets** indiquent que la variable déclarée est un tableau.

Quand on déclare un tableau, on doit préciser :

* le **nom** de la variable associée (ici `nombres`).
* le **type** des éléments du tableau (ici `int`).

La syntaxe de définition d'un tableau en C# est donc la suivante.

    typeElement[] nomTableau;

Allocation mémoire
------------------

Comme pour un objet, la simple déclaration d'un tableau de provoque pas de réservation mémoire pour stocker ses valeurs. Pour cela, il est nécessaire d'allouer la mémoire nécessaite en utilisant l'opérateur `new`.

    // ...
    nombres = new int[5];
    // ...

On précise entre crochets le nombre d'éléments du tableau, autrement dit sa **taille**.

Lors de l'exécution de cette ligne, une zone mémoire nécessaire au stockage de tous les éléments est réservée. Les valeurs initialement stockées dans le tableau sont inconnues.

Accès à un élément d'un tableau
-------------------------------

Les éléments d'un tableau sont stockés dans des "cases" identifiées par leur **indice**. Pour accéder à un élément, on doit donc utiliser cet indice.

    double[] valeurs = new double[4];
    valeurs[0] = 12.5;
    valeurs[1] = 10;
    valeurs[2] = 17.5;
    valeurs[3] = 13;
    double total = valeurs[0] + valeurs[1] + valeurs[2] + valeurs[3];
    Console.WriteLine(total);

En fin d'exécution, la variable `total` aura la valeur 53 et le contenu du tableau valeurs sera le suivant.

| **Indice** | 0 | 1 | 2 | 3 |
-------------|---|---|---|---|
| *`valeur`* | 12,5 | 10 | 17,5 | 13 | 

Parcours d'un tableau
---------------------

Lorsqu'on veut effectuer un traitement répétitif sur un tableau, on utilise souvent une **boucle** (TODO).

Reprenons notre exemple précédent. Additionner tous les éléments d'un tableau revient à :

1.  Initialiser une variable nommée `total` à zéro.
2.  Parcourir le tableau avec une boucle et ajouter chaque élément à la variable `total`.
3.  Une fois le tableau parcouru, `total` contiendra la somme de ses éléments, comme attendu.

Voici la traduction en C# de cet algorithme.

    double[] valeurs = new double[4];
    valeurs[0] = 12.5;
    valeurs[1] = 10;
    valeurs[2] = 17.5;
    valeurs[3] = 13;
    double total = 0;
    for (int i = 0; i < valeurs.Length; i++)
    {
        total = total + valeurs[i];
    }
    Console.WriteLine(total);

Le nombre d'éléments d'un tableau étant connu à l'avance, le choix d'une boucle `for` plutôt qu'une boucle `while` est souvent judicieux.

On constate que l'instruction C# `valeurs.Length` permet de renvoyer la taille du tableau `valeurs`.

Le compteur de boucle `i` prend successivement les valeurs 0, 1, 2, 3, ce qui correspond aux différents indices du tableau `valeurs`. Le compteur va de 0 jusqu'à *taille du tableau - 1*.

A titre d'exercice, on peut réécrire ce programme en utilisant une boucle `while`.

    // ...
    double total = 0;
    int i = 0;
    while (i < valeurs.Length)
    {
        total = total + valeurs[i];
        i++;
    }
    Console.WriteLine(total);

Les listes
==========

Limites des tableaux
--------------------

L'utilisation d'un tableau permet de stocker un ensemble de plusieurs éléments de même nature. Cependant, les tableaux souffrent de plusieurs limitations :

* leur taille est fixée au moment de l'allocation mémoire.
* toutes les opérations courantes (tri, recherche d'un élément, etc) doivent être écrites manuellement par le programmeur.

Le dépassement de capacité d'un tableau est une erreur de programmation classique.

{{% img depassement_capacite_tableau.jpg %}}

Dans l'exemple ci-dessus, on tente de définir la valeur du 5ème élément d'un tableau de 4 éléments, ce qui provoque une erreur à l'exécution.

Pour pallier à ces inconvénients, un autre type de donnée tend à les supplanter : les **listes** (appelées parfois *collections*).

Définition
----------

{{% definition %}}
Comme un tableau, une **liste** regroupe un ensemble d'éléments de même nature. Une variable de type "liste" permet de stocker plusieurs éléments partageant le même **type**.
{{% /definition %}}

Cependant, une liste offre plus de fonctionnalités qu'un tableau. En particulier, sa taille (nombre d'éléments stockables) n'est pas fixe. Si besoin, une liste se redimensionne automatiquement lors de l'ajout d'un nouvel élément.

Une liste est un **objet** et dispose de plusieurs **propriétés** et **méthodes** pour gérer les éléments qu'elle contient.

Exemple d'utilisation
---------------------

Voici l'un des exemples précédents, réécrit en utilisant une liste.

    List<double> valeurs;          // déclaration
    valeurs = new List<double>();  // instanciation

    valeurs.Add(12.5);
    valeurs.Add(10);
    valeurs.Add(17.5);
    valeurs.Add(13);

    double total = 0;
    for (int i = 0; i < valeurs.Count; i++)
    {
        total = total + valeurs[i];
    }
    Console.WriteLine(total);

Déclaration d'une liste
-----------------------

En C#, on manipule une liste grâce à une variable de type `List`.

    List<double> valeurs; 
    // ...

En observant la déclaration ci-dessus, on voit que le type des éléments stockés dans la liste (ici `double`) est défini entre `<>`. La variable `valeurs` est donc une liste de réels.

Le type `List` est une classe et la variable `valeurs` est un objet. A ce titre, sa déclaration ne provoque aucune réservation mémoire. Pour cela, il faut instancier cet objet.

Instanciation d'une liste
-------------------------

Comme pour tout objet, l'instanciation d'une liste se fait grâce à l'opérateur `new`.

    // ...
    valeurs = new List<double>();
    // ...

C'est cette opération qui déclenche la réservation d'une zone mémoire pour stocker les éléments de la liste. La taille initiale de la liste est fixée par le système. Elle n'a pas d'importance réelle, puisqu'une liste peut se redimensionner automatiquement.

Ajout d'éléments à une liste
----------------------------

    // ...
    valeurs.Add(12.5);
    valeurs.Add(10);
    valeurs.Add(17.5);
    valeurs.Add(13);
    // ...

On utilise une méthode nommée `Add` pour ajouter un élément à un objet liste. Elle prend en paramètre une valeur dont le type doit être compatible avec le type des éléments de la liste.

Accès à un élément d'une liste
------------------------------

L'accès à un élément d'une liste peut se faire de plusieurs manières. Il est possible d'utiliser la même syntaxe que pour un tableau.

    // ...
    double total = valeurs[0] + valeurs[1] + valeurs[2] + valeurs[3];
    // ...

Les éléments d'une liste sont stockés dans l'ordre de leur ajout :

* `valeurs[0]` représente le premier élément de la liste
* `valeurs[1]` représente le deuxième élément de la liste
* ...

Comme un tableau, une liste est indicée à partir de zéro. Attention à ne pas aller au-delà de la taille de la liste, comme dans l'exemple ci-dessous.

{{% img depassement_capacite_liste.jpg %}}

Itération sur une liste
-----------------------

Il existe deux solutions pour parcourir une liste élément après élément (on parle de parcours *séquentiel*). La première consiste à utiliser la même syntaxe que pour un tableau, avec une boucle `for`.

    List<double> valeurs = new List<double>();
    // ...
    double total = 0;
    for (int i = 0; i < valeurs.Count; i++)
    {
        total = total + valeurs[i];
    }
    Console.WriteLine(total);

On constate que l'instruction `valeurs.Count` permet de renvoyer la taille (nombre d'éléments) de la liste `valeurs`. `Count` est une propriété C# de la classe `List`.

Le compteur de boucle `i` prend successivement les valeurs 0, 1, 2, 3. Le compteur va de 0 jusqu'à *taille de la liste - 1*.

Le seconde possiblité de parcours d'une liste utilise un nouveau type de boucle, la boucle `foreach` ("pour chaque").

    List<double> valeurs = new List<double>();
    // ...
    foreach (double valeur in valeurs)
    {
        total = total + valeur;
    }
    Console.WriteLine(total);

La boucle `foreach` parcourt la liste `valeurs` élément après élément. A chaque tour de boucle, l'élément courant de la liste `valeurs` est affecté à la variable locale `valeur`, qui peut être utilisée dans le corps de la boucle.

{{% definition %}}
La boucle `foreach` permet de parcourir une liste élément par élément.
{{% /definition %}}

{{% tip %}}
La distinction singulier/pluriel est importante : `valeurs` désigne la liste (type : `List<double>`) et `valeur` désigne son élément courant (type : `double`).
{{% /tip %}}

La syntaxe de l'instruction `foreach` est la suivante.

    foreach (typeElement unElement in listeElements)
    {
        <instructions utilisant unElement>
    }

Liste d'objets
--------------

Les listes sont souvent utilisées pour stocker des objets, instances de classes. Reprenons la classe `CompteBancaire` étudiée au chapitre précédent.

{{% image src="uml_compte_bancaire_2.jpg" class="centered" %}}

On déclare une liste d'objets de la même manière que pour n'importe quel autre type. Son utilisation est également similaire.

Pour des raisons de commodité, on utilise souvent la boucle `foreach` pour itérer sur les éléments d'uns liste d'objets. L'exemple ci-dessous illustre l'utilisation d'une collection de comptes bancaires.

    CompteBancaire comptePierre = new CompteBancaire("Pierre", 300, "euros");
    CompteBancaire comptePaul = new CompteBancaire("Paul", 200, "dollars");
    CompteBancaire compteJacques = new CompteBancaire("Jacques", 50, "euros");

    List<CompteBancaire> listeComptes = new List<CompteBancaire>();
    listeComptes.Add(comptePierre);
    listeComptes.Add(comptePaul);
    listeComptes.Add(compteJacques);

    foreach (CompteBancaire compte in listeComptes)
    {
        Console.WriteLine(compte.Decrire());
    }

{{% img liste_comptes.jpg %}}

{{% tip %}}
Ici aussi, la distinction singulier/pluriel est importante : `compte` désigne l'élément courant de la liste `listeComptes`.
{{% /tip %}}


