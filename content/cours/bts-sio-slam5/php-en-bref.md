---
title: "Le langage PHP en bref"
url: /cours/php-en-bref
---

# Introduction

Commençons par une définition de PHP issue de Wikipedia :

> "PHP: Hypertext Preprocessor, plus connu sous son sigle PHP (acronyme récursif), est un langage de scripts libre principalement utilisé pour produire des pages Web dynamiques via un serveur HTTP, mais pouvant également fonctionner comme n'importe quel langage interprété de façon locale, en exécutant les programmes en ligne de commande. PHP dispose depuis la version 5 de fonctionnalités objet complètes. En raison de la richesse de sa bibliothèque, on désigne parfois PHP comme une plate-forme plus qu'un simple langage."

Il y a beaucoup d'informations dans ces quelques lignes, les plus importantes sont mises en évidence dans le texte :

* PHP est un langage **libre** (et gratuit).
* Il est principalement utilisé sur le Web pour générer des pages **dynamiques**.
* C'est un langage **interprété** et non compilé comme Java ou C#.
* Depuis la version 5, il peut être utilisé de manière **orientée objet**.
* Il existe autour de PHP un **écosystème** très riche (bibliothèques, CMS, frameworks, etc).

# Histoire de PHP

Le langage PHP fut créé en 1994 par Rasmus Lerdorf pour son site web. C'était à l'origine une bibliothèque logicielle écrite d'abord en langage Perl, pluis en langage C. Il s'en servait pour conserver une trace des visiteurs qui venaient consulter son CV. PHP signifiait alors Personal Home Page tools. Le code source de PHP fut publié par son auteur en 1996. En 1997, deux étudiants, Andi Gutmans et Zeev Suraski, redéveloppèrent le cœur de PHP puis son moteur interne, aboutissant à ce qu'on appelle le Zend Engine.

Les versions du langage se sont succédées depuis, apportant leur lot d'améliorations et corrigeant les (nombreuses) failles de sécurité apparues en chemin. La version 5 de PHP, sortie en 2004, utilise Zend Engine 2 et introduit un véritable modèle objet, une gestion des erreurs fondée sur le modèle des exceptions, ainsi que des fonctionnalités de gestion pour les entreprises.

Contrairement à des langages comme Java et C#, pensés par des armées d'ingénieurs chez Sun Microsystems et Microsoft, PHP a émergé du Web à partir d'une idée personnelle, puis a évolué au fur et à mesure des besoins. Cela explique le côté un peu confus du langage et certaines mauvaises décisions de design, qui ont eu des conséquences néfastes en termes de sécurité. C'est aussi pour cela que l'offre logicielle autour de PHP est si riche et adaptée à pratiquement tous les besoins.

# Fonctionnement de PHP

Même s'il peut être utilisé en ligne de commande, PHP est principalement associé à un serveur Web utilisant le protocole HTTP dans le cadre d'une architecture client/serveur.

{{% image src="php_fonctionnement.png" class="centered" %}}

1. Le client, le plus souvent un navigateur Web, fait la demande au serveur d'une page PHP au travers du protocole HTTP.
2. Le serveur HTTP envoie la page PHP à son interpréteur.
3. L'interprétation de la page PHP produit une page HTML de résultat fournie au serveur.
4. Le serveur Web renvoie cette page au client pour affichage.

{{% danger %}}
Attention à ne pas ouvrir directement une page PHP dans un navigateur (URL de type `file://`) au lieu d'en faire la demande à un serveur Web (URL de type `http://`).
{{% /danger %}}

Souvent, le code de la page PHP utilise les données stockées dans une base de données afin de générer le résultat HTML. On se trouve alors en présence d'une architecture **trois-tiers** (navigateur Web, serveur Web/interpréteur PHP, SGBD). Les tiers serveur Web et SGBD peuvent être hébergés sur des machines distinctes ou regroupés sur une machine unique. Dans ce cas d'une machine unique sous Linux avec Apache comme serveur Web et MySQL comme SGBD, on obtient ce qu'on appelle un serveur **LAMP**.

# Principales caractéristiques de PHP

La page PHP ci-dessous offre un aperçu des principales caractéristiques du langage.

    <!doctype html>
    <html lang="fr">
        <head>
            <meta charset="utf-8" />
            <title>Ma page de démonstration PHP</title>
        </head>
        <body>
            <?php
            $prenom = "Bill";
            $classe = 'BTS SIO';
            $langages = array('C#', 'Java', 'ASP.NET', 'PHP');
            $nbLangages = count($langages);
            $qualite = "débutant";
            if ($nbLangages == 4) {
                $qualite = "débrouillé";
            }
            elseif ($nbLangages > 4) {
                $qualite = "aguerri";
            }
            ?>
            <h1>Ma présentation</h1>
            <p>Bonjour, je m'appelle <?php echo "$prenom" ?> et je suis en <?php echo "$classe" ?>.</p>
            <?php
            echo 'Je suis un programmeur ' . $qualite . '. ';
            echo 'Je connais ' . $nbLangages . ' langages de programmation :</p>';
            ?>
            <ul>
                <?php
                foreach ($langages as $langage) {
                    echo "<li>$langage</li>";
                }
                ?>
            </ul>
        </body>
    </html>

On peut faire les observations suivantes :

* On définit une portion de code PHP gràce aux balises `<?php` et `?>`.
* Les variables sont préfixées par le symbole `$` et leur typage est dynamique, contrairement à des langages comme C# ou Java où le typage est statique.
* On peut construire un résultat HTML en mélangeant balises HTML et code PHP, ou bien en utilisant l'instruction PHP `echo` pour générer les balises HTML.

# Compléments sur PHP

## Affichage abrégé

Dans une page PHP, il est possible de remplacer `<?php echo ... ?>` par `<?= ... ?>` pour un résultat identique. Cette alternative à `echo` permet d'alléger le code de la page PHP. Elle est surtout utile dans les pages qui mélangent PHP et HTML. Voici un extrait de la page précédente, réécrit en utilisant cette syntaxe.

    <?php
    $prenom = "Bill";
    $classe = 'BTS SIO';
    ?>
    <h1>Ma présentation</h1>
    <p>Bonjour, je m'appelle <?= $prenom ?> et je suis en <?= $classe ?>.</p>

{{% remark %}}
Depuis PHP 5.4, cette syntaxe est toujours disponible. Avec les versions précédentes, elle nécessite l'activation de la directive `short_open_tag` dans le fichier de configuration de PHP.
{{% /remark %}}

## Syntaxe alternative pour les structures de contrôle

PHP propose une autre manière de rassembler des instructions à l'intérieur d'un bloc, pour les structures de contrôle `if`, `while`, `for`, `foreach` et `switch`. Dans chaque cas, le principe est de remplacer l'accolade d'ouverture par deux points (`:`) et l'accolade de fermeture par, respectivement, `endif;`, `endwhile;`, `endfor;`, `endforeach;` ou `endswitch;`.

Voici le même exemple écrit avec la syntaxe classique puis la syntaxe alternative.

    <?php if (!isset($user)) { ?>
        <p>Veuillez vous connecter</p>
    <?php }
    else { ?>
        <h2>Bienvenue <?= $user ?></h2>
        <span>Vous avez <?= count($messages) ?> messages en attente</span>
        <?php foreach ($messages as $message) { ?>
            <p><?= $message ?></p>
        <?php } ?>
    <?php } ?>

\

    <?php if (!isset($user)): ?>
        <p>Veuillez vous connecter</p>
    <?php else: ?>
        <h2>Bienvenue <?= $user ?></h2>
        <span>Vous avez <?= count($messages) ?> messages en attente</span>
        <?php foreach ($messages as $message): ?>
            <p><?= $message ?></p>
        <?php endforeach; ?>
    <?php endif; ?>

Plus le code HTML devient long, plus il devient difficile de savoir quel bloc PHP est fermé par la ligne `<?php } ?>`. La syntaxe alternative permet d'utiliser des structures de contrôles avec la même sémantique (et aussi la même indentation) que le code HTML. Tout comme l'affichage abrégé, elle est surtout utile dans les pages qui mélangent HTML et PHP.
