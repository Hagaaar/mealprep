# Meal Prep — Claude Code Pipeline

## Ce que ce projet fait

Une page HTML unique déployée sur GitHub Pages. Chaque semaine, on génère un nouveau `index.html` à partir du stock disponible et on le pousse sur `main`. L'URL GitHub Pages reste fixe — seul le contenu change.

## Workflow chaque semaine

1. Lire `stock.md` (mis à jour par l'utilisateur)
2. Proposer un planning 6 jours + 1 jeûne (dimanche)
3. Attendre validation de l'utilisateur
4. Générer `index.html` complet
5. `git add index.html && git commit -m "Meal prep S[N] — [dates]"` puis `git push -u origin main`

**Branche de production : `main`** — tout push va sur main pour que GitHub Pages serve le fichier.

---

## Contraintes nutritionnelles fixes

| Macro | Cible/jour |
|-------|-----------|
| kcal  | ~2 017    |
| Protéines | 170g |
| Glucides  | 132g |
| Lipides   | 90g  |

**Règles non négociables :**
- Graines de courge obligatoires tous les jours (15–20g/portion) — seul levier lipides
- Huile d'olive obligatoire les jours sardines (20ml/portion)
- Citron frais obligatoire sur tout plat avec lentilles ou épinards (absorption fer)
- Skyr + banane + flocons d'avoine = collation PRE-training 10h quotidienne
- POST-training 16h : skyr nature ou shaker whey

## Structure de la semaine

- **6 jours actifs** (lundi→samedi) alternant Cardio 🏃 / Force 💪
- **Dimanche = jeûne total** (eau, thé, café noir uniquement)
- **Chaque repas principal = 2 portions** (13h + 19h) cuisinées la veille au soir
- **Cascade de cuisine** : chaque soir, cuisiner le repas du lendemain

---

## Recettes disponibles (base)

### Poulet
- **Tikka Masala aux Épinards** — 350g émincés volaille + tomates pelées + épinards frais + curry/gochujang + riz 160g
- **Yakitori Soja-Miel** — 300g émincés volaille + soja + miel + gochujang + air fryer 200°C 12min + riz 160g
- **Poulet Citron-Herbes** — émincés + citron + herbes de Provence + haricots verts vapeur + riz

### Poisson
- **Salade Niçoise Sardines** — 2 boîtes sardines + œufs vapeur + pommes de terre + légumes 3-en-1 + olives + huile olive OBLIGATOIRE
- **Maquereau Fumé Haricots** — 1 boîte maquereaux + haricots verts + pommes de terre

### Légumineuses + Œufs
- **Dhal Corail Lait de Coco** — 160g lentilles corail + épinards surgelés + lait de coco + 8 œufs pochés
- **Chakchouka Épinards-Maïs** — tomates pelées + épinards surgelés + maïs + 4 œufs + gochujang
- **Shakshuka Corail** — 120g lentilles corail + tomates + 4 œufs pochés + sriracha

### Règles de planification
- Max 2 jours consécutifs même protéine
- Alterner poulet / poisson / légumineuses sur la semaine
- Jours légumineuses : préférer jours repos ou cardio (digestion plus longue)
- Si stock poulet insuffisant (<500g) : remplacer 1 jour poulet par légumineuses

---

## Format HTML à générer

Le fichier doit reproduire exactement la structure de l'`index.html` actuel :
- Design iOS dark mode (fond #000, cards #1c1c1e)
- 3 onglets : **Recettes** / **Courses** / **Stockage**
- Onglet Recettes : accordéon jour par jour avec badge TODAY automatique
- Onglet Courses : budget banner + progress bar + liste checkable par catégorie avec dish-tags colorés
- Onglet Stockage : frigo / congélateur / placard sec / plats cuisinés durées
- Script JS : tabs, accordion, localStorage check, auto-open today

**Variables à mettre à jour dans le HTML :**
```
<title>Meal Prep S[N] — [date_debut]–[date_fin] [Mois] [Année]</title>
<h1>MEAL PREP · S[N]</h1>
<span class="date">[date_debut] – [date_fin] [Mois]</span>
var STORE_KEY = 'mp-s[N]-[année]';
const TODAY_MAP = { ... }  // dates de la semaine
```

**CSS et JS :** copier à l'identique depuis l'`index.html` existant — ne pas modifier le style.

---

## Gestion du stock

Lire `stock.md` avant de proposer le planning.

**Logique de décision :**
1. Ingrédients marqués `✅ en stock` → utilisables directement
2. Ingrédients marqués `⚠️ vérifier` → signaler à l'utilisateur avant de planifier
3. Ingrédients absents → prévoir en courses (avec prix estimé Lidl/Aldi)
4. Après génération : mettre à jour `stock.md` avec les consommations estimées

**Catégories de courses avec prix indicatifs (Lidl/Aldi) :**
- Émincés volaille 750g : ~5,00€
- Skyr 850g : ~3,25€
- Œufs ×12 : ~2,80€  |  ×18 : ~4,20€
- Sardines ×4 boîtes : ~3,20€
- Bananes régime 6 : ~2,95€
- Citrons ×6 : ~1,00€
- Tomates pelées 800g : ~1,20€
- Lentilles corail 500g : ~1,50€
- Flocons avoine 500g : ~0,85€
- Lait de coco 200ml : ~0,95€
- Épinards frais 600g : ~1,35€

**Budget semaine :** 50€ max (courses uniquement, hors stock)

---

## Instructions de déploiement

```bash
git add index.html
git commit -m "Meal prep S[N] — [dates]"
git push -u origin main
```

Si push échoue réseau : retry ×4 avec backoff (2s, 4s, 8s, 16s).

Ne pas pousser `stock.md` sur main (fichier de travail local uniquement).
