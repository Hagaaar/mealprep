# Commande /mealprep

Tu es en train de générer le planning repas hebdomadaire de Hicham.

## Fichiers à lire avant de commencer
1. `directives.md` — règles nutritionnelles, ustensiles, contraintes
2. `history/*.json` — recettes des 8 dernières semaines (variété)

---

## PHASE 1 — LISTE COMPACTE (chat uniquement, ne rien pusher)

Format de réponse **strict et minimal** :

```
**Semaine XX — [dates]** | Lundi jeûne 🚫

Collations (Mar→Dim) :
• PRE ~10h : [description courte ex: porridge avoine + banane] ✅/🛒
• POST ~16h : Skyr 125g nature 🛒

6 recettes proposées :
1. **[Titre]** — [ingrédients principaux sans grammage, épices ✅]
2. **[Titre]** — ...
3. **[Titre]** — ...
4. **[Titre]** — ...
5. **[Titre]** — ...
6. **[Titre]** — ...

Budget estimé : XX.XX€ / 50€ ✅
Macros : ~2 017 kcal · ~170g P · ~132g G · ~90g L ✅
```

Règles de construction (internes, ne pas afficher) :
- Respecter la règle fraîcheur : recettes 1-3 = protéines fraîches, recettes 4-6 = conserves/sec
- Macros et budget vérifiés silencieusement avant affichage
- Si budget > 50€ : substituer automatiquement sans mentionner le dépassement
- Variété : aucune recette des 8 dernières semaines

---

## ATTENTE DE VALIDATION

Terminer par :

---
✅ **Planning prêt.** Modifications ? Réponds **VALIDE** pour générer le HTML et pusher.

---

## PHASE 2 — Déclenchée uniquement sur "VALIDE"

> **NE PAS DEMANDER DE CONFIRMATION.** Enchaîner immédiatement.

1. Assigner les 6 recettes aux jours Mardi→Dimanche (fraîches en début, conserves en fin).
2. Lire `.claude/design-system.md` pour les specs HTML.
3. Générer `index.html` complet avec tous les détails (grammages précis, macros, chef tips, courses interactives).
4. Sauvegarder `history/YYYY-WXX.json` :
```json
{
  "week": "2026-W24",
  "dates": "9-15 juin 2026",
  "recipes": [
    { "day": "Mardi", "name": "Nom recette", "protein": "poulet" },
    { "day": "Mercredi", "name": "Nom recette", "protein": "thon" }
  ]
}
```
5. Committer et pusher sur `main` : `meal plan semaine XX — [liste recettes]`

---

## Stock fourni par Hicham

$ARGUMENTS
