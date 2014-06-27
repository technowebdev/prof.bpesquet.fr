---
title: "Structures alternatives"
slug: structures-alternatives
---

L'objectif de ce chapitre est de découvrir comment enrichir nos programmes en leur ajoutant des possibilités d'exécution conditionnelle.

Le programme d'exemple
======================

Le programme ci-dessous permet de comparer deux nombres entiers saisis par l'utilisateur.

    Console.Write("Entrez un premier nombre : ");
    string saisie = Console.ReadLine();
    int nombre1 = Convert.ToInt32(saisie);
    Console.Write("Entrez un second nombre : ");
    saisie = Console.ReadLine();
    int nombre2 = Convert.ToInt32(sais
    if (nombre1 < nombre2)
    {
        Console.WriteLine("Le premier nombre est plus petit que le second");
    }
    else
    {
        if (nombre1 > nombre2)
        {
            Console.WriteLine("Le premier nombre est plus grand que le second");
        }
        else
        {
            Console.WriteLine("Les deux nombres sont égaux");
        }
    }

L'instruction `if`
==================

Pour fonctionner, notre programme d'exemple a besoin de déterminer si le premier nombre saisi est inférieur au second. Pour cela, il utilise une nouvelle structure : l'instruction `if`.

Syntaxe et fonctionnement
-------------------------

La syntaxe du `if` est la suivante.

    if (condition)
    {
        <instructions>
    }

Les accolades ouvrantes et fermantes délimitent ce qu'on appelle une unité de code source, appelée également **bloc de code**. Si la condition placée après l'instruction `if` est **vraie**, alors les instructions contenues dans le bloc de code seront exécutées. Les parenthèses qui délimitent la condition sont indispensables en C#.

{{% definition %}}
L'instruction `if` permet d'exécuter ou non des instructions selon la valeur d'une **condition**.
{{% /definition %}}

{{% remark %}}
On observe que les instructions du bloc associé au ``if`` sont décalées par rapport à l'instruction qui les contient. On dit qu'elles sont **indentées** . Bien indenter ses programmes est une habitude importante à acquérir.
{{% /remark %}}

La notion de condition
----------------------

Voici un court extrait du premier exemple.

    // ...
    if (nombre1 < nombre2)
    {
    // ...

L'instruction `if` est associée à la condition `(nombre1 < nombre2)`. Cette condition est ce que l'on appelle une **expression**.

{{% definition %}}
Une **expression** est un ensemble de valeurs, de variables et d'opérateurs qui produit un résultat.
{{% /definition %}}

Ici, le résultat dépend de la valeur de la variable *nombre* au moment de l'exécution :

* si `nombre1` est strictement inférieur à `nombre2`, le résultat de l'expression est **vrai** (`true` en C#).
* si `nombre1` est supérieur ou égal à `nombre2`, le résultat de l'expression est **faux** (`false` en C#).

Autrement dit, l'expression `(nombre1 < nombre2)` renvoie une valeur de type **booléen**.

Toute expression renvoyant une valeur booléenne peut être utilisée comme condition avec un `if`. C'est le cas des expressions utilisant des opérateurs de comparaison, dont voici la liste.

Opérateur | Signification 
----------|--------------
`==` | Egal à
`!=` | Différent de
`<` | Inférieur strictement 
`<=` | Inférieur ou égal
`>` | Supérieur strictement 
`>=`| Supérieur ou égal

{{% danger %}}
La plupart des langages de programmation utilisent le symbole `=` pour symboliser l'affectation d'une valeur, et le symbole `==` pour l'égalité. Attention aux confusions avec le sens mathématique de l'opérateur `=`.
{{% /danger %}}


L'instruction `else`
====================

Dans notre exemple, on souhaite agir de manière alternative en fonction du résultat de la condition `(nombre1 < nombre2)`. Le message à afficher est différent selon que cette condition soit vraie ou fausse.

    // ...
    if (nombre1 < nombre2)
    {
        // Code exécuté si nombre1 < nombre2
        Console.WriteLine("Le premier nombre est inférieur au second");
    }
    else
    {
        // Code exécuté si nombre1 >= nombre2
        // ...
    }

Syntaxe et fonctionnement
-------------------------

Une alternative s'exprime grâce à l'instruction `if` à laquelle on associe une instruction `else`.

    if (condition)
    {
        <instructions exécutées si la condition est vraie>
    }
    else
    {
        <instructions exécutées si la condition est fausse>
    }

On peut la traduire par : si la condition est vraie alors exécuter les instructions du bloc `if`, sinon exécuter les instructions du bloc `else`.

{{% definition %}}
L'instruction `if ... else ...` permet de créer un **branchement logique** à l'intérieur d'un programme. Pendant l'exécution, les instructions exécutées seront différentes selon la valeur de la condition. Un seul des deux blocs d'instructions sera pris en compte.
{{% /definition %}}

{{% remark %}}
Il est fortement conseillé de toujours indenter les instructions contenues dans les blocs `if` et `else` par rapport à l'instruction qui les contient.
{{% /remark %}}

Instructions `if`/`else` imbriquées
-----------------------------------

Notre programme d'exemple intégre la possibilité que les deux nombres saisis soient égaux.

    // ...
    if (nombre1 < nombre2)
    {
        Console.WriteLine("Le premier nombre est plus petit que le second");
    }
    else
    {
        // Code exécuté si nombre1 >= nombre2 
        if (nombre1 > nombre2)
        {
            // Code exécuté si nombre1 > nombre2 
            Console.WriteLine("Le premier nombre est plus grand que le second");
        }
        else
        {
            // Code exécuté si nombre1 = nombre2 
            Console.WriteLine("Les deux nombres sont égaux");
        }
    }

Il est possible de représenter graphiquement le flux d'exécution du programme d'exemple au moyen d'un **diagramme de flux**.

{{% image src="flux_comparaison.png" class="centered" %}}

Une instruction `if` peut être placée à l'intérieur d'un bloc d'une autre instruction `if`. C'est ce qu'on appelle **imbriquer des conditions**. Il n'y a pas de limite (si ce n'est la lisibilité du programme) au niveau de profondeur des imbrications. Grâce à l'indentation des instructions, on visualise bien les différents blocs de code crées par les instructions `if`.

{{% warning %}}
A chaque accolade ouvrante doit correspondre une accolade fermante.
{{% /warning %}}

Omission des accolades
----------------------

Dans le cas où le bloc de code associé à un `if` ou à un `else` ne comporte qu'une seule instruction, il est possible d'omettre les accolades. Notre programme d'exemple pourrait être réécrit comme ci-dessous.

    // ...
    if (nombre1 < nombre2)
        Console.WriteLine("Le premier nombre est plus petit que le second");
    else
        if (nombre1 > nombre2)
            Console.WriteLine("Le premier nombre est plus grand que le second");
        else
            Console.WriteLine("Les deux nombres sont égaux");

{{% tip %}}
En phase d'apprentissage, il est conseillé d'ajouter systématiquement des accolades pour éviter les mauvaises surprises.
{{% /tip %}}


L'instruction `switch`
======================

Le programme d'exemple
----------------------

Le programme ci-dessous conseille l'utilisateur sur la tenue à porter en fonction de la météo actuelle.

    Console.Write("Fait-il froid dehors ? (1 = un peu, 2 = beaucoup, 3 = à la folie) : ");
    string froid = Console.ReadLine();
    switch (froid)
    {
        case "1":
            Console.WriteLine("Sortez en pull.");
            break;
        case "2":
            Console.WriteLine("Sortez en blouson.");
            break;
        case "3":
            Console.WriteLine("Restez au chaud à la maison !");
            break;
        default:
            Console.WriteLine("Choix incorrect.");
            break;
    }

Syntaxe et fonctionnement
-------------------------

L'instruction `if` ne permet de gérer qu'une condition booléenne vraie ou faux. Dans certains cas, on souhaiterait plutôt pouvoir déclencher un traitement en fonction d'un choix possible parmi plusieurs plutôt que d'imbriquer des `if ... else ...`.

L'instruction `switch` offre la possibilité de répondre de manière appropriée à la valeur saisie. Elle déclenche l'exécution d'un bloc d'instructions parmi plusieurs possibles. Seul le bloc correspondant à la valeur testée sera pris en compte.

Sa syntaxe est la suivante.

    switch (variable)
    {
    case valeur1:
        <instructions>
        break;
    case valeur2:
        <instructions>
        break;
    ...
    default:
        <instructions>
        break;
    }

Il n'y a pas de limite au nombre de cas possibles. Le mot-clé `default`, à placer en fin de `switch`, est optionnel. Il sert souvent à gérer les cas d'erreurs, comme ci-dessus.

{{% warning %}}
Les instructions `break` dans les blocs `case` sont indispensables pour éviter de passer d'un bloc à un autre.
{{% /warning %}}

Conditions complexes
====================

L'opérateur logique &&
----------------------

Supposons qu'on souhaite savoir si la valeur d'une variable `X` est comprise entre 100 et 150.

{{% image src="intervalle_dedans.jpg" class="centered" %}}

Pour cela, il faut regarder si la valeur de `X` est à la fois supérieure ou égale à 100 et inférieure ou égale à 150. L'expression associée serait : `(X >= 100) ET (X <= 150)`. Cette condition est formée de deux sous-conditions qui doivent être vérifiées simultanément pour que le résultat soit vrai.

{{% remark %}}
L'expression ``100 ≤ X ≤ 150`` est mathématiquement valable mais ne peut pas s'employer en programmation.
{{% /remark %}}

En C# comme dans de nombreux autres langages, l'opérateur logique **ET** s'écrit `&&`.

    Console.Write("Entrez X : ");
    string saisie = Console.ReadLine();
    double X = Convert.ToDouble(saisie);
    if ((X >= 100) && (X <= 150))
    {
        Console.WriteLine("X est compris entre 100 et 150");
    }

Avec l'opérateur `&&`, la seule manière d'avoir un résultat vrai est que les deux sous-conditions soient vraies.

L'opérateur logique ||
----------------------

On pourrait égaler souhaiter vérifier le fait que `X` soit en dehors de
l'intervalle [100:150].

{{% image src="intervalle_dehors.jpg" class="centered" %}}

Ici, `X` peut être soit inférieur à 100, soit supérieur à 150. L'expression correspondante est `(X < 100) OU (X > 150)`. Il suffit que l'une ou l'autre des sous-conditions soit remplie pour que le résultat
soit vrai.

L'opérateur logique **OU** s'écrit en C# `||`.

    // ...
    if ((X < 100) || (X > 150))
    {
        Console.WriteLine("X est inférieur à 100 ou supérieur à 150");
    }

Avec l'opérateur `||`, la seule manière d'avoir un résultat faux est que les deux conditions soient fausses.

L'opérateur logique !
---------------------

Exprimer le fait que `X` soit en dehors de l'intervalle [100:150] revient à prendre l'inverse de la condition qui vérifie que `X` est à l'intérieur de cet intervalle. Autrement dit, l'expression
`(X < 100) OU (X > 150)` est équivalente à `Non((X >= 100) ET (X <= 150))`.

L'opérateur logique **NON** qui inverse la valeur d'une condition booléenne s'écrit en C# `!`.

    // ...
    if (!((X >= 100) && (X <= 150)))
    {
        Console.WriteLine("X est inférieur à 100 ou supérieur à 150");
    }
