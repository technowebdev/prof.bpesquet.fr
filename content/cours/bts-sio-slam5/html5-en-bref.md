---
title: "La norme HTML5 en bref"
url: /cours/html5-en-bref
---

# Présentation

Le langage HTML (*HyperText Markup Language*) a été inventé pour décrire une page Web. Il emploie des balises structurantes. Le terme HTML5 regroupe un ensemble d'évolutions du langage HTML visant à enrichir le langage pour faciliter l'écriture de clients Web riches tout en maintenant une rétrocompatibilité optimale avec l'existant. 

{{% image src="html5_logo.png" class="centered" %}}

# Support par les navigateurs actuels

HTML5 n'est pas encore un standard officiel et aucun navigateur n'offre un support exhaustif de la norme (dont certaines parties sont de toute façon susceptibles d'être modifiées...). A moins d'être dans un contexte Intranet, le développeur Web ne maîtrise pas le choix du navigateur utilisé par les utilisateurs qui visitent son site. 

{{% image src="html5_browser_support.png" class="centered" %}}

Il faut savoir que des versions antérieures d'Internet Explorer, notamment la tristement fameuse version 6, sont toujours utilisées par une part non négligeable des utilisateurs de Web.

Cela dit, tous les éditeurs de navigateurs améliorent le support à chaque nouvelle version de leur logiciel. Il est également possible d'utiliser des bibliothèques Javascript comme Modernizr ou html5shiv qui émulent les nouvelles fonctionnalités sur les anciens navigateurs. Plusieurs sites inventorient l'état du support des différentes parties de la norme et permettent au développeur Web de savoir à quoi s'attendre.

* http://html5test.com
* http://caniuse.com
* http://html5readiness.com

Le site http://html5please.com est particulièrement intéressant, puisqu'il fournit de précieux conseils sur les éléments de la norme prêts à être utilisés en production et ceux qu'il vaut mieux laisser mûrir.

# Quelques nouveautés de HTML5

## Les balises sectionnantes

Lorsqu'on voulait réaliser une mise en page moderne avec la version précédente d'HTML, on devait utiliser abondamment l'élément `<div>` (associé à une feuille de style) afin de définir les différentes parties de la page et leurs positions respectives.

    <div id="en_tete">
        <!-- Bannière -->
    </div>
    
    <div id="menu">
        <!-- Menu de navigation -->
    </div>
    
    <div id="corps">
        <!-- Contenu principal de la page -->
    </div>
    
    <div id="pied_de_page">
        <!-- Nom de l'auteur... -->
    </div>

{{% image src="html_div_layout.jpg" class="centered" %}}

HTML5 a pris en compte ce besoin récurrent et apporte de nouvelles balises pour y répondre. Elles permettent de mettre en forme une page Web comme décrit ci-dessous.

{{% image src="html5_sematic_layout.jpg" class="centered" %}}

Les informations de l'en-tête, ou la bannière sont placées à l'intérieur de la balise `<header>`. Dans cette partie, on peut placer des  images, des liens, des textes…

    <header>
        <!-- contenu de l'en-tête de la page -->
    </header>

Les principaux liens de navigation sont regroupés dans la balise `<nav>`.  Généralement, le menu est réalisé sous forme de liste à puces à l'intérieur de la balise.

    <nav>
        <ul>
            <li><a href="index.html">Accueil</a></li>
            <li><a href="contact.html">Contact</a></li>
            <li><a href="pagebts.html">BTS SIO</a></li>
            <li><a href="equipe.html">L'équipe</a></li>
        </ul>
    </nav>

La balise `<section>` sert à découper une page Web en plusieurs sous-parties : introduction, news, chapitres, etc.

    <section>
        <h1>Voici une section de page</h1>
        <p>et mon contenu de section</p>
    </section>

La balise `<aside>` contient des informations complémentaires à la page, placées par exemple sur le coté droit (une explication complémentaire, une photo, etc).  On peut  avoir plusieurs blocs `<aside>` dans la page.

    <aside>
        <!-- informations complémentaires -->
    </aside>

La balise `<article>` contient une partie autonome de la page, par exemple des actualités. Un article est susceptible d'être syndiqué via un flux RSS.

    <article>
        <h1>Mon article</h1>
        <p>rédaction …</p>
    </article>

Les informations du pied de page sont placées à l'intérieur de la balise `<footer>`. On y trouve des informations comme des liens de contact, le nom de l'auteur, les mentions légales, etc.

    <footer>
        <!-- contenu du pied de page -->
    </footer>

Ces nouvelles balises rendent la mise en page du site plus lisible, améliorent son rendu sur les différents types de terminaux Web (tablettes, smartphones, etc) et facilitent l'indexation du contenu de la page par les moteurs de recherche.

Cependant; l'usage de balises `<div>` pour la mise en page reste toujours possible, comme dans l'exemple ci-dessous. Il illustre le cas où une page ne comporte qu'une seule section de contenu.

{{% image src="html5_div_layout.jpg" class="centered" %}}

## Les balises sémantiques

HTML5 apporte également de nouvelles balises destinées à donner plus de sémantique (plus de sens, de signification) à vos pages Web. Cela permet une meilleure compréhension de votre code par les humains et les machines (navigateurs Web, moteurs de recherche, etc).

Citons par exemple la balise `<time>` qui permet d'indiquer une date/heure dans une page.

    <time datetime="2012-11-08">8 Novembre 2012</time>

L'attribut `datetime` permet de faire comprendre aux machines la vraie date, afin de faciliter les opérations d'affichage, de tri, etc. Le contenu de la balise représente le texte affiché à l'utilisateur.

Il en existe d'autres, par exemple `<figure>` qui définit une illustration accompagnée de la légende.

## Les formulaires enrichis

### Nouveaux champs de saisie

Voici quelques-uns des nouveaux types de champs utilisables dans les formulaires HTML5 :

* email
* search
* tel
* url
* date
* number
* range
* color

Chacun permet de saisir une donnée du type associé : un champ `email` permettra de saisir une adresse de courriel, un champ `date` permettra de saisir une date, etc. Ces nouveaux champs améliorent l'ergonomie des formulaires Web en les rapprochant des formulaires qu'on peut trouver sur un client lourd. Certains disposent d'attributs supplémentaires qui restreignent les possibilités de saisie, comme dans cet exemple.

    <input type="number" min="0" max="100" step="5" value="50" />

Voici son rendu sur votre navigateur : <input type="number" min="0" max="100" step="5" value="50" />

Ici, l'utilisateur pourra saisir un nombre compris entre 0 et 100. La valeur initiale du champ sera 50 et elle augmentera ou diminuera par pas de 5.

La page http://html5demo.braincracking.org/demo/input.php fournit une démonstration de l'utilisation de ces champs.  

{{% warning %}}
Le rendu de ces nouveaux champs varie assez fortement d'un navigateur à l'autre.
{{% /warning %}}

### Aide à la saisie

Deux attributs des balises de saisie permettent d'aider l'utilisateur du formulaire :

* `autofocus` (booléen) place le focus sur le champ au chargement du formulaire.
* `placeholder` définit le contenu par défaut du champ.

\ 

    <input type="email" autofocus placeholder="utilisateur@domaine.fr" />

{{% remark %}}
Les attributs booléens sont une autre nouveauté de HTML5.
{{% /remark %}}

### Validation des entrées

Si la validation finale des valeurs saisies dans un formulaire doit toujours se faire côté serveur (par exemple avec PHP) pour des raisons de sécurité, HTML5 permet de mieux guider l'utilisateur dans sa saisie sans avoir besoin de recourir au Javascript ou à d'autres bibliothèques.

Pour commencer, les nouveaux champs de saisie impliquent une restriction automatique des valeurs qu'il est possible d'entrer. Par exemple, voici la définition d'un champ de type courriel.

    <input type="email" />

Si l'utilisateur saisit une chaîne non conforme au format d'une adresse de courriel, le navigateur compatible avec HTML5 affichera un message d'erreur.

{{% image src="html5_email_validation.jpg" class="centered" %}}

Il est également possible de rendre un champ obligatoire grâce à l'attribut booléen `required`.

    <input type="email" required />