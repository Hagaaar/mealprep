# mealprep — Instructions Claude

## Contexte
Repo de planning repas hebdomadaire pour Hicham (sèche, 2 017 kcal/j).

## Fichiers clés
- `directives.md` — règles nutritionnelles, contraintes cuisine, profil complet
- `history/` — historique des menus passés (JSON par semaine ISO) pour garantir la variété
- `index.html` — interface iPhone générée chaque semaine, pushée sur main
- `.claude/commands/mealprep.md` — slash command du workflow vendredi

## Workflow habituel
Chaque vendredi ~20h, Hicham tape `/mealprep` suivi de son stock dans le chat.
Le slash command gère tout : Phase 1 (proposition + validation) → Phase 2 (génération HTML + push).

## Règle variété (critique)
Avant toute proposition, lire tous les fichiers `history/*.json` et ne jamais reprendre une recette utilisée dans les 8 dernières semaines.

## Push
Toujours pusher sur `main` (pas sur une branche feature) après validation explicite "VALIDE" de Hicham.
