# /mealprep

Lire `directives.md` + tous `history/*.json` + `liked-recipes.json` avant de commencer.

**Règle likes :** les recettes présentes dans `liked-recipes.json` ont une priorité de sélection proportionnelle à leur `count`. Une recette likée reste soumise à la règle des 8 semaines — si elle a été faite récemment elle attend, mais elle revient en priorité dès qu'elle est éligible.

**Format d'appel :** première ligne de $ARGUMENTS = nombre de semaines (`1` ou `2`), reste = stock.

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

**Si 2 semaines**, afficher deux blocs consécutifs (semaine N puis N+1). Les 12 recettes doivent toutes être différentes entre elles et absentes des 8 dernières semaines. Budget séparé pour chaque semaine (50€ max chacune). Courses S1 = samedi prochain, courses S2 = samedi suivant — mais **achats groupés pour les produits secs/conserves/épicerie** : si acheter un plus gros conditionnement en S1 revient moins cher à l'unité et couvre le besoin des 2 semaines, l'acheter dès S1 (imputé au budget S1) et le signaler comme déjà en stock pour S2 plutôt que de le racheter. Les produits frais (viande, légumes) restent achetés séparément à chaque session.
```
── SEMAINE XX — lun D au dim D mois ──
[6 recettes + budget S1]

── SEMAINE XX+1 — lun D au dim D mois ──
[6 recettes + budget S2]

Collations fixes (identiques les 2 semaines) : PRE ... | POST Skyr 125g 🛒
Achats groupés S1 → S2 : [liste des produits secs/conserves achetés en gros dès S1 pour couvrir les 2 semaines, s'il y en a]
```

Vérifications silencieuses : aucune répétition sur 8 semaines + N nouvelles · fraîcheur (fraîche Mar-Jeu, conserves Ven-Dim) · budget ≤ 50€/semaine · pas porc · glucides ≥ 100g.

Terminer par :
> ✅ Planning [1 ou 2 semaines] prêt. Réponds **VALIDE** pour générer.

---

## PHASE 2 — uniquement sur "VALIDE", enchaîner sans confirmation

### Étape 1 — Modifier `index.html`

Lire le fichier actuel. C'est le template : **ne pas toucher au CSS ni au JS** sauf les zones ci-dessous.

| Zone | Ce qu'il faut remplacer |
|------|------------------------|
| `<title>` | `Semaine XX` (1 semaine) ou `Semaines XX-YY` (2 semaines) |
| `.hero-sub` (les 3 onglets : Recettes/Courses/Conservation) | phrase courte, légère, humour (voire humour noir) — voir règle sous-titres de `CLAUDE.md`. Jamais de pavé, jamais de date/chiffre. |
| `.hero-date` (onglet Recettes) | plage complète affichée — 1 semaine : `D Mois – D Mois` · 2 semaines : `D Mois – D Mois` (du lundi S1 au dimanche S2), même logique que les onglets Courses/Stockage |
| `.week-name-txt` (Courses/Stockage) | `Semaine XX` + `— Jour DD Mois` (dernier jour de la semaine) |
| `.week-budget-txt` | `XX,XX €` |
| IDs des blocs jours (Recettes) | `day-lunD`, `day-marD`, … `day-dimD` (D = numéro du jour du mois) |
| Contenu de chaque jour | PRE-card · Repas-card (recette, ingrédients, macros, chef-tip) · POST-card |
| Section Courses `.sci` | Articles à acheter (nom, usage, prix). Pour 2 semaines : les produits secs/conserves achetés en gros dès S1 pour couvrir S1+S2 apparaissent dans le rayon "En stock — pas besoin d'acheter" de la semaine S2 (comme dans l'exemple S27 déjà présent dans le template), au lieu d'être rachetés |
| `.courses-total-amt` | total `XX,XX €` |
| `TODAY_MAP` | 7 entrées (1 semaine) ou 14 entrées (2 semaines) `'YYYY-MM-DD': 'day-xxxD'` |
| `STORE_KEY` | `'mp-sXX-YYYY'` |

**Si 2 semaines : l'onglet Recettes affiche les DEUX semaines à la fois, toujours, intégralement.** Jamais une seule semaine avec la seconde différée à plus tard — c'est la règle "affichage 2 semaines" de `CLAUDE.md`. Concrètement dans `#view-recettes` :
1. Les 7 `day-block` de la semaine N (comme d'habitude).
2. Un repère de semaine entre les deux semaines, réutilisant le style déjà défini dans le CSS du template :
   ```html
   <div class="week-marker" style="background:#BF3100">
     <div class="week-marker-txt">Semaine YY</div>
     <div class="week-marker-sub">D Mois – D Mois</div>
   </div>
   ```
   (`YY` = numéro semaine N+1, couleur = même couleur que le Lundi de cette semaine)
3. Les 7 `day-block` de la semaine N+1, avec des IDs `day-xxxD` distincts (D = jour du mois, déjà unique entre les deux semaines).

Le `.macro-ref` (cibles journalières) reste unique en bas de page, partagé entre les deux semaines.

Structure d'un jour ouvert (`day-block` avec `day-head` + `accordion-body` contenant 3 `.meal`, à répliquer exactement sur le template actuel) :
```html
<div class="day-block" style="--day:[couleur-jour];--deep:[couleur-deep]">
  <div class="day-head collapsed" id="head-day-xxxD" onclick="toggleDay('day-xxxD', this)">
    <span class="day-info"><span class="day-label">[Jour] [DD Mois]</span><span class="day-train t-force|t-cardio">[Force|Cardio]</span></span>
    <span class="chevron">▾</span>
  </div>
  <div class="accordion-body collapsed" id="day-xxxD">
    <!-- PRE ~10h -->
    <div class="meal snack">
      <div class="meal-time">PRE ~10h · [détail]</div>
      <div class="meal-body"><strong class="dish-name">[Titre collation]</strong>[description]</div>
    </div>
    <!-- Repas midi + soir -->
    <div class="meal main">
      <div class="meal-time">Midi &amp; soir · [Froid|Chaud] — préparé [jour] soir · [Ustensile si cuisson]</div>
      <div class="meal-body">
        <strong class="dish-name">[Nom recette]</strong>
        <ul>[étapes avec quantités en <strong></li>...]</ul>
        <span class="chef-tip">[Astuce chef]</span>
      </div>
    </div>
    <!-- POST ~16h -->
    <div class="meal snack">
      <div class="meal-time">POST ~16h</div>
      <div class="meal-body"><strong>Skyr nature</strong> — 125g + zestes de citron vert + pincée de sel fin</div>
    </div>
  </div>
</div>
```
Pas de macros affichées par recette dans le template actuel — seul le `.macro-ref` en bas de page (unique, partagé) donne les cibles journalières.

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

> Pour 2 semaines, `index.html` affiche **les deux semaines intégralement et simultanément** dans l'onglet Recettes (voir Étape 1). Rien n'est différé à la semaine prochaine.

### Étape 3 — Commit + push sur `main`

1 semaine : `meal plan semaine XX — R1, R2, R3, R4, R5, R6`
2 semaines : `meal plan semaines XX-YY — R1, R2, R3, R4, R5, R6 | R7, R8, R9, R10, R11, R12`

---

## Stock

$ARGUMENTS
