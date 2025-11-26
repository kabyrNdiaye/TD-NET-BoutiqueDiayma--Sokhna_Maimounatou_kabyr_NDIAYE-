# TD .NET - Boutique Diayma 2025/2026

**Étudiant** : Sokhna Maimounatou Kabyr NDIAYE  
**Département** : Génie Informatique, ESP/UCAD  
**Date** : 25 novembre 2025  
**Chargé de cours** : E. H. Ousmane Diallo  

## 2. Projets de la solution
La solution Diayma.sln contient 1 projet :
- P2FixAnAppDotNetCode\Diayma.csproj : Projet principal ASP.NET Core 2.0 (application web e-commerce avec contrôleurs MVC, vues Razor et ViewComponents pour panier/résumé).

## 3. Version SDK .NET utilisée par ces projets
Version : netcoreapp2.0 (.NET Core 2.0 – EOL, warnings sur support sécurité).
Extrait du Diayma.csproj :

(SDK 10.0.100 pour compilation ; runtime 2.0.9 pour exécution.)

## 6. Bugs trouvés lors de l'exploration
L'app s'ouvre sur http://localhost:62929. Flux testé : Accueil (produits), panier (ajout), résumé, commande.

1. **Bug 1 - Session Panier Perdue** : Articles ajoutés disparaissent après refresh.  
   Étapes : 1. Accueil > Add to Cart. 2. Refresh F5. 3. Panier vide.  
   Impact : Perte données (session non persistante en Core 2.0).

2. **Bug 2 - Erreur 500 Commande Vide** : Page commande crash si panier vide.  
   Étapes : 1. Panier vide. 2. /Order. 3. Erreur 500 (F12).  
   Impact : Pas de validation ; stack trace visible.

   ## 7. Lien vers l'exécutable
[Exécutable Windows self-contained (ZIP publish)](https://drive.google.com/file/d/1BYjJQzy6k5UXA_vbET8CCOIL69nDlq2G/view?usp=sharing)  
Détails : .NET Core 2.0 x86, portable (~100MB, lance Diayma.exe, testé localement sur http://localhost:5000).

## Optionnel 8a : Ajout Langue Wolof (Français Conservé)
J'ai ajouté la localisation pour Wolof (wo-SN) tout en conservant le français (fr-FR) comme défaut.

- **Config** : Dans Startup.cs, AddLocalization avec ResourcesPath = "Resources". SupportedCultures : fr-FR, wo-SN. Default : fr-FR.
- **Traductions** : Fichiers .resx dans Resources/Views/Product :
  - Index.fr.resx : "ProductList" = "Liste des produits", "Price" = "Prix", "AddToCart" = "Ajouter au panier".
  - Index.wo.resx : "ProductList" = "Ñuul ji", "Price" = "Lëng", "AddToCart" = "Yëg ak xëtu".
- **Vue** : Dans Views/Product/Index.cshtml, @inject IViewLocalizer Localizer + @Localizer["Clé"] pour titres/boutons.
- **Test** : App en français par défaut<a href="http://localhost:62929" target="_blank" rel="noopener noreferrer nofollow"></a>. Wolof : http://localhost:62929?culture=wo-SN (texte traduit).

Code exemple (Startup.cs) :

Merci !