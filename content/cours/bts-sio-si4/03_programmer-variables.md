---
title: "Programmer avec des variables"
url: /cours/programmer-variables
---

L'objectif de ce chapitre est de découvrir comment utiliser des variables dans un programme.

# Le programme d'exemple

Le programme d'exemple du chapitre précédent était simpliste. Enrichissons-le en permettant à l'utilisateur de saisir le montant hors taxes et en lui affichant le résultat du calcul.

    string msg = "Bienvenue dans l'application TVA !";
    Console.WriteLine(msg);
    
    // Saisie et conversion du montant hors taxes
    Console.Write("Entrez un montant HT : ");
    string saisie = Console.ReadLine();
    double montantHT = Convert.ToDouble(saisie);
    
    // Définition du taux de TVA à 20,6%
    double tauxTVA = 0.206;
    
    // Calcul du montant T.T.C.
    double montantTTC = montantHT * (1 + tauxTVA);
    
    // Affichage du montant converti
    string sortie = "Le montant TTC est de " + montantTTC;
    Console.WriteLine(sortie);
    
    Console.WriteLine("Merci d'avoir utilisé l'application. Au revoir !");

Voici le résultat de son exécution sous la forme d'une application console.

{{% img calcul_tva.jpg %}}


# Chaînes de caractères

## Création d'une chaîne de caractères

Une chaîne de caractères (en anglais `string`) représente un ensemble de caractères. Un caractère correspond *grosso modo* à ce qu'on peut obtenir en tapant sur une touche d'un clavier : une lettre, un chiffre, un espace, un signe de ponctuation, un symbole comme $ ou µ.

En programmation, on matérialise le début et la fin d'une chaîne de caractères avec des **guillemets doubles** (caractère `"`).

    string msg = "Bienvenue dans l'application TVA !";

# Concaténation de chaînes

Il est possible de créer une chaîne de caractères par assemblage d'autres chaînes. Cette opération s'appelle la **concaténation**. En C#, elle est réalisée au moyen de l'opérateur `+`.

    string msg = "Bienvenue";
    msg = msg + " en";
    msg += " BTS SIO !";

Ici, la valeur finale de la variable *msg* sera *Bienvenue en BTS SIO !*. L'opérateur `+=` est un raccourci : écrire `variable += valeur` équivaut exactement à écrire `variable = variable + valeur`, en plus concis.

# Affichage à l'écran

L'instruction C# `Console.WriteLine` permet d'écrire à l'écran le texte qui la suit entre parenthèses.

    string msg = "Bienvenue dans l'application TVA !";
    Console.WriteLine(msg);

Le texte à afficher est fourni sous la forme d'une chaîne de caractères : soit une variable de type `string`, soit directement un texte entre guillemets.

    Console.WriteLine("Merci d'avoir utilisé l'application. Au revoir !");

# Saisie d'informations

L'instruction C# `Console.ReadLine` permet d'attendre le résultat de la saisie utilisateur au clavier. Ici, son résultat est affecté à la variable nommée `saisie`, qui est de type `string`.

    // ...
    string saisie = Console.ReadLine();

{{% remark %}}
``Console.ReadLine`` renvoit toujours une valeur de type ``string``, même si l'utilisateur saisit une valeur compatible avec un autre type, comme un entier.
{{% /remark %}}
  

# Conversion de type

## Conversion explicite

Nous avons vu précédemment que des variables devaient être de type numérique pour pouvoir être utilisées dans des calculs. Cependant, l'instruction `Console.ReadLine` renvoit toujours une chaîne de caractères (`string`). Le langage C# permet heureusement de convertir cette chaîne en une valeur numérique.

    // ...
    string saisie = Console.ReadLine();
    double montantHT = Convert.ToDouble(saisie);  // conversion explicite

L'instruction C# `Convert.ToDouble` permet de passer d'une valeur de type `string` (ici la variable `saisie`) à un résultat de type `double`, affecté ici à la variable `montantHT`. Il s'agit d'une conversion de type expressément demandée par le programmeur, ou conversion **explicite**.


# Conversion implicite

Dans certaines situations, le langage C# peut automatiser la conversion de type sans intervention du programmeur. On parle alors de conversion **implicite**.

    // ...
    double montantTTC = montantHT * (1 + tauxTVA);
    string sortie = "Le montant TTC est de " + montantTTC;  // conversion implicite
    Console.WriteLine(sortie);

Ici, une conversion implicite de la variable `montantTTC` (de type `double`) vers le type `string` a lieu avant la concaténation. Il est même possible d'être encore plus concis.

    // ...
    double montantTTC = montantHT * (1 + tauxTVA);
    Console.WriteLine("Le montant TTC est de " + montantTTC);  // conversion implicite

Les principales conversions implicites concernent :

* les conversions d'un type numérique (`int`, `double`) vers le type `string`.
* les conversion d'un type numérique vers un autre type numérique capable de stocker l'information sans perte.

\

    int a = 3;
    double b = a;  // OK, un réel peut stocker une valeur entière
    int c = b;     // erreur : un entier ne peut pas stocker une valeur réelle

# Erreurs fréquentes

## Redéclaration d'une variable

Au sein d'une même unité de code source, deux variables différentes ne peuvent pas porter le même nom. En C#, une unité de code source est la zone délimitée par une paire d'accolades ouvrantes et fermantes.

Une erreur fréquente consiste à redéclarer la variable qu'on souhaite simplement réutiliser. Cela provoque une erreur, comme dans l'exemple ci-dessous.

    // ...
    double montantHT = 0;
    // ...
    double montantHT = 150;  // Erreur : redéclaration de la variable montantHT !

Comme la plupart des langages, le C# fait la distinction entre les minuscules et les majuscules dans les noms des variables. On dit qu'il est **sensible à la casse** (*case sensitive*).

    // ...
    double montantHT = 0;
    // ...
    double montantHt = 150;  // OK : déclaration d'une nouvelle variable montantHt

## Utilisation d'une variable non initialisée

Le langage C# interdit l'utilisation d'une variable tant qu'une valeur ne lui a pas été affectée.

    double a;
    double b = a;  // erreur : a n'a pas de valeur

## Mauvaise utilisation des guillemets

Dans un programme C#, tout ce qui se trouve à l'intérieur d'une paire de guillemets est considéré comme une chaîne de caractères. Il faut donc être attentif au placement des guillemets, puisque le typage des variables interdit de leur affecter une valeur incompatible avec leur type.


    double val = 20.6;    // OK
    double val = "20.6";  // erreur : "19.6" est une valeur de type string

    string msg = "3.14";  // OK
    string msg = 3.14;    // erreur : 3.14 est une valeur de type réel

## Confusion entre concaténation et addition

L'opérateur `+` a un sens différent selon le type de ses arguments :

* appliqué à des entiers ou des réels, il exprime l'addition mathématique.
* appliqué à des chaînes de caractères, il permet de les concaténer en une seule chaîne.

\

    int x = 421;
    int y = 9;
    int z = x + y;         // après l'exécution, la variable z vaut 430

    string a = "421";
    string b = "9";
    string c = a + b;      // après l'exécution, la variable c vaut "4219"
    string d = "a + b";    // après l'exécution, la variable d vaut "a + b"
    string e = "a" + "b";  // après l'exécution, la variable e vaut "ab"

## Chaîne de caractères vide

Une variable de type `string` possède une "valeur" initiale particulière : `null`. Il s'agit plutôt d'un mot-clé qui signifie : absence de valeur. Il ne faut pas le confondre avec la chaîne vide (`""`).

    string msg1;        // msg1 n'a pas de valeur
    string msg2 = "";   // la valeur de msg2 est ""
