# Commande /mealprep

Tu es en train de générer le planning repas hebdomadaire de Hicham.

## Ce que tu reçois via $ARGUMENTS
Le stock actuel saisi par Hicham (ingrédients disponibles).

## Fichiers à lire avant de commencer
1. `directives.md` — règles nutritionnelles, ustensiles, contraintes
2. `history/` — tous les fichiers JSON pour éviter les répétitions sur 8 semaines

---

## PHASE 1 — PROPOSITION (répondre dans le chat, NE RIEN PUSHER)

Affiche dans le chat un bloc **compact** (pas de grammage, pas de macros détaillées, pas de tableau de courses) :

```
Semaine XX — [lundi D au dimanche D mois YYYY]
Lundi : 🚫 JEÛNE

Collations fixes (Mar→Dim) :
• PRE ~10h : [ex: 80g flocons d'avoine + 1 banane + 15g beurre cacahuète] ✅/🛒
• POST ~16h : Skyr 125g nature 🛒

6 recettes proposées :
1. **[Titre recette]** (Mardi 💪) — [ingrédient principal, légumes, épices ✅]
2. **[Titre recette]** (Mercredi 🏃) — ...
3. **[Titre recette]** (Jeudi 💪) — ...
4. **[Titre recette]** (Vendredi 💪) — ...
5. **[Titre recette]** (Samedi 🏃) — ...
6. **[Titre recette]** (Dimanche 🏃) — ...

Budget estimé : XX.XX€ / 50€ ✅
Macros journée : ~2 017 kcal · ~170g P · ~132g G · ~90g L ✅
```

Règles de vérification silencieuses (ne pas afficher dans le chat) :
- Aucune recette des 8 dernières semaines (history/)
- Protéines fraîches Mar/Mer/Jeu, conserves/sec Ven/Sam/Dim
- Budget ≤ 50€ (si dépassement → substituer viande fraîche par légumineuses)
- Pas de porc, pas de low-carb < 100g glucides

Termine par :

---
✅ **Planning prêt pour validation.**
Tu peux demander des modifications. Quand tout est bon, réponds **VALIDE**.

---

## PHASE 2 — Déclenchée uniquement quand Hicham répond "VALIDE"

> **INSTRUCTION INTERNE — NE PAS DEMANDER DE CONFIRMATION.**
> Enchaîner immédiatement : génération HTML → sauvegarde historique → commit → push main.

### 1. Générer `index.html`

Fichier HTML autonome (CSS et JS inline, Google Fonts autorisées).

**PALETTE & TYPOGRAPHIE**
```css
--paper: #FAF2DF;        /* fond global */
--card: #FFF9EC;         /* fond cartes */
--card-border: #E8D9B5;  /* bordures */
--ink: #2C1810;          /* texte principal */
--ink-muted: #7A6652;    /* texte secondaire */
--brown-deep: #BF3100;   /* accent fort, Lundi */
--forest: #8EA604;       /* vert */
--blue-deep: #6893AB;    /* bleu */
--sun: #E8A000;          /* orange/jaune */
```
Google Fonts : Newsreader (serif, titres), Hanken Grotesk (sans, corps), Space Mono (mono, macros/chiffres).

**Couleurs des jours (gradient Lundi → Dimanche)**
Lundi #BF3100 → Mardi #D44C00 → Mercredi #E06420 → Jeudi #E87830 → Vendredi #F08C38 → Samedi #F8A040 → Dimanche #FF9241

**STRUCTURE**
- `<html>` avec classe `tab-recettes` / `tab-courses` / `tab-stockage` selon l'onglet actif (chaque onglet a son fond de page).
- Header fixe : badge "Semaine XX" à gauche, badge "date range" à droite. Fond `--card`, bordure bas `--card-border`.
- Barre d'onglets en bas fixe (3 onglets : Recettes | Courses | Stockage), indicateur pill animé qui glisse.
- Padding body : 16px latéral, 80px en haut (header), 72px en bas (tab bar).

**ONGLET RECETTES**
Hero :
```html
<p class="hero-label">Salut chef !</p>
<p class="hero-sub">Alors qu'est-ce qu'on mange aujourd'hui ?</p>
```
7 blocs journaliers en accordéon (Lundi → Dimanche), chaque jour a sa couleur (cf. gradient ci-dessus).
- En-tête : nom du jour + emoji entraînement à gauche, chevron › à droite (tourne à l'ouverture).
- Badge "Aujourd'hui" : pill orange, injecté dynamiquement sur le jour courant (scrollIntoView + ouverture auto).
- Lundi jeûne : accordéon normal, une seule fast-card "Jeûne 24h 🚫" (label rouge).
- Jours normaux : 3 cards — PRE-training (bordure gauche couleur du jour), Repas midi+soir (même bordure, chef-tip en italique), POST-training (Skyr, même bordure).

**ONGLET COURSES**
Hero :
```html
<p class="hero-label">C'est l'heure des courses !</p>
<p class="hero-sub">On reste fort devant le rayon gâteaux et friandises.</p>
```
- Banner budget : montant total (vert gras) / 50€ + reste.
- Barre progression : articles cochés X/Y, fill animé.
- Articles : small square `.check-box` (→ vert + ✓ au clic), nom + tags, prix à droite.
- Articles en stock : opacité 40%, non cliquables.
- Coches persistées en localStorage, clé `mp-sXX-YYYY` (semaine + année).
- Bouton reset en bas.

**ONGLET STOCKAGE**
Hero :
```html
<p class="hero-label">Chaque chose à sa place.</p>
<p class="hero-sub">Allez ! C'est parti pour une bonne partie de Tetris.</p>
```
3 sections : Frigo / Placard / Plats cuisinés (tons bleus, list-box arrondie).

**JS**
```js
// DOMContentLoaded :
// 1. Restaurer coches localStorage
// 2. TODAY_MAP = { 'YYYY-MM-DD': 'day-id', ... } pour les 7 jours de la semaine
// 3. Détecter date du jour → injecter badge + ouvrir accordéon + scrollIntoView (setTimeout 120ms)
// 4. showTab(name), toggleDay(id, header)
```

**MOBILE-FIRST** : conçu pour iPhone 375px. `user-select:none`, `-webkit-tap-highlight-color:transparent`, transitions accordéon 0.35s ease, chevron 0.25s.

**IMPORTANT** : aucune balise de citation, aucun commentaire superflu. Code 100% pur navigateur.

---

### 2. Sauvegarder l'historique `history/YYYY-WXX.json`
```json
{
  "week": "YYYY-WXX",
  "dates": "D-D mois YYYY",
  "recipes": [
    { "day": "Mardi", "name": "Nom recette", "protein": "poulet" },
    ...
  ]
}
```

### 3. Commit et push sur `main`
Message : `meal plan semaine XX — [liste des recettes]`

---

## Stock fourni par Hicham

$ARGUMENTS
