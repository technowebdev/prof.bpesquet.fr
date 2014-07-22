---
title: "Développement PHP moderne"
date: 2014-07-22
---

Découvrez comment bâtir une application Web fonctionnelle et sûre en tirant le meilleur du langage PHP.

{{% warning %}}
Ce tutoriel est en cours d'écriture.
{{% /warning %}}

# Introduction

## Pourquoi ce tutoriel

Le langage [PHP](http://php.net) est à l'heure actuelle le principal langage serveur du Web dynamique. Il souffre malgré tout d'un déficit d'image par rapport à des technologies concurrentes comme ASP.NET ou Java. Ces dernières imposent un cadre rigide qui guide et rassure le développeur. A l'inverse, PHP est une technologie très souple qui laisse beaucoup de liberté, y compris celle de faire un peu n'importe quoi. Lorsqu'on développe en PHP, il est donc essentiel de connaître et d'appliquer les meilleures pratiques.

PHP a évolué avec le temps et dispose à présent de fonctionnalités avancées parfois méconnues. Son écosystème est très riche et des milliers de projets cherchent à améliorer l'expérience du développeur PHP. Il n'est pas facile de se repérer dans cette jungle foisonnante pour choisir les bons outils.

Ce tutoriel vise à présenter une manière de concevoir une application Web en tirant parti des possibilités qu'offre le langage PHP et en s'appuyant sur des outils de son écosystème qui ont fait leurs preuves. En un mot, en utilisant PHP de manière **moderne**.

## Contexte choisi

Nous allons mettre en oeuvre les principes présentés dans ce tutoriel en construisant un exemple simple : une application Web de type [CMS](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_contenu). Notre micro-CMS d'exemple sera basique : il permettra de gérer une liste d'articles ainsi que les commentaires associés.

Le code source associé est disponible sous la forme d'un [dépôt GitHub](https://github.com/bpesquet/MicroCMS).

## Méthodologie de réalisation

En nous inspirant des [méthodes agiles](http://fr.wikipedia.org/wiki/M%C3%A9thode_agile) et notamment de [SCRUM](http://fr.wikipedia.org/wiki/Scrum_(m%C3%A9thode\)), nous allons bâtir l'application par étapes successives appelées **itérations**, ou encore [sprints](http://fr.wikipedia.org/wiki/Scrum_\(m%C3%A9thode\)#Le_sprint) dans SCRUM. 

{{% definition %}}
Une itération est une phase de travail volontairement courte permettant de produire une version souvent limitée mais toujours livrable d'un produit.
{{% /definition %}}

Certaines itérations seront consacrées à l'ajout de nouvelles fonctionnalités à l'application. Les autres permettront d'améliorer son architecture en pratiquant ce qu'on appelle la [refactorisation](http://fr.wikipedia.org/wiki/R%C3%A9usinage_de_code) (*refactoring*). 

## Fonctionnalités attendues

On regroupe dans les tableaux ci-dessous les fonctionnalités attendues de l'application que nous allons construire. En conformité avec la méthodologie agile choisie, nous exprimons les fonctionnalités métier sous la forme de [récits utilisateur](http://fr.wikipedia.org/wiki/R%C3%A9cit_utilisateur) (*user stories*).

### Récits utilisateur

Référence | Description
----------|------------
User_U01 | En tant que visiteur anonyme, je peux visualiser la liste de tous les articles sur la page d'accueil.
User_U02 | En tant que visiteur anonyme, je peux accéder à l'application depuis un terminal fixe ou mobile et obtenir un affichage toujours adapté.
User_U03 | En tant que visiteur anonyme, je peux cliquer sur le titre d'un article afin de consulter son contenu et ses commentaires.
User_U04 | En tant que visiteur anonyme, je peux m'inscrire comme utilisateur enregistré en saisissant mes informations personnelles : nom, prénom, adresse de courriel et mot de passe.
User_U05 | En tant qu'utilisateur, je peux me connecter en indiquant mon adresse de courriel (utilisée comme login) et mon mot de passe.
User_U06 | En tant qu'utilisateur connecté, je peux ajouter un commentaire à un article.
User_U07 | En tant qu'utilisateur connecté, je peux modifier mes informations personnelles.
User_U08 | En tant qu'utilisateur connecté, je peux me déconnecter pour redevenir un utilisateur anonyme.
User_A01 | En tant qu'administrateur, je peux me connecter de la même manière qu'un utilisateur.
User_A02 | En tant qu'administrateur connecté, j'ai les mêmes possibilités qu'un utilisateur connecté.
User_A03 | En tant qu'administrateur connecté, je peux créer un nouvel article.
User_A04 | En tant qu'administrateur connecté, je peux modifier un article existant.
User_A05 | En tant qu'administrateur connecté, je peux supprimer un article existant.
User_D01 | En tant que développeur extérieur, je peux utiliser un service Web pour accéder à la liste des articles.

### Récits techniques

Référence | Description
----------|------------
Tech_01 | L'application utilise une base de données relationnelle pour stocker ses données persistantes.
Tech_02 | L'application respecte une architecture de type MVC (Modèle-Vue-Contrôleur).
Tech_03 | L'architecture de l'application se base sur un *framework* PHP.
Tech_04 | Les données métier de l'application font l'objet d'une modélisation orientée objet.
Tech_05 | L'application est protégée contre le risque d'injection de code SQL dans la base de données.
Tech_06 | L'application est protégée contre le risque d'injection de code dans les pages Web affichées.

{{% remark %}}
Il existe un [débat](http://www.areyouagile.com/2013/03/pourquoi-une-user-story-technique-est-un-aveu-dechec/) concernant le bien-fondé de l'ajout de récits strictements techniques à un projet agile. Comme la valeur créée par notre projet d'exemple (apprendre à développer en PHP de manière moderne) est avant tout d'ordre technique, cela me paraît légitime ici.
{{% /remark %}}

### Carnet du produit

L'ensemble de ces récits forme ce qu'on appelle dans SCRUM le [carnet du produit](http://fr.wikipedia.org/wiki/Scrum_\(m%C3%A9thode\)#Carnet_du_produit_.28Product_Backlog.29) (*product backlog*). Chaque itération (sprint) va s'attacher à réaliser un ou plusieurs récits afin de vider progressivement le *backlog*, avec toujours l'idée d'obtenir en fin d'itération un produit livrable.

{{% remark %}}
Dans un contexte réel, le *backlog* évolue en même temps que le produit : nouveaux récits, bogues à corriger, etc.
{{% /remark %}}

# Itération 1 : initialisation de l'application

Le but de cette itération est d'écrire la toute première version de notre application Web d'exemple.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
User_U01 | En tant que visiteur anonyme, je peux visualiser la liste de tous les articles sur la page d'accueil.
Tech_01 | L'application utilise une base de données relationnelle pour stocker ses données persistantes.

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

## Conclusion

La toute première version (très simpliste) de notre application Web est maintenant opérationnelle. La prochaine itération va consister à améliorer son architecture.


# Itération 2 : refactorisation de l'architecture

Le but de cette itération est d'améliorer l'architecture de notre application Web d'exemple.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
Tech_02 | L'application respecte une architecture de type MVC (Modèle-Vue-Contrôleur).

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
La balise de fin de code PHP `?>` est volontairement omise à la fin du fichier `index.php. C'est une [bonne pratique](http://php.net/manual/fr/language.basic-syntax.phptags.php) pour les fichiers qui ne contiennent que du PHP. Elle permet d'éviter des problèmes lors d'inclusions de fichiers.
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

### Conclusion

Outre la feuille de style `microcms.css`, notre application Web est maintenant constituée de trois fichiers :

* `model.php` (PHP uniquement) pour l'accès aux données ;
* `view.php` (PHP et HTML) pour l'affichage des billets du blog ;
* `index.php` (PHP uniquement) pour faire le lien entre les deux pages précédentes.

Le code source associé à cette itération est disponible sur une [branche du dépôt GitHub](https://github.com/bpesquet/MicroCMS/tree/iteration-02).

Cette nouvelle structure est plus complexe, mais les responsabilités de chaque partie sont maintenant claires. En faisant ce travail de *refactoring*, nous avons rendu notre exemple conforme à un modèle d'architecture très employé sur le Web : le modèle MVC.

## Le modèle MVC

### Présentation

Le modèle MVC décrit une manière d'architecturer une application informatique en la décomposant en trois sous-parties :

* la partie Modèle ;
* la partie Vue ;
* la partie Contrôleur.

Ce modèle de conception (*design pattern*) a été imaginé à la fin des années 1970 pour le langage Smalltalk afin de bien séparer le code de l'interface graphique de la logique applicative. Il est utilisé dans de très nombreux langages : bibliothèques Swing et Model 2 (JSP) de Java, frameworks PHP, ASP.NET MVC, etc.

### Rôles des composants

La partie **Modèle** d'une architecture MVC encapsule la logique métier (*business logic*) ainsi que l'accès aux données. Il peut s'agir d'un ensemble de fonctions (Modèle procédural) ou de classes (Modèle orienté objet).

La partie Vue s'occupe des interactions avec l'utilisateur : présentation, saisie et validation des données.

La partie Contrôleur gère la dynamique de l'application. Elle fait le lien entre l'utilisateur et le reste de l'application.

### Interactions entre les composants

Le diagramme ci-dessous résume les relations entre les composants d'une architecture MVC.

{{% img mvc_symfony2.png %}}

La demande de l'utilisateur (exemple : requête HTTP) est reçue et interprétée par le contrôleur. Celui-ci utilise les services du modèle afin de préparer les données à afficher. Ensuite, le Contrôleur fournit ces données à la vue, qui les présente à l'utilisateur (par exemple sous la forme d'une page HTML).

{{% remark %}}
On peut trouver des variations de cette architecture dans lesquels la vue interagit directement avec le modèle afin de récupérer les données dont elle a besoin.
{{% /remark %}}

### Avantages et inconvénients

Le modèle MVC offre une séparation claire des responsabilités au sein d'une application, en conformité avec les principes de conception déjà étudiés : responsabilité unique, couplage faible et cohésion forte. Le prix à payer est une augmentation de la complexité de l'architecture.

Dans le cas d'une application Web, l'application du modèle MVC permet aux pages HTML (qui constituent la partie Vue) de contenir le moins possible de code serveur, étant donné que le scripting est regroupé dans les deux autres parties de l'application.

### Différences avec un modèle en couches

Attention à ne pas employer le terme de "couche" à propos du modèle MVC. Dans une architecture en couches, chaque couche ne peut communiquer qu'avec les couches adjacentes. Les parties Modèle, Vue et Contrôleur ne sont donc pas des couches.


# Itération 3 : intégration d'un framework PHP

Le but de cette itération est d'intégrer un *framework* à notre application.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
Tech_03 | L'architecture de l'application se base sur un *framework* PHP.

## Avantages apportés par un framework

En informatique comme ailleurs, il est rarement utile de réinventer la roue. La plupart des applications Web ont les mêmes besoins de base : accès au contenu de la requête HTTP reçue, création et renvoi de la réponse, gestions des sessions... Il existe une catégorie de logiciels dont le rôle est de gérer ces besoins communs : ce sont les **frameworks**.

Un framework fournit un ensemble de services de base, généralement sous la forme de classes en interaction. À condition de respecter l'architecture qu'il préconise (souvent une déclinaison du modèle MVC), un framework PHP libère le développeur de nombreuses tâches techniques comme le routage des requêtes, la sécurité, la gestion du cache, etc. Cela lui permet de se concentrer sur l'essentiel, c'est-à-dire ses tâches métier. Il existe une grande quantité de frameworks PHP. Parmi les plus connus, citons [Symfony](http://symfony.com/), [Zend Framework](http://framework.zend.com/) ou encore [Laravel](http://laravel.com/).

## Choix du framework

Il est possible d'écrire soi-même son propre framework, puis de le réutiliser dans tous ses projets PHP. C'est une tâche intéressante et formatrice, mais il est difficile d'obtenir le niveau de qualité et de sûreté que peut offrir un framework professionnel du marché. Si la construction d'un framework PHP vous intéresse, consultez le tutoriel [Evoluer vers une architecture MVC est PHP](http://bpesquet.developpez.com/tutoriels/php/evoluer-architecture-mvc/). Ici, nous allons utiliser un framework existant plutôt que d'en construire un nous-même.

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

{{% remark %}}
`__DIR__` est une [constante magique](http://php.net/manual/fr/language.constants.predefined.php) PHP qui contient le dossier du fichier courant.
{{% /remark %}}

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

## Conclusion

Nous avons refactorisé notre application Web pour intégrer le framework Silex et posé les bases d'une architecture robuste. Cependant, notre application profite encore peu des services que Silex peut fournir. Les prochaines itérations y remédieront.


# Itération 4 : refactorisation de l'accès aux données

Le but de cette itération est d'améliorer la partie Modèle de notre application Web.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
Tech_04 | Les données métier de l'application font l'objet d'une modélisation orientée objet.
Tech_05 | L'application est protégée contre le risque d'injection de code SQL dans la base de données.

## Modélisation objet du domaine

Actuellement, la partie Modèle de notre application Web est écrite de manière simpliste. Voici pour rappel le fichier source `model.php`.

    <?php
    
    // Return all articles
    function getArticles() {
        $bdd = new PDO('mysql:host=localhost;dbname=microcms;charset=utf8', 'microcms_user', 'secret');
        $articles = $bdd->query('select * from t_article order by art_id desc');
        return $articles;
    }

L'ajout futur de nouveaux services similaire risque de rendre la partie Modèle difficile à utiliser. Nous allons restructurer cette partie en introduisant une modélisation orientée objet des données métier. Pour l'instant, nos seules données métier sont les articles, qui se caractérisent pas un identifiant, un titre et un contenu. Nous allons modéliser un article sous la forme d'une classe nommée `Article` dont voici le diagramme UML. 

{{% image src="microcms_uml_article.jpeg" class="centered" %}}

la classe `Article` est ce qu'on appelle parfois (sans peur du ridicule) un POPO, ou *Plain Old PHP Objet* par analogie avec les [POJO](http://fr.wikipedia.org/wiki/Plain_Old_Java_Object) du monde Java. Autrement dit, cette classe ne contient rien de complexe : uniquement les propriétés et accesseurs nécessaires pour représenter un article.

Ecrivons maintenant cette classe en PHP. Si vous n'avez jamais utilisé PHP de manière orientée objet, je vous conseille les tutoriels des sites [openclassrooms](http://fr.openclassrooms.com/informatique/cours/programmez-en-oriente-objet-en-php) et [codecamedy](http://www.codecademy.com/fr/tracks/php).

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

## Conclusion

Cette itération nous a permis d'introduire une modélisation orientée objet du domaine et de l'accès aux données. Au passage, nous avons découvert comment Silex facilite l'inclusion de nouveaux services dans une application Web. C'est l'un des avantages de l'utilisation d'un framework.

Dans cette itération, nous avons surtout travaillé dans les parties Modèle et Contrôleur de notre application. L'itération suivante va s'intéresser à la partie Vue.


# Itération 5 : refactorisation de la présentation

Le but de cette itération est d'améliorer la technologie d'affichage de notre application.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
Tech_06 | L'application est protégée contre le risque d'injection de code dans les pages Web affichées.

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

## Conclusion

la partie Présentation de notre application Web est maintenant gérée par le moteur de remplates Twig. Cependant, le rendu utilisateur n'a pas évolué depuis l'initialisation de l'application et il reste sommaire. La prochaine itération va améliorer cela.

# Itération 6 : amélioration de la présentation

Le but de cette itération est de rendre l'affichage de notre application plus conforme aux standards actuels.

Voici la liste des éléments du *backlog* réalisés dans cette itération.

Référence | Description
----------|------------
User_U02 | En tant que visiteur anonyme, je peux accéder à l'application depuis un terminal fixe ou mobile et obtenir un affichage toujours adapté.

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

## Conclusion

Grâce à l'intégration de Bootstrap, les vues gérant l'affichage de notre application ont un aspect plus actuel et peuvent être écrites de manière adaptative. Leur rendu sera optimal quel que soit le terminal client utilisé.

Cette itération et les précédentes ont consisté en des améliorations techniques de l'application. La prochaine itération va (enfin !) lui ajouter une nouvelle fonctionnalité métier.
