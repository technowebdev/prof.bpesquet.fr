---
title: "Programmation modulaire"
url: /cours/programmation-modulaire
---

L'objectif de ce chapitre est d'apprendre à écrire des programmes en les décomposant en différentes sous-parties.

Introduction
============

Limites des programmes classiques
---------------------------------

Jusqu'à présent, nos programmes ont toujours été écrits d'un bloc. Cependant, lorsque la taille d'un programme augmente, on se rend souvent compte que certaines instructions ou groupes d'instructions ont tendance à se répéter.

**Minimiser la duplication de code** est l'un des objectifs essentiels du (bon) programmeur. En effet, dupliquer du code produit les effets négatifs suivants :

* la taille du programme (nombre de lignes d'instructions) augmente,
* sa lisibilité diminue,
* les modifications du programme sont plus longues et plus complexes (risque d'oubli).

Pour éviter cela, on aimerait pouvoir "factoriser" certaines parties du programme, c'est-à-dire les définir à un seul endroit puis y faire appel autant de fois que nécessaire. Ces parties sont appelées des **sous-programmes**.

Un premier sous-programme
-------------------------

Voici un exemple très simple utilisant un sous-programme.

    // Programme principal
    static void Main(string[] args)
    {
        DireBonjour();
        DireBonjour();
        DireBonjour();
    }

    // Sous-programme
    static void DireBonjour()
    {
        Console.WriteLine("Bonjour !");
    }

{{% img sous_programme.jpg %}}

Le sous-programme défini dans cet exemple se nomme `DireBonjour`. Il est délimité par une paire d'accolades ouvrantes et fermantes.

{{% definition %}}
Le bloc ``static void Main(...)`` constitue le point d'entrée dans le programme, par où commence son exécution. On l'appelle également **programme principal**.
{{% /definition %}}

Dans cet exemple, le sous-programme est appelé trois fois depuis le programme principal. Chaque appel déclenche l'affichage du message "Bonjour !".

{{% definition %}}
Un **sous-programme** est un petit programme inséré dans un programme général. Un sous-programme possède un nom et est délimité par des accolades.
{{% /definition %}}

Déroulement de l'exécution
--------------------------

Jusqu'à présent, les programmes que nous avons étudiés s'exécutaient de manière linéaire, du début à la fin, même en cas de présence de boucles. L'utilisation de sous-programmes va compliquer les choses.

Lorsque qu'on a besoin d'utiliser la fonctionnalité d'un sous-programme, on effectue un **appel** à celui-ci. Cet appel provoque un "branchement" vers le sous-programme, qui s'exécute. Une fois l'exécution du sous-programme terminé, le contrôle revient au niveau de l'appelant et l'exécution se poursuit. Ce fonctionnement est illustré par le schéma ci-après.

{{% image src="appel_sous_prog.jpg" class="centered" %}}

{{% remark %}}
Sans les nommer ainsi, nous avons déjà utilisé plusieurs "sous-programmes" fournis par l'environnement C# comme `Console.WriteLine` ou encore `Convert.ToDouble`.
{{% /remark %}}
    

Intérêt des sous-programmes
---------------------------

Lorsqu'on cherche à résoudre un problème complexe, il est généralement efficace de le **décomposer** en sous-problèmes plus simples. Les sous-programmes permettent d'appliquer ce principe à la réalisation de logiciels : on va décomposer le programme en écrivant plusieurs sous-programmes plus ou moins autonomes, chacun dédié à une tâche particulière. Le programme principal fera appel aux sous-programmes au fur et à mesure de son exécution.

Ainsi écrit sous la forme d'une combinaison de sous-programmes, notre programme final sera plus **lisible** et plus facile à **maintenir** et à **faire évoluer**. De plus, il sera parfois possible de **réutiliser** certains sous-programmes dans d'autre contextes.

Ecriture de sous-programmes
===========================

Valeur de retour
----------------

Le sous-programme que nous avons étudié ne renvoit aucune valeur au programme principal.

    // ...

    // Sous-programme
    static void DireBonjour()
    {
        Console.WriteLine("Bonjour !");
    }

L'absence de valeur de retour est indiquée en C# par le mot-clé `void` avant le nom du sous-programme. Un sous-programme qui ne renvoie pas de valeur est appelé une **procédure**.

En fonction des besoins, il est également possible d'écrire un sous-programme qui renvoie une valeur de retour, comme dans l'exemple ci-dessous.

    static void Main(string[] args)
    {
        string messageRecu = DireBonjour();
        Console.WriteLine("Le sous-programme vous dit : " + messageRecu);
    }

    static string DireBonjour()
    {
        return "Bonjour !";
    }

{{% img sous_prog_fonction.jpg %}}

Par rapport à le version précédente du sous-programme `DireBonjour`, on observe ici la présence d'un **type de retour** (`string`) et le renvoi d'une valeur en fin de sous-programme ("Bonjour !") grâce au mot-clé `return`.

Quand on crée un sous-programme qui renvoie une valeur de retour, on
doit :

* préciser quel est le type de la valeur renvoyée par le sous-programme.
* définir quelle est la valeur renvoyée en utilisant le mot-clé `return` à la fin du sous-programme.

Un sous-programme qui renvoie une valeur est appelé une **fonction**. L'appel d'un sous-programme renvoyant une valeur retourne toujours un résultat, qui peut être récupéré et utilisé ensuite par le programme appelant.

Variables locales
-----------------

Il est possible de déclarer des variables dans un sous-programme de la même manière que dans le programme principal. L'utilisation de variables dans un sous-programme permet d'améliorer sa lisibilité et de réaliser des opérations plus complexes, comme des calculs.

    static void Main(string[] args)
    {
        string messageRecu = DireBonjour();
        Console.WriteLine("Le sous-programme vous dit : " + messageRecu);
    }

    static string DireBonjour()
    {
        string message = "Bonjour !";
        return message;
    }

Le sous-programme de l'exemple ci-dessus comporte une variable `message` de type `string`. Son résultat d'exécution est identique à celui de l'exemple précédent.

{{% definition %}}
Une variable déclarée dans un sous-programme est appelée **variable locale** à ce sous-programme.
{{% /definition %}}

Voici un autre exemple de sous-programme qui fait saisir un nombre entier et le renvoie au programme appelant.

    static void Main(string[] args)
    {
        int nombreSaisi = SaisirEntier();
        Console.WriteLine("Le nombre saisi est " + nombreSaisi);
    }

    static int SaisirEntier()
    {
        Console.Write("Entrez un nombre entier : ");
        string saisie = Console.ReadLine();
        int nombre = Convert.ToInt32(saisie);
        return nombre;
    }

{{% img saisir_entier.jpg %}}

Portée des variables locales
----------------------------

Nous avons rencontré la notion de **portée** d'une variable dans le chapitre précédent (TODO). Cette notion prend de l'importance quand on pratique la programmation modulaire. Voici l'un des exemples précédents, légèrement modifié.

    static void Main(string[] args)
    {
         string messageRecu = DireBonjour();
         Console.WriteLine("Le sous-programme vous dit : " + messageRecu);
         Console.WriteLine("Mais peut-il vous dire " + message + " ?");
    }

    static string DireBonjour()
    {
         string message = "Bonjour !";
         return message;
    }

Une tentative d'exécution se solde par un message d'erreur provenant du compilateur.

{{% img portee_variable_locale.jpg %}}

Cette erreur prouve le fait que la variable *message*, locale au sous-programme `DireBonjour`, n'est pas utilisable en-dehors de celui-ci.

{{% definition %}}
La portée d'une variable locale se limite au sous-programme dans lequel elle est déclarée.
{{% /definition %}}

Ne pas pouvoir utiliser de variables locales en dehors des sous-programmes où elles sont définies peut sembler une limitation. C'est au contraire un grand avantage : chaque sous-programme peut déclarer ses propres variables sans se préoccuper des variables locales définies ailleurs.

Variables globales
------------------

Il existe des situations où on souhaiterait que des variables soient utilisables depuis n'importe quel endroit du programme.

    static void Main(string[] args)
    {
        int a = 5;
        int b = 10;
        Console.WriteLine("Avant l'échange, a=" + " et b=" + b);
        Echanger();
        Console.WriteLine("Après l'échange, a=" + " et b=" + b);
    }

    static void Echanger()
    {
        int temp = b;
        b = a;
        a = temp;
    }

Ce programme ne peut être exécuté : les variables `a` et `b` sont déclarées dans le programme principal et ne sont pas visibles depuis le sous-programme *Echanger*. Ces variables sont locales au programme principal.

{{% img erreur_variable_locale.jpg %}}

Pour pouvoir utiliser `a` et `b` partout, il faut les déclarer en dehors du programme principal et de tout sous-programme. On appelle ces variables des **variables globales**.

    // Déclaration des variables globales
    static int a;
    static int b;
    
    static void Main(string[] args)
    {
        a = 5;
        b = 10;
        Console.WriteLine("Avant l'échange, a=" + a + " et b=" + b);
        Echanger();
        Console.WriteLine("Après l'échange, a=" + a + " et b=" + b);
    }

    static void Echanger()
    {
        int temp = b;
        b = a;
        a = temp;
    }

{{% img variable_globale.jpg %}}

Quand on programme de manière modulaire, il faut être attentif à l'endroit où on déclare les variables. Les variables globales semblent plus pratiques à utiliser puisqu'elles sont visibles depuis n'importe quel endroit du programme.

Cependant, elles présentent plusieurs défauts. Un sous-programme qui utilise des variables globales est plus difficile à réutiliser dans un autre contexte. De plus, une variable globale peut être utilisée depuis n'importe quel endroit du programme, ce qui augmente le risque de modification accidentelle.

{{% tip %}}
Il est conseillé de **minimiser** le nombre de variables globales, voire de s'en passer complètement.
{{% /tip %}}


