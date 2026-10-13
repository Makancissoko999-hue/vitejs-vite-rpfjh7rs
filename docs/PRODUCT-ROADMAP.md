# MAKCISS CAPITAL — feuille de route produit

## Décision de lancement
- Marchés initiaux : ventes locales au Mali et en Espagne.
- Appareil de pilotage disponible : iPhone ; privilégier les outils web accessibles depuis mobile.
- Les ventes transfrontalières sont reportées après validation des ventes locales, des paiements et de la logistique.

## Étape 1 — Prototype de vitrine
- [x] Vitrine adaptative mobile/ordinateur.
- [x] Sélecteur de marché Mali / Espagne.
- [x] Recherche et filtres de catégories.
- [x] Panier de démonstration.
- [x] Parcours de commande simulé, sans paiement.
- [x] Espace vendeur informatif.
- [x] Mention explicite des données fictives et de l'absence de paiement réel.

## Étape 2 — Backend réel
- [ ] Authentification et récupération de compte.
- [ ] Rôles séparés : client, vendeur, livreur, administrateur.
- [ ] Base PostgreSQL avec politiques d'accès vérifiées côté serveur.
- [ ] Catalogue persistant, stocks et images produits.
- [ ] Commandes et transitions d'état contrôlées côté serveur.
- [ ] Journal d'audit des opérations sensibles.

## Étape 3 — Paiements et opérations
- [ ] Vérifier l'éligibilité des prestataires pour les paiements au Mali et en Espagne.
- [ ] Définir le modèle de versement vendeur sans conserver illicitement les fonds des tiers.
- [ ] Concevoir remboursements, rapprochement et gestion des paiements échoués.
- [ ] Piloter les livraisons locales et la preuve de remise.

## Étape 4 — Conformité et lancement
- [ ] Conditions de vente, confidentialité, retours et réclamations.
- [ ] Vérification vendeurs et règles produits interdits.
- [ ] Tests d'autorisations, sécurité, accessibilité et mobile.
- [ ] Commandes tests et lancement limité par zone.
- [ ] Étudier l'expédition transfrontalière seulement après validation des étapes locales.

## Limites actuelles
Le prototype utilise des produits et prix fictifs. Le panier reste en mémoire et aucun compte n'est créé. Aucun paiement, commande réelle, livraison, connexion à une base de données ou vérification de vendeur n'est activé. Il ne doit pas être présenté comme une marketplace en production.
