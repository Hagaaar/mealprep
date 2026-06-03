# Commande /mealprep

Tu es en train de générer le planning repas hebdomadaire de Hicham.

## Ce que tu reçois via $ARGUMENTS
Le stock actuel saisi par Hicham (ingrédients disponibles avec quantités).

## Fichiers à lire impérativement avant de commencer
1. `directives.md` — toutes les règles nutritionnelles, ustensiles, contraintes
2. `history/` — tous les fichiers JSON présents pour identifier les recettes utilisées récemment (éviter toute répétition sur 8 semaines)

---

## PHASE 1 — PROPOSITION (répondre dans le chat, ne rien pusher)

Génère et affiche dans le chat :

### 1. Récapitulatif semaine
- Numéro de semaine ISO (ex: Semaine 24 — 9 au 15 juin 2026)
- Lundi = JEÛNE (rappel)

### 2. Les 6 recettes (Mardi → Dimanche)
Pour chaque jour, afficher :
```
MARDI — 💪 Force
Recette : [Nom de la recette]
Ustensile : [Air Fryer / Cocotte / Tajine / Cuiseur à riz]

Ingrédients (2 portions) :
- [ingrédient] : [grammage]g  [EN STOCK ✅ / À ACHETER 🛒]
- ...

Macros plat principal : ~XXX kcal · XXg P · XXg G · XXg L
Chef tip : [astuce marinade ou cuisson]
```

### 3. Vérification variété
Liste les recettes proposées et confirme qu'aucune n'a été utilisée dans les 8 dernières semaines. Si l'historique est vide, l'indiquer.

### 4. Liste de courses consolidée
Uniquement les articles À ACHETER (pas ceux en stock).
Format :
```
RAYON BOUCHERIE / POISSONNERIE
- [article] [quantité] ~X.XX€

RAYON ÉPICERIE
- ...

TOTAL ESTIMÉ : XX.XX€ / 50.00€ budget
```
Si le total dépasse 50€ → proposer automatiquement une substitution (viande fraîche → légumineuses) et recalculer.

### 5. Macros journée complète
Tableau récapitulatif confirmant que les totaux respectent les cibles.

---

## ATTENTE DE VALIDATION

Termine ta réponse Phase 1 par ce bloc exact :

---
✅ **Planning prêt pour validation.**
Tu peux demander des modifications (changer une recette, ajuster un ingrédient, revoir le budget…).
Quand tout est bon, réponds **VALIDE** pour générer le fichier HTML et pusher sur main.

---

## PHASE 2 — Déclenchée uniquement quand Hicham répond "VALIDE"

1. **Générer `index.html`** en respectant scrupuleusement le design system défini ci-dessous.
2. **Sauvegarder l'historique** dans `history/YYYY-WXX.json` (semaine ISO courante) avec la structure :
```json
{
  "week": "2026-W24",
  "dates": "9-15 juin 2026",
  "recipes": [
    { "day": "Mardi", "name": "Nom recette", "protein": "poulet" },
    { "day": "Mercredi", "name": "Nom recette", "protein": "thon" },
    ...
  ]
}
```
3. **Committer et pusher sur `main`** avec le message : `meal plan semaine XX — [liste des recettes]`

---

## Design system index.html

Génère un fichier HTML autonome (CSS et JS inclus, aucune dépendance externe).

**DESIGN**
- Thème sombre iOS natif. Fond #000, cartes #1c1c1e, bordures #38383a, actif #3a3a3c.
- Couleurs : vert #34c759, orange #ff9f0a, bleu #0a84ff, rouge #ff3b30, violet #bf5af2, muted #8e8e93.
- Police : -apple-system, BlinkMacSystemFont, "Segoe UI" — pas de Google Fonts.
- Toutes les couleurs en variables CSS :root.

**STRUCTURE**
- Header fixe : titre à gauche, badge date à droite (fond orange translucide, bordure orange).
- Barre d'onglets sticky sous le header (4 onglets) : Recettes | Courses | Stockage | Règles. Style pill iOS, backdrop-filter: blur, onglet actif sur #3a3a3c.
- Padding body : 16px latéral, 72px en bas.

**ONGLET RECETTES**
- Blocs journaliers en accordéon (Lundi → Dimanche).
- En-tête : texte du jour + emoji entraînement à gauche, chevron › à droite (tourne 90° à l'ouverture).
- Badge "Aujourd'hui" : pill orange, texte noir, injecté dynamiquement sur le jour actif.
- Jours de jeûne : label rouge #ff3b30, une seule fast-card.
- Chaque jour ouvert : 3 cards — PRE-training (bordure gauche orange), Repas principal midi+soir (bordure gauche bleue, avec chef-tip et tip italique), POST-training (bordure gauche orange).

**ONGLET COURSES**
- Banner budget : montant dépensé (vert, 26px gras) vs budget max + reste.
- Barre progression : articles cochés X/Y, track 4px, fill vert animé.
- Sections par rayon, list-box arrondie 12px.
- Chaque article : ring de coche 22px (→ vert + ✓ au clic), nom + tags pill 10px par catégorie, prix à droite.
- Coche persistée en localStorage. Articles en stock : opacité 40%, non cliquables.
- Bouton reset en bas.

**ONGLET STOCKAGE**
- Groupes : Frigo / Congélateur / Placard / Durées. List-box lignes simples.

**ONGLET RÈGLES**
- Grille macros 4 colonnes (orange=kcal, bleu=P, vert=G, violet=L). Blocs règles critiques avec fond coloré translucide.

**JS**
- DOMContentLoaded : restaurer coches localStorage, calculer progression, détecter date du jour → injecter badge + ouvrir accordéon + scrollIntoView (setTimeout 120ms).
- showTab(name), toggleDay(id, header).
- Jours jeûne : accordéon normal, fast-card unique.

**MOBILE-FIRST** : conçu pour iPhone (375px). user-select:none, -webkit-tap-highlight-color:transparent, transitions accordéon 0.35s ease, chevron 0.25s.

**IMPORTANT** : aucune balise de citation ou référence dans le code HTML/CSS/JS. Code 100% pur, directement utilisable par le navigateur.

---

## Stock fourni par Hicham

$ARGUMENTS
