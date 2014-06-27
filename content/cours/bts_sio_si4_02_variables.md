---
title: "Les variables"
slug: variables
---

L'objectif de ce chapitre est de comprendre le rôle joué par les variables dans un programme.

# Le programme d'exemple

Nous allons débuter notre apprentissage de la programmation en étudiant un exemple très simple : un programme C# qui permet de calculer un prix TTC à partir d'un prix hors taxes (toujours le même). Voici son code source.

    // Définition du montant hors taxes
    double montantHT = 100;
    
    // Définition du taux de TVA à 20,6%
    double tauxTVA = 0.206;
    
    // Calcul du montant de la TVA
    double montantTVA = montantHT * tauxTVA;
    
    // Calcul du montant T.T.C.
    double montantTTC = montantHT + montantTVA;

On observe que ce code source se compose d'un certain nombre de **lignes de code** qui se terminent toutes par le caractère `;` : c'est une obligation en C#. Certaines lignes commencent par les caractères `//` : ce sont des **commentaires**, qui ne seront pas exécutées et permettent de documenter le code source.

Tentons maintenant de comprendre le fonctionnement de ce programme.

# La notion de variable

Pour effectuer son travail, notre programme a besoin de mémoriser des informations, par exemple le montant hors taxes ou encore le taux de TVA en vigueur. Pour cela, il utilise des **variables**.

{{% definition %}}
Une **variable** est une zone de stockage d'informations, une sorte de "boîte" servant à ranger des choses.
{{% /definition %}}

Un programme emploie des variables afin de pouvoir mémoriser des informations qu'il utilisera plus tard. Au niveau de l'ordinateur, déclarer une variable déclenche la réservation d'une zone de la mémoire attribuée à cette variable. Le programme (ou l'algorithme) pourra ensuite lire ou écrire des données dans cette zone mémoire en manipulant la variable.

## Déclaration d'une variable

Avant de pouvoir utiliser une variable pour stocker une information, le programme doit au préalable la créer. Cette opération s'appelle la **déclaration** de la variable.

    double tauxTVA;

En C#, la déclaration d'une variable s'effectue en choisissant :

* son **nom**, qui permet de la repérer et de l'utiliser. Ici, la variable se nomme `tauxTVA`.
* son **type**, qui permet de définir quelles données la variable peut contenir. Ici, le type donné à la variable est `double`, qui correspond à un nombre réel.
* éventuellement sa **valeur**, qui correspond à l'information stockée dans la variable.

Lorsque le programme est exécuté, la déclaration d'une variable se traduit par la réservation d'une petite partie de la mémoire de la machine. Cette zone sera dédiée au stockage de la valeur de la variable.

## Affectation d'une valeur à une variable

Une fois la variable déclarée, il est possible de lire ou d'écrire dans l'espace mémoire associé. Pour donner une nouvelle valeur à une variable, on utilise dans la plupart des langages le symbole `=`, appelé **opérateur d'affectation**.

    double tauxTVA;
    tauxTVA = 0.206;

Après l'exécution de la ligne `tauxTVA = 0.206`, la zone mémoire identifiée par *tauxTVA* contient la valeur `0,206`. Afin de gagner en concision, on combine souvent déclaration et affectation d'une valeur initiale sur la même ligne.

    double tauxTVA = 0.206;

{{% remark %}}
Dans d'autres langages comme Python ou PHP, la déclaration d'une variable se fait sans préciser son type, qui est déduit implicitement de la valeur qui lui est affectée.
{{% /remark %}}

# Caractéristiques des variables

## Nom d'une variable

Le **nom** d'une variable permet de l'identifier. Il peut comporter des lettres, des chiffres, ainsi que le caractère `_` (*underscore*). On ne peut pas utiliser pour nommer une variable l'un des mots-clés du langage (`int`, `string`, etc).

Afin d'améliorer la lisibilité des programmes, il est conseillé de respecter certaines règles lors du choix des noms des variables. L'une des conventions de nommage les plus employées est la convention [camelCase](http://fr.wikipedia.org/wiki/CamelCase), que nous utiliserons dans la suite de ce cours.

## Type d'une variable

Dans le monde réel, on n'imagine pas ranger son marteau au même endroit que ses bagues, ou que ses chaussures de football. Donner un **type** à une variable revient à préciser si une boîte doit contenir des bijoux, des outils ou plutôt des chaussures.

Les types utilisables dépendent du langage de programmation employé. A chaque type correspond un certain espace réservé en mémoire. Globalement, plus la plage de valeurs d'un type est grande, plus l'espace réservé sera important.

Voici un bref extrait des types utilisables dans le langage C#.

Type C# | Traduction | Signification
--------|------------|--------------
`int` | Entier | Un nombre entier (sans virgule)
`double` | Réel | Un nombre réel (avec virgule)
`string` | Chaîne de caractères | Zéro, un ou plusieurs caractères alphanumériques (lettres et/ou chiffres)
`bool` | Booléen | Vrai ou Faux (`true` ou `false`)

Voici d'autres exemples de déclarations de variables.

    int x = 1;
    string message = "Bonjour";
    double pi;
    bool valide = true;

Donner une type à une variable permet de **restreindre** la plage de ses valeurs possibles. Par exemple, une variable de type entier ne pourra stocker que des valeurs entières. Une tentative pour y affecter une valeur autre qu'un entier provoquera une erreur.

    int nb = 0;
    nb = 1;        // OK : 1 est un entier
    nb = 3.14;     // erreur : 3,14 est un flottant
    nb = "Hello";  // erreur : "Hello" est une chaîne de caractères
    nb = true;     // erreur : true est un booléen

Le typage des variables offre deux avantages :

* améliorer la lisibilité du programme (ou de l'algorithme).
* prévenir les erreurs de type (interdire de ranger une perceuse dans une boîte à bijoux).

## Valeur d'une variable

La **valeur** d'une variable représente le contenu de la zone mémoire associée à la variable. En C\#, la valeur d'une variable doit toujours être compatible avec son type.

## Variables et calculs

Nous avons vu que l'on peut affecter une nouvelle valeur à une variable avec l'opérateur `=`. Il est possible d'employer des variables dans le calcul de cette nouvelle valeur.

    // ...
    double montantTVA = montantHT * tauxTVA;    

Ici, `montantHT * tauxTVA` est ce qu'on appelle une **expression**. Lors de l'exécution du programme, l'expression est évaluée pour donner un résultat que l'on peut affecter à une autre variable. Pendant ce processus, les variables présentes dans l'expression sont automatiquement remplacées par leurs valeurs. Le type du résultat dépend de ceux des variables et de l'opérateur utilisés dans l'expression.

Quand leur type le permet, il est possible d'effectuer des calculs arithmétiques sur des variables. Avec des variables de type entier ou réel, on peut utiliser les opérateurs arithmétiques habituels.

Opérateur | Signification
----------|--------------
`+` | Addition
`-` | Soustraction
`*` | Multiplication
`/` | Division

A présent, nous pouvons prévoir le résultat de l'exécution de notre exemple initial.

    // Définition du montant hors taxes
    double montantHT = 100;
    
    // Définition du taux de TVA à 20,6%
    double tauxTVA = 0.206;
    
    // Calcul du montant de la TVA
    double montantTVA = montantHT * tauxTVA;
    
    // Calcul du montant T.T.C.
    double montantTTC = montantHT + montantTVA;

La variable *montantTVA* reçoit le résultat de la multiplication de `montantHT` par `tauxTVA`. Sa valeur est `20,6`. Ensuite, la variable `montantTTC` reçoit le résultat de l'addition entre `montantHT` et `montantTVA`. La valeur finale de `montantTTC` est donc `120,6`.

