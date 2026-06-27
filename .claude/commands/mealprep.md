# /mealprep

Lire `directives.md` + tous `history/*.json` + `liked-recipes.json` avant de commencer.

**Règle likes :** les recettes présentes dans `liked-recipes.json` ont une priorité de sélection proportionnelle à leur `count`. Une recette likée reste soumise à la règle des 8 semaines — si elle a été faite récemment elle attend, mais elle revient en priorité dès qu'elle est éligible.

**Format d'appel :** première ligne de $ARGUMENTS = `1`, `2`, `1 ETE` ou `2 ETE`. Pas de stock dans la commande.

**Comportement au lancement :**
1. Lire les fichiers ci-dessus en silence
2. Détecter le mode : `ETE` présent → mode canicule activé (appliquer la section MODE ÉTÉ de `directives.md`)
3. Détecter le nombre de semaines : `1` ou `2`
4. Demander le stock à Hicham :
   - Mode normal : "Quel est ton stock cette semaine ?"
   - Mode ETE : "Quel est ton stock cette semaine ? (Mode canicule activé 🌡️)"
5. Attendre la réponse avant de générer quoi que ce soit

## PHASE 1 — dans le chat uniquement, ne rien écrire sur disque

**Si 1 semaine**, afficher un bloc :
```
── SEMAINE XX — lun D au dim D mois YYYY ──
Collations fixes : PRE ~10h : [description] ✅/🛒 | POST ~16h : Skyr 125g 🛒
1. **[Titre]** (Mar 💪) — [protéine, légumes, épices ✅]
2. **[Titre]** (Mer 🏃) — ...
3. **[Titre]** (Jeu 💪) — ...
4. **[Titre]** (Ven 💪) — ...
5. **[Titre]** (Sam 🏃) — ...
6. **[Titre]** (Dim 🏃) — ...
Budget : XX,XX€ / 50€ | ~2017kcal · ~170gP · ~132gG · ~90gL
```

**Si 2 semaines**, afficher deux blocs consécutifs (semaine N puis N+1). Les 12 recettes doivent toutes être différentes entre elles et absentes des 8 dernières semaines. Budget séparé pour chaque semaine (50€ max chacune). Courses S1 = samedi prochain, courses S2 = samedi suivant.
```
── SEMAINE XX — lun D au dim D mois ──
[6 recettes + budget S1]

── SEMAINE XX+1 — lun D au dim D mois ──
[6 recettes + budget S2]

Collations fixes (identiques les 2 semaines) : PRE ... | POST Skyr 125g 🛒
```

Vérifications silencieuses : aucune répétition sur 8 semaines + N nouvelles · fraîcheur (fraîche Mar-Jeu, conserves Ven-Dim) · budget ≤ 50€/semaine · pas porc · glucides ≥ 100g.

Terminer par :
> ✅ Planning [1 ou 2 semaines] prêt. Réponds **VALIDE** pour générer.

---

## PHASE 2 — uniquement sur "VALIDE", enchaîner sans confirmation

### Étape 1 — Modifier `index.html`

Lire le fichier actuel. C'est le template : **ne pas toucher au CSS ni au JS** sauf les 9 zones ci-dessous.

| Zone | Ce qu'il faut remplacer |
|------|------------------------|
| `<title>` | `Semaine XX` |
| `.week-name-txt` | `Semaine XX` + `— Jour DD Mois` (dernier jour de la semaine) |
| `.week-budget-txt` | `XX,XX €` |
| IDs des blocs jours | `day-lunD`, `day-marD`, … `day-dimD` (D = numéro du jour du mois) |
| Contenu de chaque jour | PRE-card · Repas-card (recette, ingrédients, macros, chef-tip) · POST-card |
| Section Courses `.sci` | Articles à acheter (nom, usage, prix) |
| `.courses-total-amt` | total `XX,XX €` |
| `TODAY_MAP` | 7 entrées `'YYYY-MM-DD': 'day-xxxD'` |
| `STORE_KEY` | `'mp-sXX-YYYY'` |

Structure d'un jour ouvert (3 cards, à répliquer exactement) :
```html
<!-- PRE ~10h -->
<div class="recipe-card" style="border-left-color:[couleur-jour]">
  <div class="rc-label">PRE ~10h</div>
  <div class="rc-title">[description]</div>
  <div class="rc-macros">[XXXkcal · XXgP · XXgG · XXgL]</div>
</div>
<!-- Repas midi + soir -->
<div class="recipe-card" style="border-left-color:[couleur-jour]">
  <div class="rc-label">Repas midi + soir · [Ustensile]</div>
  <div class="rc-title">[Nom recette]</div>
  <ul class="rc-ingredients">[liste ingrédients avec grammage]</ul>
  <div class="rc-macros">[XXXkcal · XXgP · XXgG · XXgL]</div>
  <div class="rc-tip"><em>[Chef tip]</em></div>
</div>
<!-- POST ~16h -->
<div class="recipe-card" style="border-left-color:[couleur-jour]">
  <div class="rc-label">POST ~16h</div>
  <div class="rc-title">Skyr 125g nature</div>
  <div class="rc-macros">115kcal · 24gP · 3gG · 2gL</div>
</div>
```

Couleurs des jours : Lun `#BF3100` · Mar `#D44C00` · Mer `#E06420` · Jeu `#E87830` · Ven `#F08C38` · Sam `#F8A040` · Dim `#FF9241`

Structure d'un article courses :
```html
<li class="sci" data-id="[id-unique]" onclick="toggle(this)">
  <div class="check-box"></div>
  <div class="sci-content">
    <div class="sci-info">
      <div class="sci-name">[Nom produit]</div>
      <div class="sci-use">[Jours d'utilisation]</div>
    </div>
    <div class="sci-right">
      <div class="sci-price">~X,XX€</div>
      <div class="sci-qty">[quantité]</div>
    </div>
  </div>
</li>
```

### Étape 2 — Sauvegarder les fichiers history

**1 semaine :** un seul fichier `history/YYYY-WXX.json`.
**2 semaines :** deux fichiers `history/YYYY-WXX.json` + `history/YYYY-WYY.json`.

```json
{"week":"YYYY-WXX","dates":"D-D mois YYYY","recipes":[
  {"day":"Mardi","name":"...","protein":"..."},
  ...
]}
```

> Pour 2 semaines, `index.html` représente toujours **la semaine N uniquement** (semaine en cours). La semaine N+1 sera affichée la semaine prochaine : l'historique est déjà sauvegardé, il suffira de re-lancer `/mealprep 1` avec le nouveau stock.

### Étape 3 — Commit + push sur `main`

1 semaine : `meal plan semaine XX — R1, R2, R3, R4, R5, R6`
2 semaines : `meal plan semaines XX-YY — R1, R2, R3, R4, R5, R6 | R7, R8, R9, R10, R11, R12`

---

## Stock

Le stock est fourni par Hicham après la demande — ne pas utiliser $ARGUMENTS comme stock.
