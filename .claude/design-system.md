# Design system — index.html

Génère un fichier HTML autonome (CSS et JS inclus, aucune dépendance externe).

## DESIGN
- Thème sombre iOS natif. Fond #000, cartes #1c1c1e, bordures #38383a, actif #3a3a3c.
- Couleurs : vert #34c759, orange #ff9f0a, bleu #0a84ff, rouge #ff3b30, violet #bf5af2, muted #8e8e93.
- Police : -apple-system, BlinkMacSystemFont, "Segoe UI" — pas de Google Fonts.
- Toutes les couleurs en variables CSS :root.

## STRUCTURE
- Header fixe : titre à gauche, badge date à droite (fond orange translucide, bordure orange).
- Barre d'onglets sticky sous le header (4 onglets) : Recettes | Courses | Stockage | Règles. Style pill iOS, backdrop-filter: blur, onglet actif sur #3a3a3c.
- Padding body : 16px latéral, 72px en bas.

## ONGLET RECETTES
- Blocs journaliers en accordéon (Lundi → Dimanche).
- En-tête : texte du jour + emoji entraînement à gauche, chevron › à droite (tourne 90° à l'ouverture).
- Badge "Aujourd'hui" : pill orange, texte noir, injecté dynamiquement sur le jour actif.
- Jours de jeûne : label rouge #ff3b30, une seule fast-card.
- Chaque jour ouvert : 3 cards — PRE-training (bordure gauche orange), Repas principal midi+soir (bordure gauche bleue, avec chef-tip italique), POST-training (bordure gauche orange).

## ONGLET COURSES
- Banner budget : montant dépensé (vert, 26px gras) vs budget max + reste.
- Barre progression : articles cochés X/Y, track 4px, fill vert animé.
- Sections par rayon, list-box arrondie 12px.
- Chaque article : ring de coche 22px (→ vert + ✓ au clic), nom + tags pill 10px par catégorie, prix à droite.
- Coche persistée en localStorage. Articles en stock : opacité 40%, non cliquables.
- Bouton reset en bas.

## ONGLET STOCKAGE
- Groupes : Frigo / Congélateur / Placard / Durées. List-box lignes simples.

## ONGLET RÈGLES
- Grille macros 4 colonnes (orange=kcal, bleu=P, vert=G, violet=L). Blocs règles critiques avec fond coloré translucide.

## JS
- DOMContentLoaded : restaurer coches localStorage, calculer progression, détecter date du jour → injecter badge + ouvrir accordéon + scrollIntoView (setTimeout 120ms).
- showTab(name), toggleDay(id, header).
- Jours jeûne : accordéon normal, fast-card unique.

## MOBILE-FIRST
Conçu pour iPhone (375px). user-select:none, -webkit-tap-highlight-color:transparent, transitions accordéon 0.35s ease, chevron 0.25s.

**IMPORTANT** : aucune balise de citation ou référence dans le code HTML/CSS/JS. Code 100% pur, directement utilisable par le navigateur.
