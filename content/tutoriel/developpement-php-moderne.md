---
title: "Développement PHP moderne"
date: 2014-07-22
---

Découvrez comment bâtir une application Web fonctionnelle et sûre en tirant le meilleur du langage PHP.

{{% image src="PHP_moderne.png" class="centered" %}}

# Introduction

## Pourquoi ce tutoriel

Le langage [PHP](http://php.net) est à l'heure actuelle le principal langage serveur du Web dynamique. Il souffre malgré tout d'un déficit d'image par rapport à des technologies concurrentes comme ASP.NET ou Java. Ces dernières imposent un cadre rigide qui guide et rassure le développeur. A l'inverse, PHP est une technologie très souple qui laisse beaucoup de liberté, y compris celle de faire un peu n'importe quoi. Lorsqu'on développe en PHP, il est donc essentiel de connaître et d'appliquer les meilleures pratiques.

PHP a évolué avec le temps et dispose à présent de fonctionnalités avancées parfois méconnues. Son écosystème est très riche et des milliers de projets cherchent à améliorer l'expérience du développeur PHP. Il n'est pas facile de se repérer dans cette jungle foisonnante pour choisir les bons outils.

Ce tutoriel vise à présenter une manière de concevoir une application Web en tirant parti des possibilités qu'offre le langage PHP et en s'appuyant sur des outils de son écosystème qui ont fait leurs preuves. En un mot, en utilisant PHP de manière **moderne**.

## Contexte choisi

Nous allons mettre en oeuvre les principes présentés dans ce tutoriel en construisant un exemple simple : une application Web de type [CMS](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_contenu). Notre micro-CMS d'exemple sera basique : il permettra de gérer une liste d'articles ainsi que les commentaires associés.

L'application Web obtenue en fin de tutoriel est [accessible en ligne](http://microcms.bpesquet.fr). Le code source associé est disponible sur [GitHub](https://github.com/bpesquet/MicroCMS).

## Méthodologie de réalisation

En nous inspirant des [méthodes agiles](http://fr.wikipedia.org/wiki/M%C3%A9thode_agile) comme [SCRUM](http://fr.wikipedia.org/wiki/Scrum_(m%C3%A9thode\)), nous allons bâtir l'application par étapes successives appelées **itérations**, ou encore [sprints](http://fr.wikipedia.org/wiki/Scrum_\(m%C3%A9thode\)#Le_sprint) dans SCRUM. 

{{% definition %}}
Une itération est une phase de travail volontairement courte permettant de produire une version intermédiaire mais livrable d'un produit.
{{% /definition %}}

Certaines itérations seront consacrées à l'ajout de nouvelles fonctionnalités à l'application. Les autres permettront d'améliorer son architecture en pratiquant ce qu'on appelle la [refactorisation](http://fr.wikipedia.org/wiki/R%C3%A9usinage_de_code) (*refactoring*). 

## Remerciements

Les ressources ci-dessous ont été d'une aide précieuse pour l'écriture de ce tutoriel :

* [Learning PHP development with Silex](http://bojanz.wordpress.com/2013/11/11/learning-php-development-with-silex/) (ma principale source d'inspiration).
* [Silex: getting your project structure right](http://php-and-symfony.matthiasnoback.nl/2012/01/silex-getting-your-project-structure-right/)
* [Scaling a Silex code base](https://igor.io/2012/11/09/scaling-silex.html)
* [PHP: the right way](http://www.phptherightway.com/)

J'ai bénéficié des conseils avisés de [Matthieu Gauthey](https://twitter.com/mgauthey), [Pablo Pernot](http://www.areyouagile.com/) et de mon collègue Alain Arsane.

# Itération 1 : initialisation de l'application

Le but de cette itération est d'écrire la toute première version de notre application Web d'exemple. Conformément aux principes de l'agilité, nous commençons par réaliser ce qui apporte le plus de "valeur" à notre CMS : la page d'accueil qui affiche la liste de tous ses articles.

## Création de la base de données

Le rôle principal de notre CMS est de gérer des articles. Tous les articles sont sauvegardés dans une base de données relationnelle nommée `microcms`. Le SGBDR utilisé est MySQL dans notre contexte. Un utilisateur MySQL nommé `microcms_user` a tous les droits sur la base `microcms`. Il est utilisé pour se connecter à MySQL depuis notre application Web.

Un article est caractérisé par son titre (`art_title`) et son contenu (`art_content`). On modélise un article sous la forme d'un enregistrement dans une table nommée `t_article`. Le champ `art_id` est la clé primaire de cette table.

{{% image src="microcms_t_article.png" class="centered" %}}

Voici le script SQL `structure.sql` qui permet de créer la base de données.

    create database if not exists microcms character set utf8 collate utf8_unicode_ci;
    use microcms;
    
    grant all privileges on microcms.* to 'microcms_user'@'localhost' identified by 'secret';
    
    drop table if exists t_article;
    
    create table t_article (
        art_id integer not null primary key auto_increment,
        art_title varchar(100) not null,
        art_content varchar(2000) not null
    ) engine=innodb character set utf8 collate utf8_unicode_ci;

On ajoute dans cette table un petit jeu de données de test contenant quelques articles. Voici le script SQL `content.sql` associé.

    insert into t_article (art_title, art_content) values
    ('First article', 'Hi there! This is the very first article.');
    insert into t_article (art_title, art_content) values
    ('Lorem ipsum', 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut hendrerit mauris ac porttitor accumsan. Nunc vitae pulvinar odio, auctor interdum dolor. Aenean sodales dui quis metus iaculis, hendrerit vulputate lorem vestibulum. Suspendisse pulvinar, purus at euismod semper, nulla orci pulvinar massa, ac placerat nisi urna eu tellus. Fusce dapibus rutrum diam et dictum. Sed tellus ipsum, ullamcorper at consectetur vitae, gravida vel sem. Vestibulum pellentesque tortor et elit posuere vulputate. Sed et volutpat nunc. Praesent nec accumsan nisi, in hendrerit nibh. In ipsum mi, fermentum et eleifend eget, eleifend vitae libero. Phasellus in magna tempor diam consequat posuere eu eget urna. Fusce varius nulla dolor, vel semper dui accumsan vitae. Sed eget risus neque.');
    insert into t_article (art_title, art_content) values
    ('Lorem ipsum in french', "J’en dis autant de ceux qui, par mollesse d’esprit, c’est-à-dire par la crainte de la peine et de la douleur, manquent aux devoirs de la vie. Et il est très facile de rendre raison de ce que j’avance. Car, lorsque nous sommes tout à fait libres, et que rien ne nous empêche de faire ce qui peut nous donner le plus de plaisir, nous pouvons nous livrer entièrement à la volupté et chasser toute sorte de douleur ; mais, dans les temps destinés aux devoirs de la société ou à la nécessité des affaires, souvent il faut faire divorce avec la volupté, et ne se point refuser à la peine. La règle que suit en cela un homme sage, c’est de renoncer à de légères voluptés pour en avoir de plus grandes, et de savoir supporter des douleurs légères pour en éviter de plus fâcheuses.");

Démarrez les serveurs Apache et MySQL, puis importez successivement les scripts `structure.sql` et `content.sql` en utilisant votre outil d'administration MySQl favori (phpMyAdmin par exemple). Notre base de données est maintenant prête à être utilisée.

## Affichage de la liste des articles

### Fichier source PHP

A présent, écrivons le fichier source `index.php` qui affiche la liste de tous les articles. Nous allons travailler directement dans le répertoire servi par votre serveur Web local. Son emplacement dépend de votre installation. Voici quelques emplacements possibles : 

* `c:\xampp\htdocs` sous Windows.
* `/var/www` sous Linux.
* `/Applications/MAMP/htdocs`sous Mac. 

Créez dans ce répertoire un sous-répertoire nommé `MicroCMS` qui sera le répertoire racine de notre application Web. Déplacez-vous dans ce répertoire puis créez un fichier texte nommé `index.php`. Ensuite, copiez-collez le code source ci-dessous dans ce fichier.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8" />
        <link href="microcms.css" rel="stylesheet" />
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <header>
            <h1>MicroCMS</h1>
        </header>
        <?php
        $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
        $articles = $bdd->query('select * from t_article order by art_id desc');
        foreach ($articles as $article): 
        ?>
            <article>
                <h2><?= $article['art_title'] ?></h2>
                <p><?= $article['art_content'] ?></p>
            </article>
        <?php endforeach; ?>
        <footer class="footer">
            <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
        </footer>
    </body>
    </html>

Ce code source mérite quelques commentaires :

* il utilise la norme [HTML5](http://fr.wikipedia.org/wiki/HTML5) et emploie certaines nouvelles balises, comme \<article\> ;
* il utilise [l'affichage abrégé](http://php.net/manual/fr/function.echo.php) `<?= … ?>` plutôt que `<?php echo … ?>`, ainsi que la [syntaxe alternative](http://php.net/manual/fr/control-structures.alternative-syntax.php) pour la boucle `foreach` ;
* il utilise l'extension [PDO](http://php.net//manual/fr/book.pdo.php) de PHP afin d'interagir avec la base de données.

Pour le reste, il s'agit d'un exemple classique d'utilisation de PHP pour construire une page dynamique affichée par le navigateur client.

### Feuille de style CSS

Afin d'améliorer la présentation, nous utilisons une feuille de style nommé `microcms.css`.

    .footer {
        border-top: 1px solid #ccc;
        padding-top: 10px;
        text-align: center;
    }

Créez cette feuille de style dans le même répertoire que le fichier `index.php`.

### Affichage obtenu

Après avoir vérifié que votre serveur Web est bien démarré, lancez votre navigateur Web favori et tapez l'URL http://localhost/microcms. Vous devez voir s'afficher la liste des articles.

{{% image src="microcms_articles_flatphp.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-01).

## Bilan

La toute première version (très simpliste) de notre application Web est maintenant opérationnelle. Elle nous a permis d'initialiser la structure de l'application. La prochaine itération va consister à améliorer son architecture.


# Itération 2 : refactorisation de l'architecture

Le but de cette itération est de modifier notre application Web d'exemple en introduisant une architecture de type MVC (Modèle-Vue-Contrôleur).

## Critique de l'application existante

Les principaux défauts de notre application Web actuelle sont les suivants :

* elle mélange balises HTML et code PHP ;
* sa structure est monobloc, ce qui rend sa réutilisation difficile.

De manière générale, tout logiciel doit gérer plusieurs problématiques :

* interactions avec l'extérieur, en particulier l'utilisateur : saisie et contrôle de données, affichage. C'est la problématique de **présentation** ;
* opérations sur les données (calculs) en rapport avec les règles métier (« business logic »). C'est la  problématique des **traitements** ;
* accès et stockage des informations qu'il manipule, notamment entre deux utilisations. C'est la problématique des **données**.

L'application Web actuelle mélange code de présentation (les balises HTML) et accès aux données (requêtes SQL). Ceci est contraire au **principe de responsabilité unique** (*Single Responsibility Principle*). Ce principe de conception logicielle est le suivant : afin de clarifier l'architecture et de faciliter les évolutions, une application bien conçue doit être décomposée en sous-parties, chacune ayant un rôle et une responsabilité particuliers. 

L'architecture actuelle montre ses limites dès que le contexte se complexifie. Le volume de code des pages PHP explose et la maintenabilité devient délicate. Il faut faire mieux.

## Séparation des responsabilités

### Isolation de l'affichage

Une première amélioration consiste à séparer le code d'accès aux données du code de présentation au sein du fichier `index.php`.

    <?php
    // Data access
    $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
    $articles = $bdd->query('select * from t_article order by art_id desc');
    ?>
    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8" />
        <link href="microcms.css" rel="stylesheet" />
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <header>
            <h1>MicroCMS</h1>
        </header>
        <?php foreach ($articles as $article): ?>
            <article>
                <h2><?= $article['art_title'] ?></h2>
                <p><?= $article['art_content'] ?></p>
            </article>
        <?php endforeach; ?>
        <footer class="footer">
            <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
        </footer>
    </body>
    </html>

Le code est devenu plus lisible, mais les problématiques de présentation et d'accès aux données sont toujours gérées au sein d'un même fichier PHP. En plus de limiter la modularité, ceci est contraire aux bonnes pratiques de développement PHP (norme [PSR-1](http://www.php-fig.org/psr/psr-1/)).

On peut aller plus loin dans le découplage en regroupant le code d'affichage précédent dans un fichier dédié nommé `view.php`.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8" />
        <link href="microcms.css" rel="stylesheet" />
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <header>
            <h1>MicroCMS</h1>
        </header>
        <?php foreach ($articles as $article): ?>
            <article>
                <h2><?= $article['art_title'] ?></h2>
                <p><?= $article['art_content'] ?></p>
            </article>
        <?php endforeach; ?>
        <footer class="footer">
            <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
        </footer>
    </body>
    </html>

Le fichier `index.php` devient alors :

    <?php
    // Data access
    $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
    $articles = $bdd->query('select * from t_article order by art_id desc');
    
    // Data display
    require 'view.php';

La fonction PHP [require](http://php.net//manual/fr/function.require.php) fonctionne de manière similaire à [include](http://php.net/manual/fr/function.include.php) : elle inclut et exécute le fichier spécifié. En cas d'échec, `include` ne produit qu'un avertissement alors que `require stoppe l'exécution du fichier source.

{{% remark %}}
La balise de fin de code PHP `?>` est volontairement omise à la fin du fichier `index.php`. C'est une [bonne pratique](http://php.net/manual/fr/language.basic-syntax.phptags.php) pour les fichiers qui ne contiennent que du PHP. Elle permet d'éviter des problèmes lors d'inclusions de fichiers.
{{% /remark %}}

### Isolation de l'accès aux données

Nous avons amélioré l'architecture de notre application, mais nous pourrions gagner en modularité en isolant le code d'accès aux données dans un fichier PHP dédié. Appelons ce fichier `model.php`.

    <?php

    // Return all articles
    function getArticles() {
        $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
        $articles = $bdd->query('select * from t_article order by art_id desc');
        return $articles;
    }

Dans ce fichier, nous avons déplacé la récupération des articles du CMS à l'intérieur d'une fonction nommée `getArticles.

Le code d'affichage (fichier `view.php`) ne change pas. Le lien entre accès aux données et présentation est effectué par le fichier `index.php`. Ce fichier est maintenant très simple.

    <?php

    require 'model.php';
    $articles = getArticles();
    require 'view.php';

Le résultat affiché reste bien entendu identique.

## Bilan

Outre la feuille de style `microcms.css`, notre application Web est maintenant constituée de trois fichiers :

* `model.php` (PHP uniquement) pour l'accès aux données ;
* `view.php` (PHP et HTML) pour l'affichage des billets du blog ;
* `index.php` (PHP uniquement) pour faire le lien entre les deux pages précédentes.

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-02).

Cette nouvelle structure est plus complexe, mais les responsabilités de chaque partie sont maintenant claires. En faisant ce travail de *refactoring*, nous avons rendu notre exemple conforme à un modèle d'architecture très employé sur le Web : le modèle **MVC**. Si vous découvrez ce concept, consultez impérativement le [cours sur le modèle MVC](/cours/modele-mvc).


# Itération 3 : intégration d'un framework PHP

Le but de cette itération est d'intégrer un *framework* à notre application.

## Avantages apportés par un framework

En informatique comme ailleurs, il est rarement utile de réinventer la roue. La plupart des applications Web ont les mêmes besoins de base : accès au contenu de la requête HTTP reçue, création et renvoi de la réponse, gestions des sessions... Il existe une catégorie de logiciels dont le rôle est de gérer ces besoins communs : ce sont les **frameworks**.

Un framework fournit un ensemble de services de base, généralement sous la forme de classes en interaction. À condition de respecter l'architecture qu'il préconise (souvent une déclinaison du modèle MVC), un framework PHP libère le développeur de nombreuses tâches techniques comme le routage des requêtes, la sécurité, la gestion du cache, etc. Cela lui permet de se concentrer sur l'essentiel, c'est-à-dire ses tâches métier. Il existe une grande quantité de frameworks PHP. Parmi les plus connus, citons [Symfony](http://symfony.com/), [Zend Framework](http://framework.zend.com/) ou encore [Laravel](http://laravel.com/).

## Choix du framework

Il est possible d'écrire soi-même son propre framework, puis de le réutiliser dans tous ses projets PHP. C'est une tâche intéressante et formatrice, mais il est difficile d'obtenir le niveau de qualité et de sûreté que peut offrir un framework professionnel du marché. Si la construction d'un framework PHP vous intéresse, consultez le tutoriel [Evoluer vers une architecture MVC en PHP](http://bpesquet.developpez.com/tutoriels/php/evoluer-architecture-mvc/). Ici, nous allons utiliser un framework existant plutôt que d'en construire un nous-même.

Au sein de l'écosystème des frameworks PHP, deux catégories coexistent. Les frameworks classiques comme Symfony2 ou Zend fournissent un très grand nombre de services (gestion avancée des formulaires, *mapping* objet-relationnel, etc). Ces frameworks complexes imposent leur architecture au développeur et peuvent être intimidants pour un développeur PHP débutant.

L'autre catégorie de frameworks se concentre sur un ensemble réduit de services de base, et laisse au développeur beaucoup de liberté pour construire son application. On les appelle des **micro-frameworks**. Leur minimalisme les rend idéaux pour s'initier en douceur au fonctionnement d'un framework PHP. C'est pourquoi nous allons baser notre application Web sur un micro-framework. L'un d'entre eux est *made in France* et basé sur les composants de Symfony, soit deux bonnes raisons de le choisir : c'est le micro-framework [Silex](http://silex.sensiolabs.org/).

## Premiers pas avec Silex

Intégrer un framework à une application nécessite de savoir l'utiliser. Si le fonctionnement de Silex et/ou du gestionnaire de dépendances [Composer](https://getcomposer.org/) vous sont inconnus, consultez le tutoriel [Premiers pas avec le framework PHP Silex](/tutoriel/premiers-pas-framework-php-silex/).

## Réécriture de l'application avec Silex

### Récupération de Silex via Composer

Afin de pouvoir récupérer les fichiers de Silex, créez dans le répertoire `MicroCMS` servi par votre serveur Web local. un fichier texte nommé `composer.json` ayant le contenu suivant.

    {
        "require": {
            "silex/silex": "~1.2"
        }
    }

Ouvrez une fenêtre de terminal et déplacez-vous dans le répertoire `MicroCMS`. Ensuite, lancez la commande ci-dessous :

    $ composer install

Si tout va bien, Composer va télécharger les fichiers de Silex dans un sous-répertoire nommé `vendor` du répertoire courant. L'arborescence du projet est maintenant la suivante.

{{% img microcms_arborescence_silex.png %}}

### Mise à jour de l'arborescence

Créez dans `MicroCMS` les sous-répertoires suivants :

* `app`, qui contiendra la configuration de l'application Silex ;
* `src`, qui contiendra les fichiers source PHP ;
* `views`, qui contiendra les vues de l'application ;
* `web`, qui contiendra les fichiers accessibles aux clients Web. 

Déplacez le fichier `view.php` dans le sous-répertoire `views`, puis déplacez le fichier `model.php` dans le sous-répertoire `src`. Déplacez ensuite les fichiers `index.php` et `microcms.css` dans le sous-répertoire `web`. Editez `index.php` et remplacez son contenu par le code source ci-dessous.

    <?php
    
    require_once __DIR__.'/../vendor/autoload.php';
    
    $app = new Silex\Application();
    
    require __DIR__.'/../app/routes.php';
    
    $app->run();

Ce fichier constitue le **contrôleur frontal** de notre application Web. Il centralise la gestion des requêtes HTTP entrantes. Dans ce fichier, on instancie l'objet Silex principal `$app` puis on inclut la définitions des routes de l'application (fichier `routes.php`).

Toujours dans `web`, créez un nouveau fichier texte nommé `.htaccess` contenant le texte ci-dessous. Ce fichier permet de rediriger toutes les requêtes entrantes vers `index.php`.

    # Redirect incoming URLs to index.php
    <IfModule mod_rewrite.c>
        Options -MultiViews

        RewriteEngine On
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteRule ^ index.php [QSA,L]
    </IfModule>

Dans le sous-répertoire `app`, créez maintenant le fichier `routes.php` avec le contenu ci-dessous.

    <?php
    
    // Return all articles
    $app->get('/', function () {
        require '../src/model.php';
        $articles = getArticles();
    
        ob_start();                  // start buffering HTML output
        require '../views/view.php';
        $view = ob_get_clean();      // assign HTML output to $view
        return $view;
    });

Silex permet de définir des **routes**, c'est-à-dire des points d'entrée dans l'application. A chaque route est associée une réponse construite par notre code. La route ci-dessus correspond à l'URL racine de l'application (`/`). La [fonction anonyme](http://php.net//manual/fr/functions.anonymous.php) associée à cette route utilise la fonction `getArticles` du modèle pour récupérer la liste des articles. 

Chaque route doit renvoyer explicitement une réponse. Les fonctions PHP [ob_start](http://php.net/manual/fr/function.ob-start.php) et [ob_get_clean](http://php.net/manual/fr/function.ob-get-clean.php) permettent de récupérer le résultat de l'appel à `require` (autrement dit la vue générée) dans une variable nommée `$view`. Cette variable est renvoyée à la fin de la fonction.

Voici l'arborescence obtenue après tous ces changements.

{{% img microcms_arborescence_silex_2.png %}}

### Définition d'un hôte virtuel

Enfin, il nous reste à configurer un **hôte virtuel** afin que l'application puisse répondre à une URL de la forme http://microcms. En suivant l'exemple donné dans le tutoriel [Premiers pas avec le framework PHP Silex](/tutoriel/premiers-pas-framework-php-silex/), éditez le fichier de configuration Appache `httpd-vhosts.conf` et ajoutez le contenu ci-dessous à la fin en adaptant les lignes commençant par `DocumentRoot`et `Directory` à votre configuration locale.

    <VirtualHost *:80>
        DocumentRoot "C:\xampp\htdocs\MicroCMS\web"
        ServerName microcms
        <Directory "C:\xampp\htdocs\MicroCMS\web">
            AllowOverride all
        </Directory>
    </VirtualHost>

Redémarrez le serveur Web Apache pour terminer la configuration de l'hôte virtuel. A ce stade, une requête HTTP vers http://microcms doit afficher correctement la liste des articles. 

{{% image src="microcms_articles_silex_1.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-03).

## Bilan

Nous avons refactorisé notre application Web pour intégrer le framework Silex et posé les bases d'une architecture robuste. Cependant, notre application profite encore peu des services que Silex peut fournir. Les prochaines itérations y remédieront.


# Itération 4 : refactorisation de l'accès aux données

Le but de cette itération est d'améliorer la partie Modèle de notre application Web.

## Modélisation objet du domaine

Actuellement, la partie Modèle de notre application Web est écrite de manière simpliste. Voici pour rappel le fichier source `model.php`.

    <?php
    
    // Return all articles
    function getArticles() {
        $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
        $articles = $bdd->query('select * from t_article order by art_id desc');
        return $articles;
    }

L'ajout futur de nouveaux services similaires risque de rendre la partie Modèle difficile à utiliser. Nous allons restructurer cette partie en introduisant une modélisation orientée objet des données métier. Pour l'instant, nos seules données métier sont les articles, qui se caractérisent par un identifiant, un titre et un contenu. Nous allons modéliser un article sous la forme d'une classe nommée `Article` dont voici le diagramme UML. 

{{% image src="microcms_uml_article.jpeg" class="centered" %}}

la classe `Article` est ce qu'on appelle parfois (sans peur du ridicule) un POPO, ou *Plain Old PHP Objet* par analogie avec les [POJO](http://fr.wikipedia.org/wiki/Plain_Old_Java_Object) du monde Java. Autrement dit, cette classe ne contient rien de complexe : uniquement les propriétés et accesseurs nécessaires pour représenter un article.

Ecrivons maintenant cette classe en PHP. Si vous n'avez jamais utilisé PHP de manière orientée objet, je vous conseille les tutoriels des sites [OpenClassrooms](http://fr.openclassrooms.com/informatique/cours/programmez-en-oriente-objet-en-php) (chapitres 1 et 2) et [Codecamedy](http://www.codecademy.com/fr/tracks/php).

    <?php
    
    namespace MicroCMS\Domain;
    
    class Article 
    {
        /**
         * Article id.
         *
         * @var integer
         */
        private $id;

        /**
         * Article title.
         *
         * @var string
         */
        private $title;

        /**
         * Article content.
         *
         * @var string
         */
        private $content;
    
        public function getId() {
            return $this->id;
        }
    
        public function setId($id) {
            $this->id = $id;
        }
    
        public function getTitle() {
            return $this->title;
        }
    
        public function setTitle($title) {
            $this->title = $title;
        }
    
        public function getContent() {
            return $this->content;
        }
    
        public function setContent($content) {
            $this->content = $content;
        }
    }

Vous aurez peut-être remarqué que cette classe est définie dans un **espace de noms** (instruction PHP `namespace` au début du fichier). En PHP comme dans les autres langages qui les supportent, un espace de noms permet d'éviter les conflits de nommage des éléments (exemple : deux classes portant le même nom) en regroupant ces éléments dans des espaces dédiés. Ainsi, le nom complet de notre classe `Article` est `MicroCMS\Domain\Article`. Pour plus d'informations sur les espaces de noms en PHP, consultez la [documentation du langage](http://php.net//manual/fr/language.namespaces.php) ou ce [tutoriel](http://fr.openclassrooms.com/informatique/cours/les-espaces-de-noms-en-php).

Afin de permettre un chargement automatisé de la classe `Article`, le fichier source `Article.php` associé doit se trouver dans le répertoire correspondant à son espace de noms. Créez dans le répertoire `src` du projet le sous-répertoire `MicroCMS`, puis le sous-répertoire `Domain` dans `MicroCMS`. Enfin, créez le fichier `Article.php` et copiez/collez-y le contenu ci-dessus.

{{% danger %}}
Veillez à bien respecter les distinctions majuscules/minuscules dans les noms des répertoires et des fichiers source.
{{% /danger %}}

## Remplacement de PDO par DBAL

Il faut maintenant transformer notre partie Modèle afin qu'elle renvoie une liste d'objets de la classe `Article`. Nous allons en profiter pour changer de technologie d'accès à la base de données en remplaçant PDO par [DBAL](http://www.doctrine-project.org/projects/dbal.html). 

Comme son nom l'indique, DBAL est une couche d'abstraction de base de données. Tout comme PDO, DBAL fournit des services de connexion et d'exécution de requêtes SQL indépendants du SGBDR utilisé : le même code pourra interagir avec MySQL, ORACLE ou encore PostgreSQL. Par rapport à PDO, DBAL fournit des services additionnels comme la gestion avancée des transactions et des types. Le remplacement de PDO par DBAL va également permettre d'illustrer le mécanisme d'ajout de services proposé par le framework Silex.

### Mise à jour de l'accès aux données

Ecrivons le nouveau code d'accès aux données utilisant DBAL. Nous allons continuer à utiliser la POO en définissant ce code dans la classe `ArticleDAO`.

    <?php
    
    namespace MicroCMS\DAO;
    
    use Doctrine\DBAL\Connection;
    use MicroCMS\Domain\Article;
    
    class ArticleDAO
    {
        /**
         * Database connection
         *
         * @var \Doctrine\DBAL\Connection
         */
        private $db;
    
        /**
         * Constructor
         *
         * @param \Doctrine\DBAL\Connection The database connection object
         */
        public function __construct(Connection $db) {
            $this->db = $db;
        }
    
        /**
         * Return a list of all articles, sorted by date (most recent first).
         *
         * @return array A list of all articles.
         */
        public function findAll() {
            $sql = "select * from t_article order by art_id desc";
            $result = $this->db->fetchAll($sql);
            
            // Convert query result to an array of Article objects
            $articles = array();
            foreach ($result as $row) {
                $articleId = $row['art_id'];
                $articles[$articleId] = $this->buildArticle($row);
            }
            return $articles;
        }
    
        /**
         * Creates an Article object based on a DB row.
         *
         * @param array $row The DB row containing Article data.
         * @return \MicroCMS\Domain\Article
         */
        private function buildArticle($row) {
            $article = new Article();
            $article->setId($row['art_id']);
            $article->setTitle($row['art_title']);
            $article->setContent($row['art_content']);
            return $article;
        }
    }

Cette classe est définie dans l'espace de noms `MicroCMS\DAO` et utilise (instruction PHP `use`) les classes `Doctrine\DBAL\Connection` et `MicroCMS\Domain\Article`. Elle mémorise l'objet de connexion à la BD dans sa propriété `$db`, définie par son constructeur. L'ancienne fonction `getArticles` est remplacée par la méthode `findAll` qui renvoie la liste de tous les articles sous forme d'objets de la classe `Article`. La classe `ArticleDAO` dispose également d'une méthode interne `buildArticle` qui instancie un objet de la classe `Article` à partir d'une ligne de résultat SQL.

L'acronyme DAO signifie *Data Access Object*, ou objet d'accès aux données. Il s'agit d'un modèle de conception (*design pattern*) qui propose de regrouper le code d'accès aux données d'une application dans des classes dédiées. C'est le cas de notre classe `ArticleDAO`.

Créez le fichier source `ArticleDAO.php` dans le répertoire `src/MicroCMS/DAO` (à créer) et ajoutez-lui le code source de la classe. Ensuite, supprimez le fichier `src/model.php` devenu inutile.

### Mise à jour de l'application

Plusieurs étapes sont à réaliser avant de pouvoir utiliser le nouveau code d'accès aux données.

Tout d'abord, il faut indiquer à Composer que notre projet dépend maintenant de DBAL. Modifiez le fichier `composer.json` comme indiqué ci-dessous.

    {
        "require": {
            "silex/silex": "~1.2",
            "doctrine/dbal": "~2.4"
        },
        "autoload": {
            "psr-0": {"MicroCMS": "src/"}
        }
    }

La nouvelle entrée `autoload` dans ce fichier permet d'ajouter notre propre code source, défini dans le répertoire `src`, au mécanisme de chargement automatique (*autoloading*) géré par Composer. Finies les instructions `require` partout dans le code ! Pour que cela fonctionne, il faut que notre code source respecte le standard [PSR-0](http://www.php-fig.org/psr/psr-0/) - c'est le cas ici.

Lancez ensuite la commande ci-dessous pour récupérer les fichiers du projet DBAL et mettre à jour le fichier `vendor/autoload.php` géré par Composer.

    $ composer update

Ensuite, créez dans le répertoire `app` du projet un nouveau fichier nommé `app.php`. Ce fichier va contenir le paramétrage de l'application Silex. Ajoutez dans ce fichier le code ci-dessous.

    <?php
    
    // Register global error and exception handlers
    use Symfony\Component\Debug\ErrorHandler;
    ErrorHandler::register();
    use Symfony\Component\Debug\ExceptionHandler;
    ExceptionHandler::register();
    
    // Register service providers.
    $app->register(new Silex\Provider\DoctrineServiceProvider());
    
    // Register services.
    $app['dao.article'] = $app->share(function ($app) {
        return new MicroCMS\DAO\ArticleDAO($app['db']);
    });

La première partie de ce fichier configure Silex pour gérer les erreurs PHP qui pourraient se produire pendant l'exécution de l'application. Cela permet d'obtenir des messages d'erreur explicites. Vous trouverez plus d'explications dans la [documentation du framework](http://silex.sensiolabs.org/doc/cookbook/error_handler.html).

La deuxième partie du fichier enregistre le [fournisseur de services](http://silex.sensiolabs.org/doc/providers.html) associé à DBAL, [DoctrineServiceProvider](http://silex.sensiolabs.org/doc/providers/doctrine.html).

Enfin, la troisième partie enregistre un nouveau [service](http://silex.sensiolabs.org/doc/services.html) nommé `dao.article` sous la forme d'une instance partagée de la classe `ArticleDAO`. Une fois le service enregistré, l'appel `$app['dao.article']` renverra cette instance.

{{% remark %}}
Le service `$app['db']` est défini automatiquement lors de l'enregistrement du fournisseur `DoctrineServiceProvider`.
{{% /remark %}}

Nous allons également améliorer la configuration de l'application. Pour cela, créez le fichier `prod.php` dans le sous-répertoire `app/config` du projet. Ce fichier contient les options de configuration liés à la mise en production de notre application. Ajoutez-lui le contenu ci-dessous.

    <?php
    
    // Doctrine (db)
    $app['db.options'] = array(
        'driver'   => 'pdo_mysql',
        'charset'  => 'utf8',
        'host'     => 'localhost',
        'port'     => '3306',
        'dbname'   => 'microcms',
        'user'     => 'microcms_user',
        'password' => 'secret',
    );

Il s'agit du paramétrage de la connexion à la base de données via DBAL.

Créez le fichier `dev.php` dans le sous-répertoire `app/config` du projet. Ce fichier contient les options de configuration liés au développement de notre application. Ajoutez-lui le contenu ci-dessous.

    <?php
    
    // include the prod configuration
    require __DIR__.'/prod.php';
    
    // enable the debug mode
    $app['debug'] = true;

Ce fichier inclut la configuration de production puis paramètre Silex pour afficher des informations de débogage détaillées en cas d'erreur, ce qui est utile pendant la phase de développement.

A présent, modifiez le fichier `routes.php` du répertoire `app` comme indiqué ci-dessous.

    <?php
    
    // Return all articles
    $app->get('/', function () use ($app) {
        $articles = $app['dao.article']->findAll();
    
        ob_start();                  // start buffering HTML output
        require '../views/view.php';
        $view = ob_get_clean();      // assign HTML output to $view
        return $view;
    });

L'appel à la fonction `getArticles` est remplacé par l'utilisation du service `dao.article` enregistré dans `app.php`. `$app['dao.article']` renvoie un objet de la classe `ArticleDAO`dont on utilise ensuite la méthode `findAll` pour récupérer la liste des articles.

La variable `$articles` utilisée dans ce fichier source contient à présent un tableau d'objets de la classe `Article`. Il faut donc modifier une partie de la vue `views/view.php` en conséquence.

    // ...
    <?php foreach ($articles as $article): ?>
        <article>
            <h2><?= $article->getTitle() ?></h2>
            <p><?= $article->getContent() ?></p>
        </article>
    <?php endforeach; ?>
    // ...

Chaque élément `$article` du tableau `$articles` est un objet de la classe `Article`, et non plus un tableau associatif. A l'intérieur de la boucle `foreach` qui parcourt la liste des articles, on utilise les méthodes `getTitle` et `getContent` de cette classe afin d'accéder aux données de l'article.

Il ne nous reste plus qu'à modifier le contrôleur frontal `web/index.php` afin d'inclure les fichiers de paramétrage de l'application.

    <?php
    
    require_once __DIR__.'/../vendor/autoload.php';
    
    $app = new Silex\Application();
    
    require __DIR__.'/../app/config/dev.php';
    require __DIR__.'/../app/app.php';
    require __DIR__.'/../app/routes.php';
    
    $app->run();

La structure de notre application est maintenant la suivante.

{{% img microcms_arborescence_dbal.png %}}

C'est le moment de tester notre refactorisation en accédant à l'URL http://microcms. Si tout va bien, le résultat affiché reste le même.

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-04).

## Bilan

Cette itération nous a permis d'introduire une modélisation orientée objet du domaine et de l'accès aux données. Au passage, nous avons découvert comment Silex facilite l'inclusion de nouveaux services dans une application Web. C'est l'un des avantages de l'utilisation d'un framework.

Dans cette itération, nous avons surtout travaillé dans les parties Modèle et Contrôleur de notre application. L'itération suivante va s'intéresser à la partie Vue.


# Itération 5 : refactorisation de la présentation

Le but de cette itération est d'améliorer la technologie d'affichage de notre application.

## Critique de l'application existante

La partie Présentation de notre application actuelle correspond au répertoire `views`, dans lequel on définit un fichier PHP/HTML par vue affichée. Voici pour mémoire le contenu du fichier `view.php` affichant la liste des articles.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8" />
        <link href="microcms.css" rel="stylesheet" />
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <header>
            <h1>MicroCMS</h1>
        </header>
        <?php foreach ($articles as $article): ?>
            <article>
                <h2><?= $article->getTitle() ?></h2>
                <p><?= $article->getContent() ?></p>
            </article>
        <?php endforeach; ?>
        <footer class="footer">
            <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
        </footer>
    </body>
    </html>

L'évolution de l'application va impliquer l'écriture de nouvelles vues (détails sur un article, formulaire de connexion, etc). Toutes les vues auront cependant des éléments communs (partie `<head>`, pied de page, etc). On aimerait pouvoir définir un squelette de vue commun et ne définir dans chaque vue que ses éléments spécifiques.

Un autre problème de notre application tient à la sécurité. Actuellement, notre vue n'est pas protégée contre les [injections de code](http://fr.wikipedia.org/wiki/Injection_de_code_dans_les_applications_web) sur la page HTML générée. Ici, si `$article->getTitle()` contient un code malicieux (par exemple du JavaScript), la page HTML générée par cette vue exécutera ce code JavaScript non désiré.

Le mécanisme standard de défense contre les injections de code dans du HTML consiste à **échapper** (*escape*) toutes les données dynamiques incluses dans le code HTML. La technique classique est de faire appel à la fonction PHP [htmlspecialchars](http://php.net//manual/fr/function.htmlspecialchars.php) qui transforme certains caractères tels que `<` ou `>`, ce qui désactive l'interprétation des balises comme `<script>`. Silex fournit ce mécanisme sous la forme de la méthode [escape](http://silex.sensiolabs.org/api/Silex/Application.html#method_escape). Cependant, il est fastidieux d'échapper systématiquement toutes les variables PHP dans toutes nos vues.

Afin de remédier à toutes ces limitations, nous allons utiliser une solution plus moderne en intégrant à notre application un moteur de *templates*.

## Choix du moteur de templates

Un **moteur de templates** est un logiciel spécialisé dans la générations de vues. Un *template* (que l'on peut traduire par "gabarit") est un fichier texte contenant des instructions spécifiques (variables, structures de contrôle, etc). Lorsqu'un template est généré, les instructions spécifiques qu'il contient sont exécutées par le moteur pour aboutir au résultat désiré.

Quelque part, PHP est en lui-même un moteur de templates. Cependant, un moteur de templates dédié comme celui que nous allons utiliser fournit une syntaxe plus claire et des services plus avancés.

Il existe plusieurs moteurs de templates PHP, comme par exemple [Smarty](http://www.smarty.net/). Notre choix va se porter sur le moteur standard de Silex et de Symfony : [Twig](http://twig.sensiolabs.org/).

La prise en main de Twig n'est pas très difficile. Si vous souhaitez des informations détaillées, consultez sa [documentation](http://twig.sensiolabs.org/doc/templates.html) ou encore ce [tutoriel](http://fr.openclassrooms.com/informatique/cours/utilisation-de-twig-un-moteur-de-templates).

## Intégration de Twig

L'intégration de Twig est facilitée par l'existence d'un fournisseur de services pour Silex. Nous allons donc employer la même technique que pour DBAL à l'itération précédente.

Commençons par définir une dépendance de notre projet envers Twig dans le fichier `composer.json`. 

    {
        "require": {
            "silex/silex": "~1.2",
            "doctrine/dbal": "~2.4",
            "twig/twig": "~1.16"
        },
        "autoload": {
            "psr-0": {"MicroCMS": "src/"}
        }
    }

Mettez ensuite à jour les dépendances en tapant la ligne ci-dessous dans un terminal.

    $ composer update

Ensuite, éditez le fichier `app/app.php` pour y ajouter l'enregistrement de Twig auprès de Silex.

    // ...

    // Register service providers.
    $app->register(new Silex\Provider\DoctrineServiceProvider());
    $app->register(new Silex\Provider\TwigServiceProvider(), array(
        'twig.path' => __DIR__.'/../views',
    ));

    // ...

Ici, Twig est configuré pour que le répertoire dans lequel nous stockerons nos templates soit le répertoire `views` du projet.

{{% remark %}}
Le service `$app['twig']` est défini automatiquement lors de l'enregistrement du fournisseur `TwigServiceProvider`.
{{% /remark %}}

A présent, remplaçons la vue `views/view.php` par un template Twig pour afficher la liste des articles. Dans le répertoire `views`, créez le fichier `index.html.twig` avec le contenu ci-dessous.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8" />
        <link href="microcms.css" rel="stylesheet" />
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <header>
            <h1>MicroCMS</h1>
        </header>
        {% autoescape %}
        {% for article in articles %}
            <article>
                <h2>{{ article.title }}</h2>
                <p>{{ article.content }}</p>
            </article>
        {% endfor %}
        {% endautoescape %}
        <footer class="footer">
            <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
        </footer>
    </body>
    </html>

Comme vous le constatez, la syntaxe de Twig est assez proche de celle du PHP : 

* la boucle `for` permet de parcourir le tableau `$articles` ;
* l'instruction `article.title` fait appel à la méthode `getTitle` de l'objet `$article` ([plus de précisions](http://twig.sensiolabs.org/doc/templates.html#variables)) ;
* les instructions `{% autoescape %}` et `{% endautoescape %}` délimitent un bloc de code dans lequel l'échappement des variables dynamiques est réalisé automatiquement.

Vous pouvez maintenant supprimer le fichier `views/view.php` devenu inutile.

Enfin, on modifie la route Silex dans le fichier `app/routes.php` pour générer la nouvelle vue.

    <?php

    // Return all articles
    $app->get('/', function () use ($app) {
        $articles = $app['dao.article']->findAll();
        return $app['twig']->render('index.html.twig', array('articles' => $articles));
    });

Ici, on demande au service Twig (`$app['twig']`) de générer le template `index.html.twig` en lui passant ses données dynamiques en paramètre. Ici, la seule donnée dynamique est une variable nommée `articles` qui contient le tableau d'objets de la classe `Article` renvoyé par la partie Modèle.

Il est temps de vérifier l'intégration de Twig en accédant à http://microcms. Même si la technologie utilisée a changé, la liste des articles s'affiche exactement comme précédemment.

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-05).

## Bilan

la partie Présentation de notre application Web est maintenant gérée par le moteur de remplates Twig. Cependant, le rendu utilisateur n'a pas évolué depuis l'initialisation de l'application et il reste sommaire. La prochaine itération va améliorer cela.


# Itération 6 : amélioration de la présentation

Le but de cette itération est de rendre l'affichage de notre application plus conforme aux standards actuels.

## Introduction au design Web adaptatif

Commençons avec une image qui vaut mieux qu'un long discours.

{{% img this_is_the_web.png %}}

De nos jours, un site Web a plus de chances d'être consulté depuis un terminal mobile (*smartphone*, tablette, etc) que depuis un classique poste fixe. Cette (r)évolution doit absolument est prise en compte pour qu'un utilisateur de terminal mobile puisse consulter et utiliser le site dans de bonnes conditions.

Il existe plusieurs réponses complémentaires à cette problématique, comme par exemple la création d'une version mobile d'un site ou encore le développement d'applications dédiées à chaque écosystème mobile (iOS, Android, Windows Phone...). La solution la moins coûteuse consiste à adapter l'affichage en détectant les caractéristiques du terminal client. C'est ce qu'on appelle le **design Web adaptatif**, traduction de l'anglais *responsive (Web) design*. Pour une introduction générale à ce concept, consultez [Wikipedia](http://fr.wikipedia.org/wiki/Site_web_adaptatif).

Il existe plusieurs manières d'obtenir un design Web adaptatif. On peut le réaliser "à la main" en utilisant des [media queries](http://www.alsacreations.com/article/lire/930-css3-media-queries.html) (fournies par la norme CSS3) pour adapter la mise en page à l'environnement détecté. il existe également des frameworks qui facilitent la mise en page adaptative. Nous allons utiliser le plus populaire d'entre eux : [Bootstrap](http://getbootstrap.com/).

## Premiers pas avec Bootstrap

Pour une introduction générale au fonctionnement de Bootstrap, consultez le tutoriel [Premiers pas avec le framework Bootstrap](/tutoriel/premiers-pas-framework-bootstrap/).

## Installation de Bootstrap et de jQuery

Les fichiers de Bootstrap sont nécessaires au navigateur client pour afficher les pages HTML de notre application. Nous allons donc les installer dans le répertoire `web`. Dans ce répertoire, créez un sous-répertoire `lib` puis un sous-répertoire `bootstrap` dans `lib`. Téléchargez Bootstrap sur [cette page](http://getbootstrap.com/getting-started/#download) puis décompressez le contenu de l'archive dans le répertoire `bootstrap`. 

Pour fonctionner totalement, Bootstrap nécessite l'inclusion de la librairie JavaScript [jQuery](http://jquery.com/). Créez dans le répertoire `web/lib` un sous-répertoire `jquery`. Ensuite, téléchargez la version "production" de jQuery sur [cette page](http://jquery.com/download/) puis copiez le fichier JavaScript téléchargé dans le répertoire `jquery`.

Afin de clarifier l'organisation de `web`, créez dans ce répertoire un sous-répertoire `css` puis déplacez-y le fichier `microcms.css`.

Vous devez obtenir dans `web` une arborescence de la forme suivante.

{{% img microcms_arborescence_bootstrap.png %}}

## Réécriture de la vue avec Bootstrap

Nous allons modifier la vue `index.html.twig` pour y intégrer Bootstrap. Au passage, nous allons en profiter pour ajouter à l'application une barre de navigation fixée en haut de la fenêtre. Voici son nouveau code source.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="{{ app.request.basepath }}/lib/bootstrap/css/bootstrap.min.css" rel="stylesheet">
        <link href="{{ app.request.basepath }}/css/microcms.css" rel="stylesheet">
        <title>MicroCMS - Home</title>
    </head>
    <body>
        <div class="container">
            <nav class="navbar navbar-default navbar-fixed-top navbar-inverse" role="navigation">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#navbar-collapse-target">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                        <a class="navbar-brand" href="/">MicroCMS</a>
                    </div>
                    <div class="collapse navbar-collapse" id="navbar-collapse-target">
                    </div>
                </div><!-- /.container -->
            </nav>
            {% autoescape %}
            {% for article in articles %}
                <article>
                    <h2>{{ article.title }}</h2>
                    <p>{{ article.content }}</p>
                </article>
            {% endfor %}
            {% endautoescape %}
            <footer class="footer">
                <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
            </footer>
        </div>
    </body>
    </html>

Dans la partie `<head>` de cette page, nous avons ajouté les liens vers les feuilles de style de l'application et de Boostrap en préfixant ces liens par la variable `app.request.basepath` de Silex. Cela permet de gérer tous les scenarii possibles de déploiement de l'application ([plus de détails](http://silex.sensiolabs.org/doc/cookbook/assets.html)).

Dans le corps de cette page, nous avons introduit une barre de navigation (`navbar`) fixée en haut de la fenêtre (`navbar-fixed-top`). Tous les éléments du corps sont inclus dans un conteneur Boostrap (`container`).

Le fait de fixer la barre de navigation en haut de la fenêtre nécessite de décaler la balise `<body>`. Il faut donc modifier la feuille style `microcms.css` ainsi :

    body { 
        padding-top: 40px; 
    }
    
    .footer {
        border-top: 1px solid #ccc;
        padding-top: 10px;
        text-align: center;
    }

Accédez à l'URL http://microcms depuis votre navigateur Web. Vous obtenez à présent un résultat plus flatteur.

{{% image src="microcms_articles_bootstrap.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-06).

## Bilan

Grâce à l'intégration de Bootstrap, les vues gérant l'affichage de notre application ont un aspect plus actuel et peuvent être écrites de manière adaptative. Leur rendu sera optimal quel que soit le terminal client utilisé.

Cette itération et les précédentes ont consisté en des améliorations techniques de l'application. La prochaine itération va (enfin !) lui ajouter une nouvelle fonctionnalité métier.


# Itération 7 : affichage des détails sur un article

Le but de cette itération est de permettre au visiteur de consulter les détails sur un article en cliquant sur son titre.

## Mise à jour de la base de données

Notre base de données actuelle doit évoluer pour intégrer le stockage des commentaires sur les articles. Un commentaire se caractérise par son identifiant, son auteur, son contenu ainsi que l'article auquel il se rapporte.

L'un de nos récits utilisateur ("En tant qu'utilisateur connecté, je peux ajouter un commentaire à un article") implique que l'auteur d'un commentaire soit un utilisateur enregistré. Au cours de cette itération, nous allons gérer l'auteur comme une simple chaîne. On crée donc une table `t_comment` pour stocker les commentaires, en lui ajoutant les champs requis ainsi qu'une clé étrangère vers la table `t_article`. On aboutit au contenu ci-dessous pour le fichier `db/structure.sql`.

    create database if not exists microcms character set utf8 collate utf8_unicode_ci;
    use microcms;
    
    grant all privileges on microcms.* to 'microcms_user'@'localhost' identified by 'secret';
    
    drop table if exists t_comment;
    drop table if exists t_article;
    
    create table t_article (
        art_id integer not null primary key auto_increment,
        art_title varchar(100) not null,
        art_content varchar(2000) not null
    ) engine=innodb character set utf8 collate utf8_unicode_ci;
    
    create table t_comment (
        com_id integer not null primary key auto_increment,
        com_author varchar(100) not null,
        com_content varchar(500) not null,
        art_id integer not null,
        constraint fk_com_art foreign key(art_id) references t_article(art_id)
    ) engine=innodb character set utf8 collate utf8_unicode_ci;

On enrichit le jeu de données de test de l'application avec quelques commentaires.

    # ...

    insert into t_comment(art_id, com_author, com_content) values
    (1, 'John Doe', 'Great! Keep up the good work.');
    insert into t_comment(art_id, com_author, com_content) values
    (1, 'Ann Yone', "Thank you, I'll try my best.");

Mettez à jour les scripts SQL `db/structure.sql` et `db/content.sql` pour ajouter les éléments ci-dessus, puis exécutez-les dans cet ordre afin de mettre votre base de données à jour.

## Mise à jour de l'application

### Partie Modèle

En respectant les choix de design effectués dans une itération précédente, on modélise un commentaire sous la forme d'une classe `Commentaire` dans l'espace de noms `MicroCMS\Domain`. Voici le diagramme UML associé.

    {{% image src="microcms_uml_article_comment.jpeg" class="centered" %}}

Ce diagramme modélise l'association entre un article et ses commentaires.

Créez le fichier source `Comment.php` dans le répertoire `src/MicroCMS/Domain`, puis ajoutez-y le code source de la classe `Comment`.

    <?php
    
    namespace MicroCMS\Domain;
    
    class Comment 
    {
        /**
         * Comment id.
         *
         * @var integer
         */
        private $id;
    
        /**
         * Comment author.
         *
         * @var string
         */
        private $author;
    
        /**
         * Comment content.
         *
         * @var integer
         */
        private $content;
    
        /**
         * Associated article.
         *
         * @var \MicroCMS\Domain\Article
         */
        private $article;
    
        public function getId() {
            return $this->id;
        }
    
        public function setId($id) {
            $this->id = $id;
        }
    
        public function getAuthor() {
            return $this->author;
        }
    
        public function setAuthor($author) {
            $this->author = $author;
        }
    
        public function getContent() {
            return $this->content;
        }
    
        public function setContent($content) {
            $this->content = $content;
        }
    
        public function getArticle() {
            return $this->article;
        }
    
        public function setArticle($article) {
            $this->article = $article;
        }
    }

L'association avec un article se traduit dans le code source par la présence d'une propriété `article`. Il ne s'agit pas d'un simple identifiant de type entier, mais bien d'un objet de la classe `Article`.

A présent, il faut créer la classe d'accès aux données pour les commentaires. Cette classe doit permettre de récupérer la liste des commentaires associés à un article donné. Elle est logiquement nommée `CommentDAO` et se trouve dans l'espace de noms `MicroCMS\DAO`. Voici une première version de cette classe.

    <?php
    
    namespace MicroCMS\DAO;
    
    use Doctrine\DBAL\Connection;
    use MicroCMS\Domain\Comment;
    
    class CommentDAO
    {
        /**
         * Database connection
         *
         * @var \Doctrine\DBAL\Connection
         */
        private $db;
    
        /**
         * Constructor
         *
         * @param \Doctrine\DBAL\Connection The database connection object
         */
        public function __construct(Connection $db) {
            $this->db = $db;
        }
    
        /**
         * Return a list of all comments for an article, sorted by date (most recent first).
         *
         * @param $articleId The article id.
         *
         * @return array A list of all comments for the article.
         */
        public function findAllByArticle($articleId) {
            // ...
        }
    
        /**
         * Creates an Comment object based on a DB row.
         *
         * @param array $row The DB row containing Comment data.
         * @return \MicroCMS\Domain\Comment
         */
        private function buildComment($row) {
            // ...
        }
    }

On peut remarquer que la propriété `$db` ainsi que le constructeur sont exactement les mêmes que dans la classe `ArticleDAO`. Il s'agit d'une **duplication de code**.

{{% tip %}}
La duplication de code est l'ennemie du bon développeur, et l'un des symptômes d'un design perfectible. 
{{% /tip %}}

Nous allons profiter de cette itération pour refactoriser le code d'accès aux données afin de supprimer cette duplication de code. Commençons par identifier les besoins communs à toutes les classes d'accès aux données :

* la connexion à la base (propriété `$db`) ;
* la construction d'un objet du domaine à partir d'une ligne de résultat SQL (méthodes `buildArticle` et `buildComment`).

Nous factorisons ces besoin communs au sein d'une classe abstraite `DAO` dont **hériteront** toutes nos classes d'accès aux données. Si vous avez besoin de détails sur le concept d'héritage, consultez ce [cours](/cours/principaux-concepts-objet/). Voici le code source de la classe `DAO`.

    <?php
    
    namespace MicroCMS\DAO;
    
    use Doctrine\DBAL\Connection;
    
    abstract class DAO 
    {
        /**
         * Database connection
         *
         * @var \Doctrine\DBAL\Connection
         */
        private $db;
    
        /**
         * Constructor
         *
         * @param \Doctrine\DBAL\Connection The database connection object
         */
        public function __construct(Connection $db) {
            $this->db = $db;
        }
    
        /**
         * Grants access to the database connection object
         *
         * @return \Doctrine\DBAL\Connection The database connection object
         */
        protected function getDb() {
            return $this->db;
        }
    
        /**
         * Builds a domain object from a DB row.
         * Must be overridden by child classes.
         */
        protected abstract function buildDomainObject($row);
    }

La connexion à la base de données est encapsulée sous la forme d'une propriété privée `$db` et d'un accesseur protégé (donc accessible uniquement aux classes dérivées) `getDb`. La construction d'un objet du domaine est spécifique à chaque entité métier : on factorise donc uniquement la déclaration de ce service (méthode protégée `buildDomainObject`). Chaque classe d'accès aux données devra **redéfinir** cette méthode pour consstruire un objet du domaine particulier.

Créez le fichier source `DAO.php` dans le répertoire `src/MicroCMS/DAO`, puis ajoutez-y le code source de la classe `DAO`.

L'existence de la classe abstraite `DAO` nous permet de modifier la définition de la classe `ArticleDAO` comme indiqué ci-dessous.

    <?php
    
    namespace MicroCMS\DAO;
    
    use MicroCMS\Domain\Article;
    
    class ArticleDAO extends DAO
    {
        /**
         * Return a list of all articles, sorted by date (most recent first).
         *
         * @return array A list of all articles.
         */
        public function findAll() {
            $sql = "select * from t_article order by art_id desc";
            $result = $this->getDb()->fetchAll($sql);
            
            // Convert query result to an array of Article objects
            $articles = array();
            foreach ($result as $row) {
                $articleId = $row['art_id'];
                $articles[$articleId] = $this->buildDomainObject($row);
            }
            return $articles;
        }
    
        /**
         * Creates an Article object based on a DB row.
         *
         * @param array $row The DB row containing Article data.
         * @return \MicroCMS\Domain\Article
         */
        protected function buildDomainObject($row) {
            $article = new Article();
            $article->setId($row['art_id']);
            $article->setTitle($row['art_title']);
            $article->setContent($row['art_content']);
            return $article;
        }
    }

La classe `ArticleDAO` hérite (mot-clé `extends`) de la classe abstraite `DAO`. L'utilisation directe de la propriété `$db` est remplacée par l'appel de la méthode `getDb` définie dans `DAO`. La méthode `buildArticle` est remplacée par la méthode redéfinie `buildDomainObject`.

{{% remark %}}
Nous aurions pu aller plus loin dans le redesign en factorisant dans la classe `DAO` la construction d'un objet du domaine générique. Cela aurait complexifié l'architecture au-delà du niveau de ce tutoriel.
{{% /remark %}}

Voici maintenant le code source de la classe `CommentDAO`.

    <?php
    
    namespace MicroCMS\DAO;
    
    use MicroCMS\Domain\Comment;
    
    class CommentDAO extends DAO 
    {
        /**
         * @var \MicroCMS\DAO\ArticleDAO
         */
        protected $articleDAO;
    
        public function setArticleDAO($articleDAO) {
            $this->articleDAO = $articleDAO;
        }
    
        /**
         * Return a list of all comments for an article, sorted by date (most recent first).
         *
         * @param $articleId The article id.
         *
         * @return array A list of all comments for the article.
         */
        public function findAllByArticle($articleId) {
            $sql = "select * from t_comment where art_id=? order by com_id";
            $result = $this->getDb()->fetchAll($sql, array($articleId));
            
            // Convert query result to an array of Comment objects
            $comments = array();
            foreach ($result as $row) {
                $comId = $row['com_id'];
                $comments[$comId] = $this->buildDomainObject($row);
            }
            return $comments;
        }
    
        /**
         * Creates an Comment object based on a DB row.
         *
         * @param array $row The DB row containing Comment data.
         * @return \MicroCMS\Domain\Comment
         */
        protected function buildDomainObject($row) {
            // Find the associated article
            $articleId = $row['art_id'];
            $article = $this->articleDAO->find($articleId);
    
            $comment = new Comment();
            $comment->setId($row['com_id']);
            $comment->setAuthor($row['com_author']);
            $comment->setContent($row['com_content']);
            $comment->setArticle($article);
            return $comment;
        }
    }

Afin de pouvoir construire complètement une instance de la classe `Comment`, la classe `CommentDAO` doit pouvoir récupérer un article à partir de son identifiant et construire une instance de la classe `Article`. Plutôt que d'ajouter cela dans le code source de `CommentDAO`, on ajoute dans la classe `ArticleDAO` une nouvelle méthode `find` définissant le service requis. La classe `CommentDAO` a besoin de la classe `ArticleDAO` pour fonctionner : on dit qu'il existe une **dépendance** entre la classe `CommentDAO` et la classe `ArticleDAO`. Cette dépendance se traduit dans le code source de `CommentDAO` par la présence d'une propriété privée `articleDAO` et d'un accesseur en écriture (mutateur) `setArticleDAO`. 

Créez le fichier source `CommentDAO.php` dans le répertoire `src/MicroCMS/DAO` et ajoutez-y le code de la classe `CommentDAO`. Ensuite, ajoutez au fichier `ArticleDAO.php` la méthode `find` ci-dessous.

    <?php
    
    // ...
    
    class ArticleDAO extends DAO
    {
        // ...

        /**
         * Returns an article matching the supplied id.
         *
         * @param integer $id
         *
         * @return \MicroCMS\Domain\Article|throws an exception if no matching article is found
         */
        public function find($id) {
            $sql = "select * from t_article where art_id=?";
            $row = $this->getDb()->fetchAssoc($sql, array($id));
    
            if ($row)
                return $this->buildDomainObject($row);
            else
                throw new \Exception("No article matching id " . $id);
        }

        // ...
    }

Notre refactorisation de la partie Modèle est maintenant terminée. 

### Partie Vue

L'évolution de cette partie consiste à ajouter une vue affichant les détails sur un article : titre, contenu et liste des commentaires. Cela se traduit par l'ajout d'un nouveau template `article.html.twig` dans le répertoire `views`. Voici une première version de ce nouveau template.

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="{{ app.request.basepath }}/lib/bootstrap/css/bootstrap.min.css" rel="stylesheet">
        <link href="{{ app.request.basepath }}/css/microcms.css" rel="stylesheet">
        
        <title>MicroCMS - {{ article.title }}</title>
    </head>
    <body>
        <div class="container">
            <nav class="navbar navbar-default navbar-fixed-top navbar-inverse" role="navigation">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#navbar-collapse-target">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                        <a class="navbar-brand" href="/">MicroCMS</a>
                    </div>
                    <div class="collapse navbar-collapse" id="navbar-collapse-target">
                    </div>
                </div><!-- /.container -->
            </nav>
            {% autoescape %}
            <p>
                <h2>{{ article.title }}</h2>
                <p>{{ article.content }}</p>
                <h3>Comments</h3>
                {% if comments %}
                    {% for comment in comments %}
                        <strong>{{ comment.author }}</strong> said : {{ comment.content }}<br>
                    {% endfor %}
                {% else %}
                    No comments yet.
                {% endif %}
            </p>
            {% endautoescape %}
            <footer class="footer">
                <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
            </footer>
        </div>
    </body>
    </html>

Ce template utilise les structures de contrôle Twig `if/else` et `for` afin d'afficher la liste des commentaires.

Le template existant `index.html.twig` et le nouveau template `article.html.twig` partagent de nombreux éléments : partie `<head>`, barre de navigation, pied de page... Pour éviter la duplication de code, on aimerait centraliser la définition de ces éléments et les inclure dans nos templates.

Le moteur de templates Twig permet de faire encore mieux : il supporte le mécanisme [d'héritage de templates](http://twig.sensiolabs.org/doc/templates.html#template-inheritance). Cela permet de définir un template de base contenant les éléments communs, puis de créer chaque template spécifique par **héritage** du template commun.

Créez dans le répertoire `views` un fichier texte `layout.html.twig` qui sera notre template commun :

    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="{{ app.request.basepath }}/lib/bootstrap/css/bootstrap.min.css" rel="stylesheet">
        <link href="{{ app.request.basepath }}/css/microcms.css" rel="stylesheet">
        <title>MicroCMS - {% block title %}{% endblock %}</title>
    </head>
    <body>
        <div class="container">
            <nav class="navbar navbar-default navbar-fixed-top navbar-inverse" role="navigation">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#navbar-collapse-target">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                        <a class="navbar-brand" href="/">MicroCMS</a>
                    </div>
                    <div class="collapse navbar-collapse" id="navbar-collapse-target">
                    </div>
                </div><!-- /.container -->
            </nav>
            {% autoescape %}
            <div id="content">{% block content %}{% endblock %}</div>
            {% endautoescape %}
            <footer class="footer">
                <a href="https://github.com/bpesquet/MicroCMS">MicroCMS</a> is a minimalistic CMS built as a showcase for modern PHP development.
            </footer>
        </div>
    </body>
    </html>

Ce template définit deux blocs, appelés `title` et `content`. Les templates dérivés redéfinissent ces blocs afin d'ajouter les parties spécifiques de chaque vue. Voici la nouvelle définition du fichier `index.html.twig` qui affiche la liste des articles.

    {% extends "layout.html.twig" %}
    
    {% block title %}Home{% endblock %}
    
    {% block content %}
    {% for article in articles %}
        <article>
            <a class="articleTitle" href="/article/{{ article.id }}"><h2>{{ article.title }}</h2></a>
            <p>{{ article.content }}</p>
        </article>
    {% endfor %}
    {% endblock %}

On constate l'utilisation du mot-clé `extends` pour indiquer que `index.html.twig`hérite du template commun `layout.html.twig`. Le reste du template définit les valeurs des blocs `title` et `content`. Un lien (balise `<a>`) ajouté au titre de chaque article renvoie vers une URL du type `/article/<identifiant de l'article>`. Voici le code HTML généré avec notre jeu de données de tests.

    <!-- ... --> 
    <article>
        <a class="articleTitle" href="/article/3"><h2>Lorem ipsum in french</h2></a>
        <p>...</p>
    </article>
    <article>
        <a class="articleTitle" href="/article/2"><h2>Lorem ipsum</h2></a>
        <p>...</p>
    </article>
    <article>
        <a class="articleTitle" href="/article/1"><h2>First article</h2></a>
        <p>Hi there! This is the very first article.</p>
    </article>
    <!-- ... -->

Le template `article.html.twig` suit le même modèle.

    {% extends "layout.html.twig" %}
    
    {% block title %}{{ article.title }}{% endblock %}
    
    {% block content %}
    <p>
        <h2>{{ article.title }}</h2>
        <p>{{ article.content }}</p>
        <h3>Comments</h3>
        {% if comments %}
            {% for comment in comments %}
                <strong>{{ comment.author }}</strong> said : {{ comment.content }}<br>
            {% endfor %}
        {% else %}
            No comments yet.
        {% endif %}
    </p>
    {% endblock %}

La dernière modification de la partie Vue consiste à enrichir légèrement la feuille de style `web/css/microcms.css` pour améliorer la présentation des titres d'article cliquables.

    /* ... */

    .articleTitle:hover, .articleTitle:focus {
        text-decoration: none;
    }

### Partie Contrôleur

la partie Contrôleur de notre application fait le lien entre le Modèle et la Vue. On commence par mettre à jour le fichier `app/app.php` afin d'enregistrer le nouveau service d'accès aux commentaires.

    // ...

    // Register services.
    $app['dao.article'] = $app->share(function ($app) {
        return new MicroCMS\DAO\ArticleDAO($app['db']);
    });
    $app['dao.comment'] = $app->share(function ($app) {
        $commentDAO = new MicroCMS\DAO\CommentDAO($app['db']);
        $commentDAO->setArticleDAO($app['dao.article']);
        return $commentDAO;
    });

C'est dans ce fichier que la dépendance envers la classe `ArticleDAO` est **injectée** à l'instance de `CommentDAO` grâce au mutateur `setArticleDAO`.

Enfin, on fait évoluer le fichier `app/routes.php` afin d'ajouter une nouvelle route.

    <?php
    
    // Returns all articles
    $app->get('/', function () use ($app) {
        $articles = $app['dao.article']->findAll();
        return $app['twig']->render('index.html.twig', array('articles' => $articles));
    });
    
    // Returns detailed info about an article
    $app->get('/article/{id}', function ($id) use ($app) {
        $article = $app['dao.article']->find($id);
        $comments = $app['dao.comment']->findAllByArticle($id);
        return $app['twig']->render('article.html.twig', array('article' => $article, 'comments' => $comments));
    });

La nouvelle route génère le template `article.html.twig` en lui passant en paramètres les données nécessaires, récupérées depuis les services de la partie Modèle : l'article identifié par le paramètre `$id` présent dans l'URL et la liste des commentaires associés à cet article.

Cette longue itération touche à sa fin et il est temps de tester l'application. Ouvrez l'URL http://microcms pour afficher la liste des articles, puis cliquez sur le titre de l'article du bas. Vous devriez obtenir l'affichage de ses détails.

{{% image src="microcms_article_comments.png" class="centered" %}}

Si vous cliquez sur le titre d'un article sans aucun commentaire, vous obtenez un résultat de la forme suivante.

{{% image src="microcms_article_nocomments.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-07).

## Bilan

Au cours de cette itération, nous avons ajouté à l'application une fonctionnalité métier en nous appuyant sur les bases définies précédemment. Nous avons également saisi les occasions de refactoriser l'architecture afin qu'elle s'adapte aux nouveaux besoins.

Afin de réaliser de nouvelles fonctionnalités métier, l'itération suivante va s'intéresser à la sécurisation de l'application. 

# Itération 8 : gestion de la sécurité

Le but de cette itération est d'offrir aux visiteurs la possibilité de s'identifier afin d'être reconnus par l'application.

## Contexte métier

Nous souhaitons ajouter à notre CMS une fonctionnalité d'ajout de commentaires à un article. Cependant, cet ajout ne doit être possible que pour les utilisateurs enregistrés dans l'application. Tout commentaire sera associé à son auteur, qui est nécessairement un utilisateur enregistré.

Afin de pouvoir réaliser cette fonctionnalité, il est nécessaire de sécuriser notre application Web. Pour cela, nous allons tirer parti des possibilités du framework Silex, reprises de celles de son grand frère Symfony.

## Symfony et la sécurité

La sécurisation est un besoin récurrent des applications Web. Comme tous les frameworks majeurs, Symfony dispose de fonctionnalités avancées dans ce domaine. Ce paragraphe en fait un bref résumé. Pour plus de détails sur la sécurité avec Symfony/Silex, consultez les rubriques associées des documentations de [Symfony](http://symfony.com/doc/current/book/security.html) et de [Silex](http://silex.sensiolabs.org/doc/providers/security.html).

Symfony envisage la sécurité comme un processus en deux étapes :

1. L'**authentification**. Durant cette étape, l'utilisateur s'identifie auprès de l'application. Celle-ci tente ensuite de le reconnaître.
2. L'**autorisation**. Ici, l'application détermine si l'utilisateur reconnu a accès à la ressource qu'il demande.

{{% image src="security_authentication_authorization.png" class="centered" %}}

Symfony permet de sécuriser les ressources d'une application Web en définissant un **pare-feu** (*firewall*). Lorsqu'un utilisateur fait une requête à une URL qui est protégée par un pare-feu, le système de sécurité de Symfony est activé. Le rôle du pare-feu est de déterminer si un utilisateur doit ou ne doit pas être authentifié (selon sa configuration, un pare-feu peut autoriser ou non les utilisateurs anonymes), et s'il doit l'être, de retourner une réponse à l'utilisateur afin d'entamer le processus d'authentification. Cette authentification peut prendre différentes formes : saisie d'un couple login/mot de passe dans un formulaire Web (la plus courante), certificat, etc.

{{% image src="security_anonymous_user_access.png" class="centered" %}}

L'autorisation se base sur l'attribution de **rôles** aux utilisateurs reconnus. Dans la configuration du pare-feu, on peut soumettre l'accès à certaines ressources à la possession par l'utilisateur du rôle associé.

{{% image src="security_ryan_no_role_admin_access.png" class="centered" %}}

## Gestion des mots de passe

La forme la plus courante d'authentification, celle que nous allons adopter, consiste à attribuer à chaque utilisateur un login et un mot de passe. Ces identifiants (*credentials*) permettent à l'application de reconnaître l'utilisateur.

Comme l'actualité nous le rappelle souvent, la gestion des mots de passe revêt une importante critique. Il est essentiel qu'une application Web stocke et manipule ses mots de passe sous forme cryptée et non directement "en clair". Les mots de passe de nos utilisateurs seront donc stockés après application d'un [algorithme de hachage cryptographique](http://fr.wikipedia.org/wiki/Fonction_de_hachage) (*digest*). Par exemple, le mot `Baptiste` donne le résultat `04ce34a463c52d41c4d0c04c9afd0abe` après application de l'algorithme de hachage [MD5](http://fr.wikipedia.org/wiki/MD5). Le résultat d'un eopération de hachage est appelée empreinte.

{{% image src="Hash_function_fr.svg.png" class="centered" %}}

Les algorithmes de hachage ont la particularité d'être unidirectionnels : il n'existe pas de moyen de revenir de l'empreinte obtenue au mot de passe en clair initial. Le mot de passe saisi par un utilisateur sera immédiatement haché avec le même algorithme, puis comparé avec la valeur cryptée stockée : si les deux résultats sont identiques, c'est que l'utilisateur a saisi le bon mot de passe.

Même si nos mots de passe sont stockées sous forme hachée, le risque subsiste qu'un individu mal intentionné arrive à s'introduire dans la base de données pour dérober ces mots de passe cryptés. Il pourrait ensuite utiliser une solution de type force brute pour hacher un très grand nombre de mots de passe et comparer le résultat avec les mots de passe volés jusqu'à trouver une correspondance. 

Le [salage](http://fr.wikipedia.org/wiki/Salage_\(cryptographie\)) est une solution pour limiter ce risque. Cette technique consiste à ajouter plusieurs caractères au mot de passe juste avant de le hacher. Le résultat du hachage est différent de celui obtenu avec le mot de passe seul. Cela permet de protéger les mots de passe contre les attaques de type [dictionnaire](http://fr.wikipedia.org/wiki/Attaque_par_dictionnaire) (force brute avec utilisation d'une liste de mots de passe potentiels). Les données ajoutés au mot de passe sont appelées *salt*. Pour plus de sécurité, le *salt* doit être différent pour chaque mot de passe.

Pour plus de détails concernant les bonnes pratiques de cryptage des mots de passe, consultez cet [article](http://www.jasypt.org/howtoencryptuserpasswords.html).

## Sécurisation de l'application

### Base de données

La structure de notre base de données doit évoluer afin de refléter les nouveaux besoins métier : un commentaire est maintenant associé à un utilisateur de l'application. Voici le nouveau script SQL `structure.sql` qui permet de créer la base.

    create database if not exists microcms character set utf8 collate utf8_unicode_ci;
    use microcms;
    
    grant all privileges on microcms.* to 'microcms_user'@'localhost' identified by 'secret';
    
    drop table if exists t_comment;
    drop table if exists t_user;
    drop table if exists t_article;
    
    create table t_article (
        art_id integer not null primary key auto_increment,
        art_title varchar(100) not null,
        art_content varchar(2000) not null
    ) engine=innodb character set utf8 collate utf8_unicode_ci;
    
    create table t_user (
        usr_id integer not null primary key auto_increment,
        usr_name varchar(50) not null,
        usr_password varchar(88) not null,
        usr_salt varchar(23) not null,
        usr_role varchar(50) not null 
    ) engine=innodb character set utf8 collate utf8_unicode_ci;
    
    create table t_comment (
        com_id integer not null primary key auto_increment,
        com_content varchar(500) not null,
        art_id integer not null,
        usr_id integer not null,
        constraint fk_com_art foreign key(art_id) references t_article(art_id),
        constraint fk_com_usr foreign key(usr_id) references t_user(usr_id)
    ) engine=innodb character set utf8 collate utf8_unicode_ci;

Les utilisateurs sont stockés dans la table `t_user`. Voici la description de ses champs.

* `usr_id` est l'identifiant de l'utilisateur.
* `usr_name` est le nom de l'utilisateur. Il sera utilisé commé login. 
* `usr_password` est son mot de passé, stockée sous forme hachée.
* `usr_salt` est le *salt* utilisé pour hacher le mot de passe. Il est stocké en clair.
* `usr_role` est le rôle attribué à l'utilisateur. Il sera utilisé lors de la phase d'autorisation.

On observe également que la table `t_comment` contient maintenant une clé étrangère vers la table `t_user`, afin de matérialiser le lien entre un commentaire et son auteur.

Les données de test sont également mises à jour. Voici le script `content.sql` associé.

    insert into t_article(art_title, art_content) values
    ('First article', 'Hi there! This is the very first article.');
    insert into t_article(art_title, art_content) values
    ('Lorem ipsum', 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut hendrerit mauris ac porttitor accumsan. Nunc vitae pulvinar odio, auctor interdum dolor. Aenean sodales dui quis metus iaculis, hendrerit vulputate lorem vestibulum. Suspendisse pulvinar, purus at euismod semper, nulla orci pulvinar massa, ac placerat nisi urna eu tellus. Fusce dapibus rutrum diam et dictum. Sed tellus ipsum, ullamcorper at consectetur vitae, gravida vel sem. Vestibulum pellentesque tortor et elit posuere vulputate. Sed et volutpat nunc. Praesent nec accumsan nisi, in hendrerit nibh. In ipsum mi, fermentum et eleifend eget, eleifend vitae libero. Phasellus in magna tempor diam consequat posuere eu eget urna. Fusce varius nulla dolor, vel semper dui accumsan vitae. Sed eget risus neque.');
    insert into t_article(art_title, art_content) values
    ('Lorem ipsum in french', "J’en dis autant de ceux qui, par mollesse d’esprit, c’est-à-dire par la crainte de la peine et de la douleur, manquent aux devoirs de la vie. Et il est très facile de rendre raison de ce que j’avance. Car, lorsque nous sommes tout à fait libres, et que rien ne nous empêche de faire ce qui peut nous donner le plus de plaisir, nous pouvons nous livrer entièrement à la volupté et chasser toute sorte de douleur ; mais, dans les temps destinés aux devoirs de la société ou à la nécessité des affaires, souvent il faut faire divorce avec la volupté, et ne se point refuser à la peine. La règle que suit en cela un homme sage, c’est de renoncer à de légères voluptés pour en avoir de plus grandes, et de savoir supporter des douleurs légères pour en éviter de plus fâcheuses.");
    
    /* raw password is 'john' */
    insert into t_user(usr_name, usr_salt, usr_password, usr_role) values
    ('JohnDoe', 'YcM=A$nsYzkyeDVjEUa7W9K', 'L2nNR5hIcinaJkKR+j4baYaZjcHS0c3WX2gjYF6Tmgl1Bs+C9Qbr+69X8eQwXDvw0vp73PrcSeT0bGEW5+T2hA==', 'ROLE_USER');
    /* raw password is 'jane' */
    insert into t_user(usr_name, usr_salt, usr_password, usr_role) values
    ('JaneDoe', 'dhMTBkzwDKxnD;4KNs,4ENy', 'EfakNLxyhHy2hVJlxDmVNl1pmgjUZl99gtQ+V3mxSeD8IjeZJ8abnFIpw9QNahwAlEaXBiQUBLXKWRzOmSr8HQ==', 'ROLE_USER');
    
    insert into t_comment(art_id, usr_id, com_content) values
    (1, 1, 'Great! Keep up the good work.');
    insert into t_comment(art_id, usr_id, com_content) values
    (1, 2, "This project is awesome!");

Ce jeu de données insère dans la base les utilisateurs 'JohnDoe' (mot de passe : 'john') et 'JaneDoe' (mot de passe : 'jane'). Pour chaque utilisateur, un *salt* a été généré aléatoirement puis l'algorithme de hachage par défaut de Symfony a été utilisé pour générer le mot de passe crypté. Celui-ci est stocké dans la base. On attribue à tous les utilisateurs le rôle `ROLE_USER` (rôle par défaut pour Symfony).

### Composants Symfony

Afin d'exploiter les fonctionnalités offertes par Symfony, nous devons récupérer les composants nécessaires. Il suffit pour cela de les déclarer dans le fichier de dépendances `composer.json`.

    "require": {
        ...
        "symfony/security": "~2.4",
        "symfony/twig-bridge": "~2.4"
    }
    ...

Le composant `security` regroupe les services de gestion de la sécurité. Le composant `twig-bridge` permet d'accéder à certains services Symfony depuis les templates Twig.

Une fois ce fichier modifié, on utilise Composer pour télécharger ces composants et leurs éventuelles dépendances.

    $ composer update

### Partie Modèle

La première étape de notre travail dans cette partie est de modéliser un utilisateur de l'application sous la forme d'une classe `User` située dans l'espace de noms `MicroCMS\Domain`. Voici son code source. 

    <?php
    
    namespace MicroCMS\Domain;
    
    use Symfony\Component\Security\Core\User\UserInterface;
    
    class User implements UserInterface
    {
        /**
         * User id.
         *
         * @var integer
         */
        private $id;
    
        /**
         * User name.
         *
         * @var string
         */
        private $username;
    
        /**
         * User password.
         *
         * @var string
         */
        private $password;
    
        /**
         * Salt that was originally used to encode the password.
         *
         * @var string
         */
        private $salt;
    
        /**
         * Role.
         * Values : ROLE_USER or ROLE_ADMIN.
         *
         * @var string
         */
        private $role;
    
        public function getId() {
            return $this->id;
        }
    
        public function setId($id) {
            $this->id = $id;
        }
    
        /**
         * @inheritDoc
         */
        public function getUsername() {
            return $this->username;
        }
    
        public function setUsername($username) {
            $this->username = $username;
        }
    
        /**
         * @inheritDoc
         */
        public function getPassword() {
            return $this->password;
        }
    
        public function setPassword($password) {
            $this->password = $password;
        }
    
        /**
         * @inheritDoc
         */
        public function getSalt()
        {
            return $this->salt;
        }
    
        public function setSalt($salt)
        {
            $this->salt = $salt;
        }
    
        public function getRole()
        {
            return $this->role;
        }
    
        public function setRole($role) {
            $this->role = $role;
        }
    
        /**
         * @inheritDoc
         */
        public function getRoles()
        {
            return array($this->getRole());
        }
    
        /**
         * @inheritDoc
         */
        public function eraseCredentials() {
            // Nothing to do here
        }
    }

On constate une différence majeure avec les classes métier `Article` et `Comment` : la classe `User` implémente l'interface Symfony [UserInterface](http://api.symfony.com/2.5/Symfony/Component/Security/Core/User/UserInterface.html) et définit les méthodes présentes dans cette interface. Ces méthodes sont indispensables pour que l'utilisateur puisse être authentifié et autorisé par Symfony.

La classe `Comment` subit un changement (mineur du point de vue du code source) : sa propriété `author` n'est plus une chaîne de caractères, mais une instance de la classe `User`. On met à jour le commentaire pour refléter cette évolution.

    <?php
    
    namespace MicroCMS\Domain;
    
    class Comment 
    {
        // ...
    
        /**
         * Comment author.
         *
         * @var \MicroCMS\Domain\User
         */
        private $author;

        // ...

Nous devons également créer la classe `UserDAO` qui gère l'accès aux utilisateurs.

    <?php
    
    namespace MicroCMS\DAO;
    
    use Symfony\Component\Security\Core\User\UserInterface;
    use Symfony\Component\Security\Core\User\UserProviderInterface;
    use Symfony\Component\Security\Core\Exception\UsernameNotFoundException;
    use Symfony\Component\Security\Core\Exception\UnsupportedUserException;
    use MicroCMS\Domain\User;
    
    class UserDAO extends DAO implements UserProviderInterface
    {
        /**
         * Returns a user matching the supplied id.
         *
         * @param integer $id
         *
         * @return \MicroCMS\Domain\User|throws an exception if no matching user is found
         */
        public function find($id) {
            $sql = "select * from t_user where usr_id=?";
            $row = $this->getDb()->fetchAssoc($sql, array($id));
    
            if ($row)
                return $this->buildDomainObject($row);
            else
                throw new \Exception("No user matching id " . $id);
        }
    
        /**
         * {@inheritDoc}
         */
        public function loadUserByUsername($username)
        {
            $sql = "select * from t_user where usr_name=?";
            $row = $this->getDb()->fetchAssoc($sql, array($username));
    
            if ($row)
                return $this->buildDomainObject($row);
            else
                throw new UsernameNotFoundException(sprintf('User "%s" not found.', $username));
        }
    
        /**
         * {@inheritDoc}
         */
        public function refreshUser(UserInterface $user)
        {
            $class = get_class($user);
            if (!$this->supportsClass($class)) {
                throw new UnsupportedUserException(sprintf('Instances of "%s" are not supported.', $class));
            }
            return $this->loadUserByUsername($user->getUsername());
        }
    
        /**
         * {@inheritDoc}
         */
        public function supportsClass($class)
        {
            return 'MicroCMS\Domain\User' === $class;
        }
    
        /**
         * Creates a User object based on a DB row.
         *
         * @param array $row The DB row containing User data.
         * @return \MicroCMS\Domain\User
         */
        protected function buildDomainObject($row) {
            $user = new User();
            $user->setId($row['usr_id']);
            $user->setUsername($row['usr_name']);
            $user->setPassword($row['usr_password']);
            $user->setSalt($row['usr_salt']);
            $user->setRole($row['usr_role']);
            return $user;
        }
    }

Cette classe reprend la structure de nos classes DAO existantes et implémente l'interface Symfony [UserProviderInterface](http://api.symfony.com/2.5/Symfony/Component/Security/Core/User/UserProviderInterface.html). Cette interface contient les méthodes nécessaires pour qu'une classe puisse être utilisée comme *fournisseur de données utilisateur* par le composant de gestion de la sécurité de Symfony au cours du processus d'authentification.

La classe `CommentDAO` est mise à jour : elle dépend maintenant de la classe `UserDAO` pour construire un objet `Comment` complet à partir d'un résultat de requête SQL.

    <?php
    
    namespace MicroCMS\DAO;
    
    use MicroCMS\Domain\Comment;
    
    class CommentDAO extends DAO 
    {
        // ...
    
        /**
         * @var \MicroCMS\DAO\UserDAO
         */
        protected $userDAO;
    
        public function setUserDAO($userDAO) {
            $this->userDAO = $userDAO;
        }
    
        // ...
    
        /**
         * Creates an Comment object based on a DB row.
         *
         * @param array $row The DB row containing Comment data.
         * @return \MicroCMS\Domain\Comment
         */
        protected function buildDomainObject($row) {
            // Find the associated article
            $articleId = $row['art_id'];
            $article = $this->articleDAO->find($articleId);
    
            // Find the associated user
            $userId = $row['usr_id'];
            $user = $this->userDAO->find($userId);
    
            $comment = new Comment();
            $comment->setId($row['com_id']);
            $comment->setContent($row['com_content']);
            $comment->setArticle($article);
            $comment->setAuthor($user);
            return $comment;
        }
    }

### Partie Contrôleur

Le fichier de configuration de l'application Silex `app.php` est modifié pour intégrer les nouveaux services.

    <?php
    
    // Register global error and exception handlers
    use Symfony\Component\Debug\ErrorHandler;
    ErrorHandler::register();
    use Symfony\Component\Debug\ExceptionHandler;
    ExceptionHandler::register();
    
    // Register service providers.
    $app->register(new Silex\Provider\DoctrineServiceProvider());
    $app->register(new Silex\Provider\TwigServiceProvider(), array(
        'twig.path' => __DIR__.'/../views',
    ));
    $app->register(new Silex\Provider\SessionServiceProvider());
    $app->register(new Silex\Provider\UrlGeneratorServiceProvider());
    $app->register(new Silex\Provider\SecurityServiceProvider(), array(
        'security.firewalls' => array(
            'secured' => array(
                'pattern' => '^/',
                'anonymous' => true,
                'logout' => true,
                'form' => array('login_path' => '/login', 'check_path' => '/login_check'),
                'users' => $app->share(function () use ($app) {
                    return new MicroCMS\DAO\UserDAO($app['db']);
                }),
            ),
        ),
    ));
    
    // Register services.
    $app['dao.article'] = $app->share(function ($app) {
        return new MicroCMS\DAO\ArticleDAO($app['db']);
    });
    $app['dao.user'] = $app->share(function ($app) {
        return new MicroCMS\DAO\UserDAO($app['db']);
    });
    $app['dao.comment'] = $app->share(function ($app) {
        $commentDAO = new MicroCMS\DAO\CommentDAO($app['db']);
        $commentDAO->setArticleDAO($app['dao.article']);
        $commentDAO->setUserDAO($app['dao.user']);
        return $commentDAO;
    });

Il est important de bien comprendre les paramètres utilisés pour la définition du pare-feu (*firewall*) associé au fournisseur de services *SecurityServiceProvider* :

* `pattern` définit la partie sécurisée de l'application sous la forme d'une [expression rationnelle](http://fr.wikipedia.org/wiki/Expression_rationnelle). Ici, la valeur `^/` indique que le pare-feu sécurise l'intégralité de l'application ;
* `anonymous` précise qu'un utilisateur non authentifié peut tout de même accéder à la partie sécurisée. Il est nécessaire pour que les visiteurs anonymes puissent continuer à consulter les articles du CMS ;
* `logout` indique qu'il est possible pour les utilisateurs authentifiés de se déconnecter de l'application ;
* `form` permet d'utiliser un formulaire comme méthode d'authentification. `login_path` définit le chemin vers le formulaire et `check_path` le chemin d'authentification ;
* `users` définit le fournisseur de données utilisateur, autrement dit la source de données qui permet d'accéder aux utilisateurs de l'application. Ici, il s'agit logiquement d'une instance de la classe `UserDAO` créée précédemment.

{{% remark %}}
L'enregistrement du fournisseur de services *SessionServiceProvider* démarre automatiquement la gestion des sessions.
{{% /remark %}}

Il faut aussi ajouter une route pour afficher le formulaire d'authentification dans le fichier `routes.php`.

    <?php
    
    use Symfony\Component\HttpFoundation\Request;
    
    // ...
    
    // Login form
    $app->get('/login', function(Request $request) use ($app) {
        return $app['twig']->render('login.html.twig', array(
            'error'         => $app['security.last_error']($request),
            'last_username' => $app['session']->get('_security.last_username'),
        ));
    })->bind('login');  // named route so that path('login') works in Twig templates

Elle utilise la classe Symfony `Request` pour afficher la vue `login.html.twig` en lui passant en paramètres l'éventuelle dernière erreur de sécurité (par exemple un utilisateur non reconnu) et le dernier nom d'utilisateur utilisé.

{{% warning %}}
Cette nouvelle route est nommée `login` grâce à l'appel à la méthode `bind`. Sans cela, l'appel à la fonction `path('login')` dans un template Twig provoque une erreur (voir plus loin).
{{% /warning %}}

### Partie Vue

Dans la partie Vue, il faut tout d'abord créer la vue `login.html.twig` associée à la route d'authentification.

    {% extends 'layout.html.twig' %}
    
    {% block title %}User authentication{% endblock %}
    
    {% block content %}
    <h2 class="text-center">{{ block('title') }}</h2>
    {% if error %}
    <div class="alert alert-danger">
        <strong>Login failed!</strong> {{ error }}
    </div>
    {% endif %}
    <div class="well">
        <form class="form-signin form-horizontal" role="form" action="{{ path('login_check') }}" method="post">
            <div class="form-group">
                <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
                <input type="text" name="_username" value="{{ last_username }}" class="form-control" placeholder="Enter your username" required autofocus>
                </div>
            </div>
            <div class="form-group">
                <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
                    <input type="password" name="_password" class="form-control" placeholder="Enter your password" required>
                </div>
            </div>
            <div class="form-group">
                <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
                    <button type="submit" class="btn btn-default btn-primary"><span class="glyphicon glyphicon-log-in"></span> Login</button>
                </div>
            </div>
        </form>
    </div>
    {% endblock %}

Comme toutes nos vues, elle hérite de `layout.html.twig` afin d'intégrer les éléments d'interface communs (barre de navigation, pied de page, etc). Elle définit un formulaire (balise `<form>`) contenant les champs `_username` et '_password' pour saisir le login et le mot de passe de l'utilisateur. L'action associée à ce formulaire utilise la fonction `path` (fournie par le composant `twig-bridge`) pour récupérer le chemin d'authentification défini lors du paramétrage du pare-feu. Le nom de ce chemin provient de la valeur du paramètre `check_path` : les `/` sont remplacés par des `_` et le `/` initial est supprimé.

Ensuite, on modifie la vue `article.html.twig` pour obtenir un affichage adapté à la présence d'un utilisateur connecté.

    {% extends "layout.html.twig" %}
    
    {% block title %}{{ article.title }}{% endblock %}
    
    {% block content %}
    <p>
        <h2>{{ article.title }}</h2>
        <p>{{ article.content }}</p>
        
        <h3>Comments</h3>
        {% if comments %}
            {% for comment in comments %}
                <strong>{{ comment.author.username }}</strong> said : {{ comment.content }}<br>
            {% endfor %}
        {% else %}
            No comments yet.
        {% endif %}
    
        <h3>Add a comment</h3>
        {% if is_granted('IS_AUTHENTICATED_FULLY') %}
            Soon!
        {% else %}
            <a href="{{ path('login') }} ">Log in</a> to add comments.
        {% endif %}
    </p>
    {% endblock %} 

Le nom de l'auteur du commentaire est maintenant accessible via la variable Twig `comment.author.username` et non plus `comment.author`. L'appel à la fonction Twig `is_granted('IS_AUTHENTICATED_FULLY')` permet de vérifier si la vue est affichée pour un utilisateur authentifié par l'application. Si c'est le cas, il faudrait lui offrir la possibilité d'ajouter un commentaire. Ce sera l'objet d'une prochaine itération. Sinon, On précise au visiteur anonyme qu'il doit se connecter pour pouvoir commenter l'article.

Enfin, on modifie la partie commune à toutes les vues (fichier `layout.html.twig`) afin d'ajouter à la barre de navigation un menu déroulant associé à l'éventuel utilisateur authentifié.

    <!doctype html>
    <html>
    <head>
        <!-- ...-->
    </head>
    <body>
        <div class="container">
            <nav class="navbar navbar-default navbar-fixed-top navbar-inverse" role="navigation">
                <div class="container">
                    <div class="navbar-header">
                        <!-- ... -->
                    </div>
                    <div class="collapse navbar-collapse" id="navbar-collapse-target">
                        <ul class="nav navbar-nav navbar-right">
                            {% if is_granted('IS_AUTHENTICATED_FULLY') %}
                                <li class="dropdown">
                                <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                                    <span class="glyphicon glyphicon-user"></span> Welcome, {{ app.security.token.user.username }} <b class="caret"></b></a>
                                    <ul class="dropdown-menu">
                                        <li><a href="{{ path('logout') }}">Log out</a></li>
                                    </ul>
                                </li>
                            {% else %}
                                <li class="dropdown">
                                <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                                    <span class="glyphicon glyphicon-user"></span> Not connected <b class="caret"></b></a>
                                    <ul class="dropdown-menu">
                                        <li><a href="{{ path('login') }}">Log in</a></li>
                                    </ul>
                                </li>
                            {% endif %}
                        </ul>
                    </div>
                </div><!-- /.container -->
            </nav>
            <!-- ... -->
        </div>
    
        <!-- jQuery -->
        <script src="{{ app.request.basepath }}/lib/jquery/jquery-1.11.1.min.js"></script>
        <!-- JavaScript Boostrap plugin -->
        <script src="{{ app.request.basepath }}/lib/bootstrap/js/bootstrap.min.js"></script>
    </body>
    </html>

Si l'utilisateur est authentifié, le menu affiche son nom (accessible via la variable Twig `app.security.token.user.username`) et lui permet de se déconnecter (lien vers `path('logout')`). Sinon, il affiche un message et un lien vers le formulaire d'authentification (lien vers `path('login')`). On ajoute également des liens vers jQuery et le plugin JavaScript de Bootstrap afin de faire fonctionner le menu déroulant.

{{% tip %}}
L'ajout des liens JavaScript en fin de fichier plutôt qu'au début est une bonne pratique qui permet d'optimiser le temps de chargement des pages.
{{% /tip %}}

### Résultat obtenu

La sécurisation de notre application est terminée. Ouvrez l'URL http://microcms pour afficher la page d'accueil de l'application. Elle doit maintenant disposer d'un menu déroulant en haut à droite. Lorsqu'aucun utilisateur ne s'est authentifié, ce menu comporte une entrée invitant l'utilisateur à le faire.

{{% image src="microcms_article_anonymous_user.png" class="centered" %}}

Le formulaire d'authentification permet à l'utilisateur de saisir son nom et son mot de passe. Les éventuelles erreurs d'authentification sont affichées.

{{% image src="microcms_login_form.png" class="centered" %}}

Lorsque l'authentification réussit, le menu déroulant de la barre de navigation est mis à jour, ainsi que l'affichage d'un article.

{{% image src="microms_article_authenticated_user.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-08).

## Bilan

Cette itération nous a permis de sécuriser notre application Web en exploitant les possibilités offertes par Symfony (et donc Silex). On constate combien l'intégration d'un framework, même si elle nécessite un travail initial d'adaptation, facilite l'ajout de fonctionnalités complexes à une application Web.

La prochaine itération permettra aux utilisateurs authentifiés d'interagir avec l'application.

# Itération 9 : ajout de commentaires à un article

Le but de cette itération est de permettre aux utilisateurs authentifiés d'ajouter des commentaires à un article.

## Symfony et les formulaires

La saisie de commentaires par les utilisateurs de l'application implique l'ajout d'un formulaire dans la vue qui affiche les détails sur un article. Il serait possible de gérer manuellement la définition de ce formulaire et la récupération des données saisies. Nous allons plutôt en profiter pour découvrir une autre des fonctionnalités offertes par le framework Symfony : la gestion des formulaires.

Grâce au composant [Form](http://symfony.com/doc/current/book/forms.html), Symfony permet de créer un formulaire Web à partir d'un objet. Les champs du formulaire sont associés aux propriétés de cet objet. Cette association est bidirectionnelle : le formulaire affiche les valeurs des propriétés de l'objet, et sa soumission (*submit*) met à jour les propriétés de l'objet. Le composant Form permet encore bien d'autres choses, comme nous allons le voir à présent.

## Mise à jour de l'application

### Composants Symfony

Commençons par récupérer les composants Symfony nécessaires en les ajoutant dans le fichier de dépendances `composer.json`.

    "require": {
        ...
        "symfony/form": "~2.4",
        "symfony/translation": "~2.4"
    }
    ...

Le composant `form` regroupe les services de gestion des formulaires. Le composant `translation` offre des services de traduction nécessaires pour utiliser le composant `form`.

Une fois ce fichier modifié, on utilise Composer pour télécharger ces composants et leurs éventuelles dépendances.

    $ composer update

### Partie Modèle

Le formulaire que nous devons créer permettra à un utilisateur connecté de saisir un nouveau commentaire. Il sera associé à un objet de la classe métier `Comment`. Voici pour rappel le diagramme de nos classes métier actuelles.

{{% image src="microcms_uml_article_comment_author.jpeg" class="centered" %}}

Le nouveau commentaire sera associé à un article et à un utilisateur existants. Son identifiant sera défini au moment de son insertion dans la base de données. Le seul champ que notre formulaire pemettra de saisir sera donc le contenu du commentaire.

Symfony offre plusieurs manières de créer un formulaire. Nous allons employer la technique recommandée qui consiste à le définir dans sa propre classe, afin de le rendre réutilisable dans toute l'application. Dans le répertoire `src/MicroCMS/Form/Type` (à créer lui aussi), ajoutez un nouveau fichier source nommé 'CommentType.php`. Placez-y le code source suivant.

    <?php
    
    namespace MicroCMS\Form\Type;
    
    use Symfony\Component\Form\AbstractType;
    use Symfony\Component\Form\FormBuilderInterface;
    
    class CommentType extends AbstractType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder
                ->add('content', 'textarea', array(
                    'attr' => array(
                        'rows' => '4',
                        'placeholder' => 'Enter your comment',
                    )
                ))
                ->add('save', 'submit', array(
                    'label' => 'Publish comment',
                ));
        }
    
        public function getName()
        {
            return 'comment';
        }
    }

Notre classe hérite de la classe Symfony [AbstractType](http://api.symfony.com/2.5/Symfony/Component/Form/AbstractType.html) et redéfinit sa méthode `buildForm` qui, comme son nom l'indique, permet de construire un formulaire. Ici, le formulaire aura une zone de texte associée au contenu du commentaire (champ `content` de type `textarea`) et un bouton pour soumettre le formulaire (champ `save` de type `submit`). On définit également le nombre de lignes et le message d'aide à la saisie de la zone de texte, ainsi que le texte du bouton de soumission.

{{% warning %}}
Le nom de la zone de texte ("content") n'est pas choisi au hasard : il correspond exactement à la propriété `content` de la classe métier `Comment`. C'est indispensable pour que Symfony puisse associer notre formulaire à une instance de `Comment`.
{{% /warning %}}

Nous devons modifier la classe `CommentDAO` pour la rendre capable d'insérer des commentaires dans la base de données. Pour cela, une méthode `save` est ajoutée à cette classe.

    <?php

    namespace MicroCMS\DAO;

    use MicroCMS\Domain\Comment;

    class CommentDAO extends DAO 
    {
        // ...

        /**
         * Saves a comment into the database.
         *
         * @param \MicroCMS\Domain\Comment $comment The comment to save
         */
        public function save($comment) {
            $commentData = array(
                'art_id' => $comment->getArticle()->getId(),
                'usr_id' => $comment->getAuthor()->getId(),
                'com_content' => $comment->getContent()
                );
    
            if ($comment->getId()) {
                // The comment has already been saved : update it
                $this->getDb()->update('t_comment', $commentData, array('com_id' => $comment->getId()));
            } else {
                // The comment has never been saved : insert it
                $this->getDb()->insert('t_comment', $commentData);
                // Get the id of the newly created comment and set it on the entity.
                $id = $this->getDb()->lastInsertId();
                $comment->setId($id);
            }
        }

        // ...

Cette méthode rassemble les valeurs BD dans le tableau `$commentData`, puis vérifie s'il faut insérer ou mettre à jour le commentaire en se basant sur l'existence d'une valeur pour l'identifiant du commentaire. Ensuite, elle utilise la méthode DBAL appropriée pour effectuer l'opération dans la table `t_comment`.

### Partie Contrôleur

Nous devons tout d'abord enregistrer les nouveaux fournisseurs de services utilisés dans la fichier `app.php`.

    <?php

    // ...

    $app->register(new Silex\Provider\FormServiceProvider());
    $app->register(new Silex\Provider\TranslationServiceProvider());

    // ...

Ensuite, il faut mettre à jour le fichier `routes.php` pour créer le formulaire d'ajout d'un commentaire avant de générer la vue qui affiche les détails sur un article. Voici le nouveau contenu de ce fichier.

    <?php
    
    use Symfony\Component\HttpFoundation\Request;
    use MicroCMS\Domain\Comment;
    use MicroCMS\Domain\Article;
    use MicroCMS\Domain\User;
    use MicroCMS\Form\Type\CommentType;
    
    // Home page
    $app->get('/', function () use ($app) {
        $articles = $app['dao.article']->findAll();
        return $app['twig']->render('index.html.twig', array('articles' => $articles));
    });
    
    // Detailed info about an article
    $app->match('/article/{id}', function ($id, Request $request) use ($app) {
        $article = $app['dao.article']->find($id);
        $user = $app['security']->getToken()->getUser();
        $commentFormView = NULL;
        if ($app['security']->isGranted('IS_AUTHENTICATED_FULLY')) {
            // A user is fully authenticated : he can add comments
            $comment = new Comment();
            $comment->setArticle($article);
            $comment->setAuthor($user);
            $commentForm = $app['form.factory']->create(new CommentType(), $comment);
            $commentForm->handleRequest($request);
            if ($commentForm->isValid()) {
                $app['dao.comment']->save($comment);
                $app['session']->getFlashBag()->add('success', 'Your comment was succesfully added.');
            }
            $commentFormView = $commentForm->createView();
        }
        $comments = $app['dao.comment']->findAllByArticle($id);
        return $app['twig']->render('article.html.twig', array(
            'article' => $article, 
            'comments' => $comments,
            'commentForm' => $commentFormView));
    });
    
    // Login form
    $app->get('/login', function(Request $request) use ($app) {
        return $app['twig']->render('login.html.twig', array(
            'error'         => $app['security.last_error']($request),
            'last_username' => $app['session']->get('_security.last_username'),
            ));
    })->bind('login');  // named route so that path('login') works in Twig templates

Pour la route `/article/{id}`, nous avons remplacé `$app->get(...)` par `$app->match(...)` afin de gérer à la fois l'accès à cette route via les commandes HTTP GET et POST (`$app->get(...)` ne gère que la commande GET).

A l'intérieur de cette route, on récupère l'article (via son identifiant passé dans l'URL) puis l'utilisateur connecté (en utilisant le service `security` de Symfony). S'il y a bien un utilisateur connecté, on crée un nouveau commentaire puis le formulaire associé à ce commentaire (appel à `$app['form.factory']->create(...)`). Ensuite, la méthode `handleRequest` gère la soumission du formulaire ([plus de détails](http://symfony.com/doc/current/book/forms.html#handling-form-submissions)). Si les données reçues sont valides, on fait appel au DAO pour sauvegarder le nouveau commentaire et on crée un message de succès.

Dans tous les cas, on ajoute aux données dynamiques envoyées à la vue le formulaire d'ajout d'un commentaire (variable `$commentFormView`). Si aucun utilisateur n'est connecté, cette variable vaut `NULL`.

### Partie Vue

Il nous reste à afficher le formulaire créé dans la partie Contrôleur. Pour cela, on modifie le template `article.html.twig` de la manière suivante.

    {% extends "layout.html.twig" %}
    
    {% block title %}{{ article.title }}{% endblock %}
    
    {% block content %}
    <p>
        <h2>{{ article.title }}</h2>
        <p>{{ article.content }}</p>
        
        <h3>Comments</h3>
        {% if comments %}
            {% for comment in comments %}
                <strong>{{ comment.author.username }}</strong> said : {{ comment.content }}<br>
            {% endfor %}
        {% else %}
            No comments yet.
        {% endif %}
    
        <h3>Add a comment</h3>
        {% if commentForm %}
            {{ form_start(commentForm) }}
                <div class="form-group">
                    {{ form_errors(commentForm.content) }}
                    {{ form_widget(commentForm.content, { 'attr':  {
                        'class': 'form-control'
                    }}) }}
                </div>
                <div class="form-group">
                    {{ form_row(commentForm.save, { 'attr':  {
                        'class': 'btn btn-primary'
                    }}) }}
                </div>
            {{ form_end(commentForm) }}
            {% for flashMessage in app.session.flashbag.get('success') %}
                <div class="alert alert-success">
                    {{ flashMessage }}
                </div>
            {% endfor %}
        {% else %}
            <a href="{{ path('login') }} ">Log in</a> to add comments.
        {% endif %}
    </p>
    {% endblock %}

Dans ce template, on vérifie si le formulaire `commentForm` existe puis (si c'est le cas) on utilise des fonctions Twig pour générer le code HTML associé à chaque partie du formulaire.

* `form_start` génère le début du formulaire (balise HTML `<form>`).
* `form_widget` génère un champ de formulaire.
* `form_row` génère également un champ de formulaire en y ajoutant son label et les éventuelles erreurs associées.

Pour plus de précisions, consultez la [documentation détaillée](http://symfony.com/doc/current/reference/forms/twig_reference.html) de ces fonctions.

{{% remark %}}
Les champs générés par un formulaire Symfony sont par défaut obligatoires (attribut HTML5 `required`), ce qui pourra déclencher une validation côté navigateur.
{{% /remark %}}

On associe à chaque champ généré des classes Bootstrap (`form-group` et `form-control`) afin d'améliorer la présentation. Les éventuels messages de succès sont également affichés via Bootstrap.

### Résultat obtenu

Lorsqu'un utilisateur connecté clique sur le titre d'un article, la vue qui affiche son détail lui permet à présent d'ajouter un commentaire.

{{% image src="microcms_comment_form.png" class="centered" %}}

Une fois le commentaire saisi et publié, l'affichage de l'article intègre le nouveau commentaire ainsi qu'un un message de succès.

{{% image src="microcms_comment_publish.png" class="centered" %}}

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-09).

## Bilan

Cette itération a fourni l'occasion d'intégrer à notre application la gestion des formulaires. Le composant Symfony associé permet de simplifier grandement ce processus. Ce composant est très puissant et dispose de nombreuses autres fonctionnalités que celles présentées ici.

# Conclusion

Notre application Web d'exemple était au départ une simple page écrite en PHP classique. A présent, elle dispose d'une architecture robuste dont on peut rappeler les principales caractéristiques :

* séparation des responsabilités selon le principe Modèle-Vue-Contrôleur ;
* intégration d'un micro-framework ;
* modélisation objet du domaine et de l'accès aux données ;
* utilisation des espaces de noms et chargement automatique des classes ;
* intégration d'un moteur de templates pour faciliter l'écriture des vues ;
* présentation moderne et adaptée au terminal utilisé (*responsive design*) ;
* gestion avancée de la sécurité et des formulaires.

D'autres fonctionnalités comme la modélisation orientée objet des contrôleurs, la validation des formulaires, la journalisation ou encore l'internationalisation pourraient être ajoutées en exploitant les possibilités de Silex. A vous de jouer !

Ainsi se termine ce tutoriel qui vous aura, je l'espère, aidé à progresser en PHP.
