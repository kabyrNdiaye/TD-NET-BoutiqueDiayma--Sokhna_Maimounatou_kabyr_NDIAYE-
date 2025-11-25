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