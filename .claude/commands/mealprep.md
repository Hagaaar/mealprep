# Commande /mealprep

Tu es en train de générer le planning repas hebdomadaire de Hicham.

## Fichiers à lire avant de commencer
1. `directives.md` — règles nutritionnelles, ustensiles, contraintes
2. `history/*.json` — recettes des 8 dernières semaines (variété)

---

## PHASE 1 — PROPOSITION COMPACTE (chat uniquement, ne rien pusher)

### Format de réponse Phase 1 — STRICT

**Ligne d'entête :** `SEMAINE XX — [dates] | Lundi JEÛNE 🚫`

**Tableau des 6 recettes :**
```
| Jour     | Recette              | Ustensile  | Ingrédients clés à acheter        |
|----------|----------------------|------------|------------------------------------|
| Mar 💪   | [Nom recette]        | Air Fryer  | [protéine Xg 🛒], [féculents 🛒]  |
| Mer 🏃   | [Nom recette]        | Cocotte    | ...                                |
| Jeu 💪   | [Nom recette]        | Tajine     | ...                                |
| Ven 💪   | [Nom recette]        | Cocotte    | ...                                |
| Sam 🏃   | [Nom recette]        | Cocotte    | ...                                |
| Dim 🏃   | [Nom recette]        | Cocotte    | ...                                |
```

**Variété :** `✅ Aucune répétition` OU liste des conflits.

**Liste de courses (format compact) :**
```
BOUCHERIE : [article Xg ~X.XX€] · [article ~X.XX€]
CONSERVES  : [article ~X.XX€] · ...
SEC/ÉPICERIE : ...
F&L : ...
FRAIS : ...
TOTAL : XX.XX€ / 50.00€ ✅
```
Si total > 50€ → substituer automatiquement (viande fraîche → légumineuses) et recalculer.

**Macros globales (1 ligne par jour) :**
```
Mar ~XXXX kcal · XXXg P · XXXg G · XXg L ✅/⚠️
Mer ...
```

---

## ATTENTE DE VALIDATION

Terminer par :

---
✅ **Planning prêt.** Modifications ? Réponds **VALIDE** pour générer le HTML et pusher.

---

## PHASE 2 — Déclenchée uniquement sur "VALIDE"

> **NE PAS DEMANDER DE CONFIRMATION.** Enchaîner immédiatement.

1. Lire `.claude/design-system.md` pour les specs HTML.
2. Générer `index.html` complet avec tous les détails (ingrédients précis, macros, chef tips, liste de courses interactive).
3. Sauvegarder `history/YYYY-WXX.json` :
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
4. Committer et pusher sur `main` : `meal plan semaine XX — [liste recettes]`

---

## Stock fourni par Hicham

$ARGUMENTS
