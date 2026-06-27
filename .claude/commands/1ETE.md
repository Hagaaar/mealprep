# /1ETE — Planning 1 semaine (mode canicule)

Lire `directives.md` + tous `history/*.json` + `liked-recipes.json` en silence avant de commencer.
Appliquer TOUTES les règles de la section **MODE ÉTÉ / CANICULE** de `directives.md` en plus des règles globales.

**Règle likes :** les recettes présentes dans `liked-recipes.json` ont une priorité de sélection proportionnelle à leur `count`. Une recette likée reste soumise à la règle des 8 semaines.

**Au lancement :** demander immédiatement "Quel est ton stock cette semaine ? (Mode canicule activé 🌡️)" et attendre la réponse avant de générer quoi que ce soit.

---

## RAPPEL RÈGLES MODE ETE (non exhaustif — lire directives.md pour le détail complet)

- Tout se mange **froid ou à température ambiante** — réchauffer interdit
- ✅ Air Fryer + Cuiseur à riz + marinade acide uniquement — 🚫 Cocotte et Tajine interdits
- Cuisson uniquement après 21h (ou lundi soir pour le mardi)
- Protéines froides prioritaires : conserves poisson, oeufs durs, poulet poché froid
- Glucides en salade froide uniquement (riz froid, lentilles, pois chiches conserve)
- PRE-training = smoothie froid (banane + skyr + fruits + glaçons)
- Format repas = grande salade repas + sauce froide travaillée
- Légumes ≥ 50% du poids de l'assiette (règle globale)
- Fruits de saison largement autorisés (comptent dans glucides)

---

## PHASE 1 — dans le chat uniquement, ne rien écrire sur disque

Afficher un bloc :
```
── SEMAINE XX — lun D au dim D mois YYYY 🌡️ MODE CANICULE ──
Collations fixes : PRE ~10h : Smoothie [fruits] + skyr + glaçons 🛒 | POST ~16h : Skyr 125g 🛒
1. **[Titre salade froide]** (Mar 💪) — [protéine froide, crudités, sauce froide ✅]
2. **[Titre salade froide]** (Mer 🏃) — ...
3. **[Titre salade froide]** (Jeu 💪) — ...
4. **[Titre salade froide]** (Ven 💪) — ...
5. **[Titre salade froide]** (Sam 🏃) — ...
6. **[Titre salade froide]** (Dim 🏃) — ...
Budget : XX,XX€ / 50€ | ~2017kcal · ~170gP · ~132gG · ~90gL
```

Vérifications silencieuses : aucune répétition sur 8 semaines · fraîcheur · budget ≤ 50€ · pas porc · glucides ≥ 100g · légumes ≥ 50% · tout se mange froid · pas de Cocotte/Tajine.

Terminer par :
> ✅ Planning 1 semaine (mode canicule) prêt. Réponds **VALIDE** pour générer.

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
  <div class="rc-title">[Smoothie froid description]</div>
  <div class="rc-macros">[XXXkcal · XXgP · XXgG · XXgL]</div>
</div>
<!-- Repas midi + soir -->
<div class="recipe-card" style="border-left-color:[couleur-jour]">
  <div class="rc-label">Repas midi + soir · Froid 🌡️</div>
  <div class="rc-title">[Nom salade repas]</div>
  <ul class="rc-ingredients">[liste ingrédients avec grammage]</ul>
  <div class="rc-macros">[XXXkcal · XXgP · XXgG · XXgL]</div>
  <div class="rc-tip"><em>[Chef tip sauce froide]</em></div>
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

### Étape 2 — Sauvegarder l'historique

Créer `history/YYYY-WXX.json` :
```json
{"week":"YYYY-WXX","dates":"D-D mois YYYY","recipes":[
  {"day":"Mardi","name":"...","protein":"..."},
  ...
]}
```

### Étape 3 — Commit + push sur `main`

Message : `meal plan semaine XX ETE — R1, R2, R3, R4, R5, R6`
