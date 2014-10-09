---
title: "GSB-Report : mission 2"
url: /activite/gsb-report-mission2
---

# Objectifs

* Ajouter la fonctionnalité d'authentification du visiteur.
* (Bonus) Permettre au visiteur connecté de mettre à jour ses informations personnelles.

# Expression des besoins

L'application actuelle n'est pas soumise à authentification. Il faut corriger ce problème et ne permettre l'accès qu'à un visiteur authentifié à l'aide de son nom d'utilisateur et de son mot de passe. 

La barre de navigation de l'application affiche (en haut à droite) un menu déroulant indiquant le statut de l'utilisateur :

* S'il n'est pas connecté, le menu affiche "Non connecté" et comporte un lien "Se connnecter" renvoyant vers le formulaire de connexion.
* S'il l'est, le menu déroulant affiche un message de bienvenue accompagné de son nom d'utilisateur. Le menu comporte un lien "Se déconnecter" permettant la déconnexion.

La version de l'application produite à la fin de cette mission doit donner l'impression d'avoir été réalisée par les mêmes développeurs que la version initiale, tant au niveau du code source que du résultat affiché à l'écran.

# Besoins optionnels (bonus)
La barre de navigation comporte un lien "Profil" qui permet au visiteur connecté de visualiser et de modifier ses informations personnelles. Les données à afficher sont : nom, prénom, adresse, code postal, ville, date d'embauche, nom d'utilisateur, mot de passe. Un message de confirmation s'affiche lorsque les modifications sont enregistrées.

# Organisation
Le travail est individuel. Le code source du projet est hébergé sur le dépôt GitHub GSB-Report associé au compte GitHub du développeur. En fin de mission, une étiquette **mission2** est posée sur le code source.
