# mealprep — Instructions Claude

## Contexte
Repo de planning repas hebdomadaire pour Hicham (sèche, 2 017 kcal/j).

## Fichiers clés
- `directives.md` — règles nutritionnelles, contraintes cuisine, profil complet
- `history/` — historique des menus passés (JSON par semaine ISO) pour garantir la variété
- `index.html` — interface iPhone générée chaque semaine, pushée sur main
- `.claude/commands/mealprep.md` — slash command du workflow vendredi
- `.claude/commands/mealprep-ete.md` — variante canicule : que du froid (salades, jus), cuisson limitée au cuiseur à riz + Air Fryer, four/plaques interdits

## Workflow habituel
Chaque vendredi ~20h, Hicham tape `/mealprep` suivi de son stock dans le chat.
Le slash command gère tout : Phase 1 (proposition + validation) → Phase 2 (génération HTML + push).

## Règle variété (critique)
Avant toute proposition, lire tous les fichiers `history/*.json` et ne jamais reprendre une recette utilisée dans les 8 dernières semaines.

## Règle affichage 2 semaines (critique)
Quand le planning couvre 2 semaines, l'onglet Recettes doit **toujours afficher les deux semaines en même temps, intégralement** (14 jours détaillés, séparés par un repère de semaine). Interdit d'afficher une seule semaine et de réserver la seconde pour "la semaine prochaine" — c'était l'ancien comportement, il est abandonné. Seuls les accordéons par jour restent repliables/dépliables individuellement.

## Règle génération complète & achats groupés (critique)
Que la commande porte sur 1 ou 2 semaines, **tout doit être généré intégralement pour toute la période dès la validation** — recettes, courses ET stockage, sans rien différer. Le stock donné en début de commande sert à couvrir toute la période demandée.

Pour 2 semaines, l'intérêt est aussi économique : acheter en grande quantité réduit le prix à l'unité (surtout produits secs, conserves, épicerie). Donc :
- Les courses restent réparties en **deux sessions séparées** (samedi S1 et samedi S2) car les produits frais (viande, légumes) ne se conservent pas 2 semaines.
- Mais pour les produits secs/conserves/épicerie qui se conservent, acheter dès S1 la quantité couvrant les 2 semaines quand c'est plus économique, et marquer ces articles en S2 comme "en stock — acheté S1" (déjà comptés dans le budget S1) plutôt que de les racheter.
- Les recettes de S2 peuvent explicitement réutiliser des ingrédients achetés en gros pendant les courses S1 (cohérent avec l'onglet Stockage qui trace déjà les restes de S1 utilisés en S2).

## Push
Toujours pusher sur `main` (pas sur une branche feature) après validation explicite "VALIDE" de Hicham.
