---
title: "Démonstration"
---

Cette page illustre les différentes possibilités d'affichage du site.

# Texte et listes

Voici un texte *en italiques*, un autre **en gras** et un dernier `sous forme de code`.

### Liste non ordonnée

Voici une liste non ordonnée :

* Elément 1
* Elément 2
* Elément 3
    * Sous-élément 1
    * Sous-élément 2
* ...

### Liste ordonnée

Et voici une liste ordonnée :

1. Elément 1
2. Elément 2
3. Etc

# Code source

Les extraits de code source sont mise en valeur selon le langage.

```php
// PHP
<?php
echo("Bonjour le monde.");
?>
```

```c#
// C#
class Program {
    static void Main(string[] args) {
        Console.WriteLine("Bonjour le monde.");
    }
}
```

```java
// Java
public class Program {
    public static void main(String[] args) {
        System.out.println("Bonjour le monde.");
    }
}
```

Liens vers des ressources
-------------------------

### Lien interne au document (ancre)

Attention, [danger](#toc_15) !

### Lien vers un autre document

[Cette page](/site/) présente ce site Web.

### Lien externe

Allons faire un tour sur [Wikipedia](http://fr.wikipedia.org/).

#### Lien explicite

On peut aussi utiliser un lien explicite : <http://fr.wikipedia.org>.

### Image

Une image est insérée ci-dessous.

![The Lemon Cat](/images/lemoncat.jpg)

### Figure

Voici une figure (image avec légende).

 {{% figure src="/images/lemoncat.jpg" title="The Lemon Cat" %}}

Paragraphes spéciaux
--------------------

### Citation

> C'est au pied du mur qu'on voit le mieux le mur.

### Définition

{{% definition %}}
La **procrastination** est la tendance à remettre systématiquement au lendemain des actions.
{{% /definition %}}

{{% test "*Défi*" %}}

### Remarque

{{% remark %}}
Rien de spécial.
{{% /remark %}}

### Conseil

{{% tip %}}
Faisez gaffe aux pigeons.
{{% /tip %}}

### Avertissement

{{% warning %}}
A long terme, nous serons tous morts.
{{% /warning %}}

### Danger

{{% danger %}}
Ne jamais croiser les effluves !
{{% /danger %}}

Tableaux
--------
Les tableaux au format Markdown sont gérés.

Nom     |   Age
--------|------
**Julie**   |   29
Lionel  |   47
Martin  |   32

Questions/réponses
------------------

Il est possible d'ajouter une question comme ci-dessous.

{{% question text="Quelle est la couleur du cheval blanc d'Henri IV ?" %}}
Il est blanc comme vous l'aurez deviné.
{{% /question %}}

# Divers

<ul id="pageContainer">
### Stap 1
</ul>
