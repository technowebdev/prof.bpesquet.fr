---
title: "Projet AdresseIP"
url: /activite/projet-adresse-ip
---

# Objectif

Ce projet a pour objectif d'analyser une adresse IPv4 saisie par l'utilisateur.

L'adresse IP sera modélisée sous la forme d'une classe `AdresseIP` dont voici le diagramme initial (seuls les membres publics sont affichés).

{{% image src="SLAM2_AdresseIP.png" class="centered" %}}

Le programme principal fait saisir les 4 octets de l'adresse, puis vérifie sa validité et affiche sa valeur binaire si elle est valide.

{{% image src="slam2_adresseip_valbin.png" class="centered" %}}

{{% image src="slam2_adresseip_invalid.png" class="centered" %}}

Vous trouverez plus bas le code source permettant de convertir un octet du décimal vers le binaire.

**BONUS** : ne pas utiliser ce code source.

# Etapes de travail

1. Créez une nouvelle solution Visual Studio nommée **AdresseIP**.
2. Ajoutez à cette solution une application console nommée **AppIP**.
3. Ajoutez à cette solution une bibliothèque de classes nommée **LibIP**.
4. Créez dans **LibIP** une nouvelle classe nommée `AdresseIP`.
5. Codez les fonctionnalités demandées en les testant au fur et à mesure.

# Bonus

* Calculer et afficher la classe de l'adresse. Valeurs possibles : A, B, C, D, E.
* Calculer et afficher le type de l'adresse. Valeurs possibles : Publique, Privée, Réseau, Diffusion, Réservée, Multicast, Expérimentale.

{{% image src="slam2_adresseip_bonus.png" class="centered" %}}

Le tableau ci-dessous regroupe quelques résultats possibles qui vous permettront de tester votre application.

Adresse | Classe | Type
--------|--------|-----
10.0.0.0 |A|Réseau
10.0.0.1 |A|Privée
127.0.0.1 |A|Réservée
172.16.0.0 |B|Réseau
172.16.100.0 |B|Privée
172.32.100.0 |B|Publique
192.100.100.254 |C|Publique
192.100.100.255 |C|Diffusion
225.0.0.1 |D|Multicast
240.0.0.1 |E|Expérimentale

# Annexe : code source de la méthode ConvertirEnBinaire

```csharp
/// <summary>
/// Calcule la valeur binaire d'un octet décimal
/// </summary>
/// <param name="valeurDecimale">L'octet sous forme décimale</param>
/// <returns>L'octet sous forme binaire</returns>
private string ConvertirEnBinaire(int valeurDecimale)
{
    string resultat = "";

    // Méthode de la division
    // On divise le nombre décimal par 2 jusqu'à ce que le quotient soit nul
    // Les restes de chaque division constituent la valeur binaire
    int d = valeurDecimale;
    int r;
    int nbBits = 0;
    string valeurBit;
    while (d > 0)
    {
        r = d % 2;
        d = d / 2;
        if (r != 0)
            valeurBit = "1";
        else
            valeurBit = "0";
        // On ajoute le bit résultat au début de la chaîne
        resultat = valeurBit + resultat;
        nbBits++;
    }
    // On complète la valeur binaire avec des 0 pour obtenir 8 bits
    for (int i = nbBits; i < 8; i++)
        resultat = "0" + resultat;

    return resultat;
}
```
