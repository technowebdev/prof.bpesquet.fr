---
title: "Le modèle MVC"
url: /cours/modele-mvc
---

# Présentation

Le modèle MVC décrit une manière d'architecturer une application informatique en la décomposant en trois sous-parties :

* la partie **Modèle** ;
* la partie **Vue** ;
* la partie **Contrôleur**.

Ce modèle de conception (*design pattern*) a été imaginé à la fin des années 1970 pour le langage Smalltalk afin de bien séparer le code de l'interface graphique de la logique applicative. Il est utilisé dans de très nombreux langages : bibliothèques Swing et Model 2 (JSP) de Java, frameworks PHP, ASP.NET MVC, etc.

# Rôles des composants

La partie **Modèle** d'une architecture MVC encapsule la logique métier (*business logic*) ainsi que l'accès aux données. Il peut s'agir d'un ensemble de fonctions (Modèle procédural) ou de classes (Modèle orienté objet).

La partie **Vue** s'occupe des interactions avec l'utilisateur : présentation, saisie et validation des données.

La partie **Contrôleur** gère la dynamique de l'application. Elle fait le lien entre l'utilisateur et le reste de l'application.

# Interactions entre les composants

Le diagramme ci-dessous (extrait de la documentation du framework [Symfony](http://symfony.com/)) résume les relations entre les composants d'une architecture MVC.

{{% img mvc_symfony2.png %}}

La demande de l'utilisateur (exemple : requête HTTP) est reçue et interprétée par le Contrôleur. Celui-ci utilise les services du Modèle afin de préparer les données à afficher. Ensuite, le Contrôleur fournit ces données à la Vue, qui les présente à l'utilisateur (par exemple sous la forme d'une page HTML).

{{% remark %}}
On peut trouver des variantes moins "pures" de cette architecture dans lesquelles la Vue interagit directement avec le Modèle afin de récupérer les données dont elle a besoin.
{{% /remark %}}

# Avantages et inconvénients

Le modèle MVC offre une séparation claire des responsabilités au sein d'une application, en conformité avec les principes de conception déjà étudiés : responsabilité unique, couplage faible et cohésion forte. Le prix à payer est une augmentation de la complexité de l'architecture.

Dans le cas d'une application Web, l'utilisation du modèle MVC permet aux pages HTML (qui constituent la partie Vue) de contenir le moins possible de code serveur, étant donné que le scripting est regroupé dans les deux autres parties de l'application.

# Différences avec un modèle en couches

Attention à ne pas employer le terme de "couche" à propos du modèle MVC. Dans une architecture en couches, chaque couche ne peut communiquer qu'avec les couches adjacentes. Les parties Modèle, Vue et Contrôleur ne sont donc pas des couches.
