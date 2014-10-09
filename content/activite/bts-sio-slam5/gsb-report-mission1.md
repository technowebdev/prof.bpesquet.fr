---
title: "GSB-Report : mission 1"
url: /activite/gsb-report-mission1
---

# Objectifs

* Comprendre le fonctionnement de la version initiale de GSB-Report.
* Ajouter à l'application les fonctionnalités de gestion des praticiens.

# Expression des besoins

Les nouveaux besoins associés à la gestion des praticiens sont les suivants :

* Consultation de la liste des praticiens. Les informations à afficher sont (dans cet ordre) : nom, prénom, ville et type de praticien.
* Affichage des détails sur un praticien. A l'exception de son identifiant, toutes les informations sur le praticien sont à afficher, ainsi que son type.
* Recherche de praticiens à partir de leur type.
* (BONUS) Recherche avancée de praticiens à partir de leurs nom et ville.

On attend un travail soigné jusque dans les détails : commentaires dans le code, orthographe correcte partout dans l'application, et surtout respect strict des choix effectués et du mode de fonctionnement existant. 

{{% important %}}
La version de l'application produite à la fin de cette mission doit donner l'impression d'avoir été réalisée par les mêmes développeurs que la version initiale, tant au niveau du code source que du résultat affiché à l'écran.
{{% /important %}}

La clé de la réussite consiste à comprendre le fonctionnement de la gestion des médicaments. Les fonctionnalités demandées pour les praticiens sont les mêmes et doivent être réalisées de la même manière.

# Organisation
Le travail est individuel. Le code source du projet est hébergé sur un dépôt GitHub nommé GSB-Report associé au compte GitHub du développeur. En fin de mission, une étiquette **mission1** est posée sur le code source.

# Etapes de travail

L'ordre ci-dessous doit impérativement être respecté.

1. Lire attentivement les documents présentant le contexte métier et l'application Web.
2. Créer le dépôt GitHub GSB-Report puis le cloner dans un dossier local.
3. Copier le code source de la version initiale de GSB-Report dans le dossier local.
4. Créer localement la base de données gsb, y ajouter la structure puis les données de test.
5. Faire les paramétrages Apache nécessaires pour définir un hôte virtuel.
6. Vérifier le bon fonctionnement de l'application GSB-Report en local.
7. Analyser le code source de l'application afin de comprendre son fonctionnement.
8. Ajouter à l'application les fonctionnalités demandées en les testant au fur et à mesure.
9. Commiter, pousser vers le dépôt GitHub et poser l'étiquette mission1 en fin de mission.
