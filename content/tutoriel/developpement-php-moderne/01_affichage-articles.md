---
title: "Itération 1 : affichage de la liste des articles"
url: /tutoriel/developpement-php-moderne-01
draft: true
---

L'objectif de cette itération est d'écrire la toute première version de notre application Web d'exemple. Elle permettra d'afficher la liste des articles gérés par notre CMS.

# Création de la base de données des articles

Le rôle principal de notre CMS est de gérer des articles. Tous les articles sont sauvegardés dans une base de données relationnelle nommée `microcms`. Le SGBDR utilisé sera MySQL dans notre contexte. 

Un article est caractérisé par son titre (`art_title`) et son contenu (`art_content`). On modélise un article sous la forme d'un enregistrement dans une table nommée `t_article`. Le champ `art_id` est la clé primaire de cette table.

{{% image src="microcms_t_article.png" class="centered" %}}

On ajoute dans cette table un petit jeu de données de test.

    insert into t_article (art_title, art_content) values ('First article', 'Hi there! This is the very first article.');
    insert into t_article (art_title, art_content) values ('Some Lorem Ipsum', 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut hendrerit mauris ac porttitor accumsan. Nunc vitae pulvinar odio, auctor interdum dolor. Aenean sodales dui quis metus iaculis, hendrerit vulputate lorem vestibulum. Suspendisse pulvinar, purus at euismod semper, nulla orci pulvinar massa, ac placerat nisi urna eu tellus. Fusce dapibus rutrum diam et dictum. Sed tellus ipsum, ullamcorper at consectetur vitae, gravida vel sem. Vestibulum pellentesque tortor et elit posuere vulputate. Sed et volutpat nunc. Praesent nec accumsan nisi, in hendrerit nibh. In ipsum mi, fermentum et eleifend eget, eleifend vitae libero. Phasellus in magna tempor diam consequat posuere eu eget urna. Fusce varius nulla dolor, vel semper dui accumsan vitae. Sed eget risus neque.');

# Ecriture d'une première page PHP

A présent, écrivons la page PHP `index.php` qui affiche la liste de tous les articles. Voici son code source.

