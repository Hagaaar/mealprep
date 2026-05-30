# Meal Prep — Directives Planning Repas
**SÈCHE — TEMPLATE GÉNÉRIQUE · Hicham Jabiroune**

---

## Workflow pipeline

1. L'utilisateur donne son stock et précise **1 ou 2 semaines** (il décide sur le coup)
2. Déduire les dates exactes à partir de la date du jour — **demander confirmation si incertain**
3. Proposer le planning avec **les dates exactes de chaque jour** (ex : Lundi 1er Juin, Mardi 2 Juin…)
4. Attendre validation — l'utilisateur modifie ce qu'il veut
5. Générer `index.html` complet (structure §6 ci-dessous)
6. `git add index.html && git commit -m "Meal prep [dates]"` puis `git push -u origin main`

> ⚠️ **DATES OBLIGATOIRES** : chaque jour du planning et chaque en-tête d'accordéon HTML doit afficher la date exacte (jour + numéro + mois). Le `TODAY_MAP` du JS doit couvrir toutes les dates réelles de la période.

**Branche de production : `main`** — GitHub Pages sert `index.html` sur main. L'URL ne change pas, seul le contenu est remplacé.

---

## 1. Profil personnel & objectif

### 1.1 Données biométriques

| Paramètre | Valeur |
|-----------|--------|
| Sexe | Homme |
| Âge | 35 ans |
| Poids | 110 kg |
| Taille | 1m73 |
| Masse maigre estimée | ~80 kg |
| Activité | Modérée — 3 à 5 séances/semaine |

### 1.2 Cibles nutritionnelles journalières

| Nutriment | Cible/jour | Base de calcul |
|-----------|-----------|----------------|
| Calories totales | 2 017 kcal | Déficit −1 100 kcal → ~800g graisse/semaine |
| Protéines | 170 g | 2,2g × 80 kg MASSE MAIGRE |
| Glucides | 132 g | Maintien performances sportives — plancher 100g/j |
| Lipides | 90 g | Production hormonale et équilibre endocrinien |

> ⚠️ **RÈGLE CRITIQUE — PROTÉINES** : calculées sur la MASSE MAIGRE (80 kg), jamais sur le poids total (110 kg).
>
> ⚠️ Pas de low-carb agressif. Plancher absolu glucides : **100g/jour**.
>
> 💡 **CLAUSE D'AJUSTEMENT** : si fatigue marquée ou plateau en semaine 2 → remonter à 2 300 kcal (déficit ~800 kcal).

---

## 2. Planning des entraînements

| Jour | Type | Exercices | Durée |
|------|------|-----------|-------|
| **Lundi** | 🚫 REPOS | **Jeûne total** — aucun repas, aucune collation | — |
| Mardi | 💪 Force | Push-ups · Pull-ups · Bodyweight · sans machine | Libre |
| Mercredi | 🏃 Cardio | Stairmaster · Rowing · Marche inclinée | 30–40 min |
| Jeudi | 💪 Force | Push-ups · Pull-ups · Bodyweight · sans machine | Libre |
| Vendredi | 💪 Force | Push-ups · Pull-ups · Bodyweight · sans machine | Libre |
| Samedi | 🏃 Cardio | Stairmaster · Rowing · Marche inclinée | 30–40 min |
| Dimanche | 🏃 Cardio | Stairmaster · Rowing · Marche inclinée | 30–40 min |

> 🚫 **LUNDI = JEÛNE TOTAL 24h.** Aucun repas, aucune collation, aucune préparation culinaire.
>
> ✅ Boissons autorisées uniquement : eau, eau gazeuse, thé, café noir non sucré.
>
> ✅ Le jeûne du lundi est un levier métabolique intentionnel — **ne pas compenser le mardi**.

---

## 3. Structure des repas

### 3.1 Chronologie journalière

| Horaire | Moment | Contenu & règles |
|---------|--------|-----------------|
| ~10h00 | PRE-TRAINING | 356 kcal · 47g G · 16g P · 10g L — servi au bureau |
| ~12h00 | ENTRAÎNEMENT | Séance du midi (cardio ou force selon le jour) |
| ~13h00 | REPAS MIDI | Plat de récupération — préparé la veille au soir · 773 kcal · 65g P · 41g G · 39g L |
| ~16h00 | POST-TRAINING | 115 kcal · 24g P · 3g G · 2g L |
| ~19–20h | REPAS SOIR | Exactement le même plat que le midi — même portion, même grammage |
| Lundi | 🚫 JEÛNE | Jeûne total 24h — aucun repas, aucune collation, aucune préparation. Hydratation uniquement. |

### 3.2 Cible macros par repas (midi = soir)

| Moment | Kcal | Protéines | Glucides | Lipides | ×/j |
|--------|------|-----------|----------|---------|-----|
| PRE-training | 356 | 16 g | 47 g | 10 g | ×1 |
| POST-training (Skyr) | 115 | 24 g | 3 g | 2 g | ×1 |
| Plat principal (midi = soir) | 773 | 65 g | 41 g | 39 g | ×2 |
| **TOTAL JOURNÉE** | **2 017** | **170 g** | **132 g** | **90 g** | |

> ⚠️ **RÈGLE ABSOLUE** : 1 session de cuisine = 2 portions identiques. Le plat du midi **EST** le plat du soir.
>
> ⚠️ Pas de variante, pas de supplément, pas de cuisson le matin du jour même.

---

## 4. Contraintes cuisine

### 4.1 Ustensiles autorisés (liste exhaustive)

| Ustensile | Usage |
|-----------|-------|
| 🍳 Air Fryer | Cuisson sans huile, réaction de Maillard, croustillant garanti |
| 🍚 Cuiseur à riz | Glucides complexes standardisés (riz, lentilles, quinoa) |
| 🥘 Cocotte | Mijoté / cuisson vapeur / one-pot |
| 🥘 Tajine | Cuisson longue basse température, conservation micronutriments |

> 🚫 **Interdit** : poêle, casserole, four traditionnel.

### 4.2 Organisation de la préparation

- **Timing** : cuisiner la veille au soir pour le lendemain
- **Quantité** : 1 session = 2 portions identiques (midi + soir). Jamais de cuisson le matin.
- **Marinade** : laisser mariner la protéine la veille de préférence.

### 4.3 Sauces & assaisonnements disponibles en permanence

| Produit | Usage type |
|---------|-----------|
| Sauce soja | Marinade · Cuisson |
| Sriracha | Accompagnement · Cuisson |
| Miel | Marinade · Cuisson · Accompagnement |
| Huile d'olive vierge extra | Cuisson · Accompagnement |
| Maïzena | Marinade · Cuisson |
| Rack épices complet | Cumin · Paprika · Gingembre · Piment · Ail en poudre · Herbes · Curry · Garam Masala · Paprika fumé · Curcuma |

> ⚠️ **EXIGENCE SAVEUR** : les recettes doivent être savoureuses, jamais fades.
>
> ⚠️ Sauces travaillées et marinades sont **obligatoires** à chaque plat — c'est un garde-fou anti-abandon.

---

## 5. Organisation des courses

### 5.1 Paramètres fixes

| Paramètre | Règle |
|-----------|-------|
| Jour des courses | **Samedi uniquement** — une fois par semaine chez Leclerc Mulhouse |
| Enseigne | **Leclerc Mulhouse** en priorité absolue |
| Budget hebdomadaire | **50 € MAXIMUM** — absolu et non négociable |

### 5.2 Règle fraîcheur — rotation des protéines

- **Protéines fraîches en début de semaine (Mar/Mer/Jeu)** : cuire dans les 48h après achat.
- **Conserves et sec en milieu/fin de semaine (Ven/Sam/Dim)** : pas de contrainte.
- **Congélateur en dépannage** — ne pas planifier dessus systématiquement.

### 5.3 Construire la liste de courses — méthode

| N° | Action | Contrôle |
|----|--------|----------|
| 1 | Inventaire | Lister tout ce qui est disponible (conserves, congélo, sec, frais). Quantités précises. |
| 2 | Besoin net | Calculer ce dont chaque recette a besoin. Soustraire ce qui est déjà en stock. |
| 3 | Liste Leclerc | Ranger par rayon. |
| 4 | Contrôle total | Vérifier que le total ≤ 50€. Si dépassement → remplacer viande fraîche par légumineuses. |

**Prix indicatifs Leclerc Mulhouse :**

| Article | Prix estimé |
|---------|------------|
| Émincés volaille 750g | ~5,00€ |
| Skyr 850g | ~3,25€ |
| Œufs ×12 | ~2,80€ |
| Œufs ×18 | ~4,20€ |
| Sardines ×4 boîtes | ~3,20€ |
| Bananes régime 6 | ~2,95€ |
| Citrons ×6 | ~1,00€ |
| Tomates pelées 800g | ~1,20€ |
| Lentilles corail 500g | ~1,50€ |
| Flocons avoine 500g | ~0,85€ |
| Lait de coco 200ml | ~0,95€ |
| Épinards frais 600g | ~1,35€ |
| Graines de courge 250g | ~2,50€ |

---

## 6. Méthode — générer le planning de semaine

### 6.1 Ce qu'il faut fournir pour démarrer

- **Stock actuel complet** : conserves (produit + quantité + grammage/boîte) · congélateur · sec/bocaux · frais.
- **Courses déjà effectuées** : si des courses ont été faites avant génération, les lister avec les prix.

### 6.2 Checklist de génération — dans cet ordre

| N° | Action | Contrôle |
|----|--------|----------|
| 1 | Inventorier le stock disponible avant toute planification | Quantités exactes notées |
| 2 | Planifier les protéines selon rotation budget-réaliste | Rotation respectée, fraîches en début de semaine |
| 3 | Construire les recettes (2 portions/plat, sauce obligatoire, ustensiles respectés) | Saveur + macros vérifiés |
| 4 | Calculer les macros par plat — cible ~773 kcal / P65g / G41g / L39g | Ajustement lipides si jours conserves |
| 5 | Construire la liste de courses (besoin − stock) | Total ≤ 50€ — vérification obligatoire avant validation |
| 6 | Générer le fichier html | Nom du fichier : `index.html` |

### 6.3 Structure du fichier HTML attendu

**Variables à mettre à jour à chaque génération :**
```html
<title>Meal Prep — [date_debut]–[date_fin] [Mois] [Année]</title>
<h1>MEAL PREP</h1>
<span class="date">[date_debut] – [date_fin] [Mois]</span>
var STORE_KEY = 'mp-[date_debut]-[année]';
const TODAY_MAP = { 'YYYY-MM-DD': 'day-id', ... }  /* toutes les dates couvertes */
```

Pour 2 semaines : `TODAY_MAP` couvre 14 entrées, les jours s'enchaînent normalement.

**Design system :**
- Thème sombre iOS natif. Fond `#000`, cartes `#1c1c1e`, bordures `#38383a`, état actif `#3a3a3c`.
- Couleurs sémantiques : vert `#34c759`, orange `#ff9f0a`, bleu `#0a84ff`, rouge `#ff3b30`, violet `#bf5af2`, muted `#8e8e93`.
- Police : `-apple-system, BlinkMacSystemFont, "Segoe UI"` — pas de Google Fonts.
- Toutes les couleurs en variables CSS `:root`.

**3 onglets (sticky, style pill iOS, backdrop-filter blur) :**
1. **Recettes** — accordéon jour par jour
2. **Courses** — liste checkable avec budget et progression
3. **Stockage** — zones frigo/congélo/placard/durées

**Onglet Recettes :**
- Accordéon par jour (Lundi→Dimanche), chevron tourne à 90° quand ouvert.
- Badge `Aujourd'hui` : pill fond `#ff9f0a`, texte noir, injecté inline JS.
- Jours de jeûne : label en rouge `#ff3b30`, une seule `fast-card` sans meal cards.
- Cards repas : bordure gauche bleue (repas principal) / orange (collations).
- `chef-tip` : fond `rgba(10,60,120,.25)`, bordure gauche `#1a5fb4`, font-size 13px.
- `tip` : italic, muted, 12px.
- `prep-alert` : fond `rgba(255,59,48,.12)`, bordure rouge, texte rouge gras.
- **Cascade de cuisine** : chaque soir, cuisiner le repas du lendemain → inclure une `prep-alert` dans chaque jour.

**Onglet Courses :**
- Banner budget : montant dépensé (26px gras vert) + budget max + reste.
- Barre de progression animée (fill vert).
- Sections par rayon (Viandes / Poissonnerie-Conserves / Crémerie / Fruits-Légumes / Épicerie / Reports stock).
- Chaque article : ring de coche 22px + nom + `item-dishes` (tags colorés : bleu=volaille, violet=poisson, orange=œufs, vert=quotidien, rouge=warning) + `item-sub` substitutions + prix aligné droite.
- Clic → classe `checked` → ring vert + nom barré + persisté `localStorage`.
- Articles en stock : classe `stock`, opacité 40%, non cliquables.

**Onglet Stockage :**
- Groupes : Frigo / Congélateur / Placard sec / Plats cuisinés durées.

**Comportement JS :**
- `DOMContentLoaded` : charger localStorage + progression + badge Aujourd'hui + scrollIntoView `setTimeout(120ms)`.
- `showTab(name)` · `toggleDay(id, header)` · `check(el)` · `save()` · `load()` · `resetAll()` · `updateProgress()`.

**Mobile-first :**
- Conçu pour iPhone 13 mini (375px). Aucun media query.
- `user-select: none` sur éléments interactifs. Transitions légères partout.

> ⚠️ **IMPORTANT** : le code HTML généré doit être 100% pur et directement utilisable par le navigateur. Aucune balise de citation ou référence IA dans le code.

---

## 7. Exclusions & interdits absolus

| ❌ Interdit | Raison |
|------------|--------|
| **Porc** sous toutes ses formes | Exclusion alimentaire stricte |
| Repas ou collation le **lundi** | Jeûne total 24h — aucune exception |
| Autres ustensiles de cuisson | Air Fryer + Cuiseur à riz + Cocotte + Tajine seulement |
| Courses hors Leclerc Mulhouse | Budget et habitudes à maintenir |
| Dépasser **50€/semaine** | Budget maximum absolu |
| Recettes sans sauce ni épices | Saveur obligatoire — jamais fade |
| Low-carb agressif < 100g G/jour | Contre-productif pour les performances sportives |
| Protéines calculées sur poids total | Toujours sur la masse maigre (80 kg) |
| Cuisson le matin du jour même | Toujours cuisiner la veille au soir |

---

## 8. Répertoire de recettes favorites

> À utiliser comme inspiration créative — pas des menus rigides.

**Maghrébin / Méditerranéen**
- Tajine de poulet aux pommes de terre et aux olives vertes
- Tajine de boulettes de viande aux œufs
- Tajine bœuf ou agneau aux haricots et aux artichauts
- Couscous marocain au poulet et aux 7 légumes
- Zaalouk marocain
- Houmous à la viande hachée
- Taboulé
- Loubia
- Chakchouka
- Brochettes de viande hachée façon köfte

**Asiatique**
- Nouilles sautées aux légumes
- Poulet tikka masala
- Curry de poisson / de chou-fleur et carottes / d'aubergines et pommes de terre
- Dhal de lentilles corail au lait de coco
- Bo bun au bœuf à la citronnelle
- Yakitori de poulet
- Ramen (soupe de nouilles japonaise)
- Poulet teriyaki
- Pho (Phở)
- Nouilles Udon sautées au bœuf et brocolis

**Occidental / Méditerranéen**
- Moussaka
- Chili con carne (sans porc)
- Salade niçoise
- Salade César au poulet
- Fajitas au poulet et aux poivrons croquants
- Poulet basquaise
- Salade grecque à la feta et aux olives Kalamata
- Poulet Korma
