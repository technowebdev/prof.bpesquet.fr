---
title: "Premiers pas avec le framework PHP Silex"
date: 2014-06-20
---

Ce tutoriel vise à se familiariser avec le framework PHP [Silex](http://silex.sensiolabs.org/) au travers de l'écriture d'une application Web basique.

{{% image src="silex-logo.png" class="centered" %}}

# Pré-requis

* Connaître les bases du langage PHP.
* Disposer d'une machine de développement incluant le serveur Web Apache.


# Présentation de Silex

[Silex](http://silex.sensiolabs.org/) est un micro-framework PHP développé par la société française [Sensio Labs](http://sensiolabs.com/), créatrice du framework [Symfony](http://symfony.com/). Silex est en quelque sorte le petit frère de Symfony et les deux frameworks reposent sur les mêmes composants.

Contrairement à Symfony qui fournit (et impose) une architecture complète (dite *full stack*), Silex est un framework minimaliste qui laisse beaucoup de liberté au développeur. C'est pourquoi on peut le qualifier de **micro-framework**. Il fournit un ensemble réduit de services au-dessus desquels on peut développer une application Web. Son minimalisme le rend idéal pour s'initier en douceur au fonctionnement d'un framework PHP.

Silex dispose d'une [documentation en ligne](http://silex.sensiolabs.org/documentation) assez complète. Dans ce turoriel, nous allons nous contenter de l'utiliser pour afficher un simple message "Hello world" à l'utilisateur.


# Installation de Silex

L'installation de Silex peut s'effectuer de deux manières :

* En téléchargeant une archive du code source, disponible [ici](http://silex.sensiolabs.org/download).
* En utilisant le gestionnaire de dépendances [Composer](https://getcomposer.org/).

Nous allons utiliser la seconde solution, plus formatrice : Composer est un outil essentiel que tout développeur PHP sérieux se doit de connaître. 

## Introduction à Composer

Composer est un outil qui permet de définir des **dépendances** entre des projets PHP (exemple : "mon projet a besoin de Silex") et de récupérer automatiquement les fichiers associés. 

Pour fonctionner, Composer doit être installé sur la machine de développement. Vous trouverez plus de détails, ainsi que la procédure d'installation, en consultant sa [documentation](https://getcomposer.org/doc/00-intro.md). Je vous conseille d'effectuer une installation globale afin que la commande `composer`soit disponible en ligne de commande. Vous pouvez le vérifier en ouvrant une fenêtre de terminal puis en tapant simplement :

    $ composer

Si l'installation de Composer a réussi, vous obtenez la description des options utilisables.


## Création du fichier de dépendances

Une fois Composer installé, il faut créer un fichier de dépendances pour exprimer le fait que notre projet a besoin de Silex pour fonctionner. 

Dans un premier temps, nous allons travailler directement dans le répertoire servi par votre serveur Web local. Son emplacement dépend de votre installation. Voici quelques emplacements possibles : 

* `c:\xampp\htdocs` sous Windows.
* `/var/www` sous Linux.
* `/Applications/MAMP/htdocs`sous Mac. 

Créez dans ce répertoire un sous-répertoire nommé `hello-world-silex` qui sera le répertoire racine de notre application Web. Déplacez-vous dans ce répertoire puis créez un fichier texte nommé `composer.json`. Ensuite, copiez-collez le texte ci-dessous dans ce fichier.

    {
        "require": {
            "silex/silex": "~1.2"
        }
    }

Ce fichier va être lu par Composer, qui va en déduire que le projet courant nécessite Silex (plus précisément : une version de Silex au moins égale à 1.2 et inférieure à 2.0) et va récupérer automatiquement les fichiers nécessaires.

## Récupération de Silex via Composer

Ouvrez une fenêtre de terminal et déplacez-vous dans le répertoire `hello-world-silex` créé plus haut. Ensuite, lancez la commande ci-dessous :

    $ composer install

Si tout va bien, Composer va télécharger les fichiers de Silex dans un sous-répertoire nommé `vendor` du répertoire courant. Pourquoi ce nom ? Il s'agit d'une convention standard : dans un projet PHP, le répertoire `vendor` rassemble le code issu de projets tiers.

{{% img composer-install-silex.png %}}

Voici à présent l'arborescence de notre projet. On vérifie au passage que Silex repose sur certains composants du framework Symfony, regroupés dans le sous-répertoire `symfony` du répertoire `vendor`.

{{% img silex-vendor-directory-structure.png %}}

Si vous êtes curieux(se), c'est le moment d'aller examiner le code source de ces composants... Heureusement, cette étape n'est pas indispensable pour utiliser Silex ou Symfony.


# Aperçu du fonctionnement de Silex

## Un premier exemple

Maintenant que Silex est installé, il est temps de voir comment l'utiliser. Pour cela, créez dans `hello-world-silex` un sous-répertoire `web`, puis créez dans `web` un fichier `index.php`. Copiez/collez le code ci-dessous dans `index.php`.

    // web/index.php
    <?php

    require_once __DIR__.'/../vendor/autoload.php';
    
    $app = new Silex\Application();
    
    $app->get('/', function () {
        return 'Hello world';
    });
    
    $app->run();

Le fichier `vendor/autoload.php` est généré automatiquement par Composer. En l'incluant dans notre fichier source au moyen de l'instruction PHP [require_once](http://php.net/manual/fr/function.require-once.php), on peut ensuite utiliser tous les éléments PHP définis dans les sous-répertoires de `vendor`. L'intérêt de cette pratique est expliqué dans [cet article](https://igor.io/2013/09/04/composer-vendor-directory.html).

Le reste du code source de `index.php` instancie un objet nommé `$app`, puis définit ce qu'on appelle une **route**.

{{% definition %}}
Une route est un point d'entrée dans une application Web. Elle définit une correspondance entre une URL et une action de l'application.
{{% /definition %}}

La route définie ici renvoie le texte "Hello world" lorsque l'URL racine de l'application (`/`) est demandée. La syntaxe utilisée pour définir l'action peut sembler déroutante à première vue. Il s'agit d'une **fermeture** (*closure*), une fonction définie à l'intérieur du corps d'une autre fonction. Ce concept existe dans de [nombreux langages](http://fr.wikipedia.org/wiki/Fermeture_(informatique).

## Test de l'exemple

Afin de contrôler que notre exemple fonctionne, vérifiez que votre serveur Web local est lancé puis tapez l'URL http://localhost/hello-world-silex/web/index.php dans votre navigateur Web favori. 

Vous devriez obtenir l'affichage du texte "Hello world" dans le navigateur.


## Initiation au routage avec Silex

Pour l'instant, notre application Web ne dispose que d'un point d'entrée. Ajoutons-en un autre en définissant une nouvelle route dans le fichier `index.php`.

    // ...
    $app->get('/hello/{name}', function ($name) use ($app) {
        return 'Hello ' . $app->escape($name);
    
    $app->run();

Cette nouvelle route correspond à une URL de type `/hello/nom`. La partie de l'URL située après `/hello/` est passée à l'action sous la forme d'un paramètre nommé `$name`.

L'action associée à la nouvelle route construit le message affiché par concaténation. L'URL `/hello/Bob` affichera le message "Hello Bob". Elle utilise la méthode [escape](http://silex.sensiolabs.org/api/Silex/Application.html#method_escape), qui permet d'éviter les [injections de code](http://fr.wikipedia.org/wiki/Injection_de_code_dans_les_applications_web) dans le résultat généré. 

Pour tester la nouvelle route, pointez votre navigateur vers http://localhost/hello-world-silex/web/index.php/hello/Bob et vérifiez que vous obtenez le message prévu.


# Simplification des URLs

Vous aurez noté que les URLs de notre application Web commencent toutes par `/web/index.php`, ce qui est peu pratique. Plutôt que devoir écrire http://localhost/hello-world-silex/web/index.php/hello/Bob, on aimerait pouvoir écrire http://localhost/hello-world-silex/hello/Bob.

Nous allons aller plus loin et faire en sorte que l'application réponde à une URL de la forme http://hello-world-silex/hello/Bob. Cela nécessite de modifier la configuration du serveur Web local, qui sera Apache dans notre exemple.

## Définition d'un hôte virtuel

La première étape est de définir un **hôte virtuel** (*virtual host*). Le principe des hôtes virtuels est de définir plusieurs serveurs logiques sur un même serveur physique. Vous trouverez tous les détails sur les hôtes virtuels dans la [documentation Apache](https://httpd.apache.org/docs/current/fr/vhosts/).

La configuration d'un hôte virtuel sous Apache nécessite l'édition du fichier de configuration `httpd-vhosts.conf`. Son emplacement dépend de l'installation d'Apache : 

* `c:\xampp\apache\conf\extras` avec XAMPP sous Windows.
* `/Applications/MAMP/conf/apache/extras` avec MAMP sous Mac.

Ouvrez ce fichier avec un éditeur de texte puis ajoutez le contenu ci-dessous à la fin en adaptant les lignes commençant par `DocumentRoot`et `Directory` à votre configuration locale.

    <VirtualHost *:80>
        DocumentRoot "C:\xampp\htdocs"
        ServerName localhost
    </VirtualHost>  

    <VirtualHost *:80>
        DocumentRoot "C:\xampp\htdocs\hello-world-silex\web"
        ServerName hello-world-silex
        <Directory "C:\xampp\htdocs\hello-world-silex\web">
            AllowOverride all
        </Directory>
    </VirtualHost>

Le premier hôte virtuel redéfinit `localhost`, ce qui est nécessaire quand on rajoute des hôtes virtuels sous Apache. Le second crée un hôte virtuel associé au nom `hello-world-silex` et dont la racine est le répertoire `hello-world-silex/web`.

{{% remark %}}
Pour que la nouvelle configuration soit prise en compte, il faut redémarrer le serveur Web Apache.
{{% /remark %}}

Dans un second temps, il faut ajouter une information au fichier `hosts` local pour que la résolution DNS pointe sur la machine locale (127.0.0.1). Là encore, l'emplacement de ce fichier dépend de votre système : 

* `C:\Windows\System32\drivers\etc\hosts` sous Windows.
* `/private/etc/hosts`sous Mac.

{{% remark %}}
La modification de ce fichier nécessite des droits d'administrateur.
{{% /remark %}}

Editez ce fichier afin d'y ajouter la ligne ci-dessous.

    127.0.0.1   hello-world-silex

Une fois le fichier `hosts` modifié et Apache redémarré, l'application doit répondre à l'URL http://hello-world-silex avec le message "Hello world".

## Reécriture des URLs à la volée

Si vous tentez maintenant d'accéder à l'URL http://hello-world-silex/hello/Bob, vous obtenez un message d'erreur de notre navigateur. Afin de rendre ce type d'URL fonctionnel, il faut rediriger toutes les requêtes entrantes vers le fichier `index.php` écrit précédemment. 

Sous Apache, cela passe par la définition d'un fichier de réécriture d'URL (*URL rewriting*) nommé `.htaccess` et situé dans le répertoire `hello-world-silex/web`. Créez ce fichier puis copiez/collez-y le texte ci-dessous.

    # Redirect incoming URLs to index.php
    <IfModule mod_rewrite.c>
        Options -MultiViews

        RewriteEngine On
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteRule ^ index.php [QSA,L]
    </IfModule>

A présent, l'URL http://hello-world-silex/hello/Bob doit afficher le message de bienvenue. Notre application Web est fonctionnelle !

# Conclusion

Dans ce tutoriel, nous avons posé les bases d'une application Web utilisant le framework PHP Silex. Les étapes essentielles de l'installation de Silex et de la configuration du serveur Web sont réalisées. Il ne reste plus qu'à enrichir l'application en lui ajoutant des routes ainsi que les actions associées. 

Cette évolution sera aisée : l'un des intérêts d'un micro-framework comme Silex est qu'il est très facile d'ajouter à l'application Web de nouveaux services (exemples : gestion de la persistance, de la sécurité, moteur de *templates*) et d'améliorer son architecture afin de répondre aux besoins qui apparaîtront pendant le cycle de vie du logiciel.
