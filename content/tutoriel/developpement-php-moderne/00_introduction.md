---
title: "Développement PHP moderne"
url: /tutoriel/developpement-php-moderne
showInMenus: true
---

Découvrez comment bâtir une application Web fonctionnelle et sûre en tirant le meilleur du langage PHP.

{{% warning %}}
Ce tutoriel est en cours d'écriture.
{{% /warning %}}

# Contexte et objectifs

## Pourquoi ce tutoriel

Le langage [PHP](http://php.net) est à l'heure actuelle le principal langage serveur du Web dynamique. Il souffre malgré tout d'un déficit d'image par rapport à des technologies concurrentes comme ASP.NET ou Java. Ces dernières imposent un cadre rigide qui guide et rassure le développeur. A l'inverse, PHP est une technologie très souple qui laisse beaucoup de liberté, y compris celle de faire un peu n'importe quoi. Lorsqu'on développe en PHP, il est donc essentiel de connaître et d'appliquer les meilleures pratiques.

PHP a évolué avec le temps et dispose à présent de fonctionnalités avancées parfois méconnues. Son écosystème est très riche et des milliers de projets cherchent à améliorer l'expérience du développeur PHP. Il n'est pas facile de se repérer dans cette jungle foisonnante pour choisir les bons outils.

Ce tutoriel vise à présenter une manière de concevoir une application Web en tirant parti des possibilités qu'offre le langage PHP et en s'appuyant sur des outils de son écosystème qui ont fait leurs preuves. En un mot, en utilisant PHP de manière **moderne**.

## Contexte choisi

Nous allons mettre en oeuvre les principes présentés dans ce tutoriel en construisant un exemple simple : une application Web de type [CMS](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_contenu). Notre micro-CMS d'exemple sera basique : il permettra de gérer une liste d'articles ainsi que les commentaires associés.

Le code source associé est disponible sous la forme d'un [dépôt GitHub](https://github.com/bpesquet/MicroCMS).

# Méthodologie de réalisation

En nous inspirant des [méthodes agiles](http://fr.wikipedia.org/wiki/M%C3%A9thode_agile) et notamment de [SCRUM](http://fr.wikipedia.org/wiki/Scrum_(m%C3%A9thode\)), nous allons bâtir l'application par étapes successives appelées **itérations**, ou encore [sprints](http://fr.wikipedia.org/wiki/Scrum_\(m%C3%A9thode\)#Le_sprint) dans SCRUM. 

{{% definition %}}
Une itération est une phase de travail volontairement courte permettant de produire une version souvent limitée mais toujours livrable d'un produit.
{{% /definition %}}

Certaines itérations seront consacrées à l'ajout de nouvelles fonctionnalités à l'application. Les autres permettront d'améliorer son architecture en pratiquant ce qu'on appelle la [refactorisation](http://fr.wikipedia.org/wiki/R%C3%A9usinage_de_code) (*refactoring*). 

# Fonctionnalités attendues

On regroupe dans les tableaux ci-dessous les fonctionnalités attendues de l'application que nous allons construire. En conformité avec la méthodologie agile choisie, nous exprimons les fonctionnalités métier sous la forme de [récits utilisateur](http://fr.wikipedia.org/wiki/R%C3%A9cit_utilisateur) (*user stories*).

## Récits utilisateur

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

## Récits techniques

Référence | Description
----------|------------
Tech_01 | L'application respecte une architecture de type MVC (Modèle-Vue-Contrôleur).
Tech_02 | L'application utilise une base de données relationnelle pour stocker ses données persistantes.
Tech_03 | L'application est protégée contre le risque d'injection de code SQL dans la base de données.
Tech_04 | L'application est protégée contre le risque d'injection de code JavaScript dans les pages affichées.

{{% remark %}}
Il existe un [débat](http://www.areyouagile.com/2013/03/pourquoi-une-user-story-technique-est-un-aveu-dechec/) concernant le bien-fondé de l'ajout de récits strictements techniques à un projet agile. Comme la valeur créée par notre projet d'exemple est avant tout d'ordre technique (apprendre à développer en PHP de manière moderne), cela ma paraît légitime ici.
{{% /remark %}}

## Carnet du produit

L'ensemble de ces récits forme ce qu'on appelle dans SCRUM le [carnet du produit](http://fr.wikipedia.org/wiki/Scrum_\(m%C3%A9thode\)#Carnet_du_produit_.28Product_Backlog.29) (*product backlog*). Chaque itération (sprint) va s'attacher à réaliser un ou plusieurs récits afin de vider progressivement le *backlog*, avec toujours l'idée d'obtenir en fin d'itération un produit livrable.

{{% remark %}}
Dans un contexte réel, le *backlog* évolue en même temps que le produit : nouveaux récits, bogues à corriger, etc.
{{% /remark %}}

# Liste des itérations

TODO

# Conclusion

TODO

