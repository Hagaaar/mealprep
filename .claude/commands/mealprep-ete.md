# /mealprep-ete

Variante estivale (canicule) de `/mealprep`. Mêmes règles de `directives.md` (profil, macros, entraînement, budget, exclusions, favoris, historique 8 semaines) et **exactement le même déroulé Phase 1 → validation → Phase 2** que `.claude/commands/mealprep.md`, à l'exception des règles cuisine ci-dessous qui les remplacent pour toute la durée du planning généré.

## Règles ÉTÉ (override cuisine — remplace la section "Ustensiles" et "Structure des repas / cuisson" de `directives.md`)

- 🚫 **Aucun repas chaud.** Repas midi et soir (toujours identiques entre eux) sont servis **froids** uniquement : salades composées, bowls froids, poke bowls, wraps froids, etc.
- ✅ **Seules cuissons autorisées** : riz au **cuiseur à riz**, et éventuellement une cuisson ponctuelle à l'**Air Fryer** (protéine/légumes) — à laisser refroidir avant de composer le plat froid.
- 🚫 **Four traditionnel et plaques/poêle/casserole strictement interdits** (renforce l'interdiction déjà présente dans `directives.md`).
- 🚫 Cocotte et tajine non utilisés en mode été (cuisson longue → incompatible avec un plat froid).
- ⭐ **Préférence** pour les salades composées (protéine + riz froid + légumes crus/marinés + sauce) et les **jus/smoothies maison** — à privilégier notamment pour varier les collations PRE/POST training (jus pressé maison en alternative ponctuelle au Skyr, selon le stock disponible).

Tout le reste reste identique à `/mealprep` : glucides ≥100g/j, budget ≤50€/semaine, pas de porc, jeûne total lundi, alternance stricte Force/Cardio, fraîcheur courses (fraîche Mar-Jeu, conserves Ven-Dim), sauces/épices obligatoires à chaque plat, priorité `liked-recipes.json`, règle des 8 semaines, règle affichage 2 semaines intégral, règle génération complète + achats groupés.

## Déroulé

Suivre à la lettre **Phase 1** puis **Phase 2** telles que décrites dans `.claude/commands/mealprep.md` (format de proposition, validation "VALIDE", modification `index.html`, sauvegarde `history/*.json`, commit + push sur `main`), avec deux adaptations :
- Dans chaque `.meal-time` de repas principal, mentionner systématiquement `[Froid]` (jamais `[Chaud]`).
- L'ustensile mentionné est limité à `Cuiseur à riz` et/ou `Air Fryer`.

**Format d'appel identique :** première ligne de $ARGUMENTS = nombre de semaines (`1` ou `2`), reste = stock.

## Stock

$ARGUMENTS
