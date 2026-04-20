# 🌿 NutritIA — Diététicienne Intelligente

> Application web de nutrition personnalisée propulsée par l'IA Claude d'Anthropic.  
> Calculs scientifiques, menus sur mesure, recettes complètes et liste de courses générés en temps réel.

---

## 📋 Table des matières

- [Aperçu](#-aperçu)
- [Fonctionnalités](#-fonctionnalités)
- [Accès & Sécurité](#-accès--sécurité)
- [Installation](#-installation)
- [Utilisation](#-utilisation)
- [Architecture technique](#-architecture-technique)
- [Calculs nutritionnels](#-calculs-nutritionnels)
- [Technologies](#-technologies)
- [Confidentialité](#-confidentialité)

---

## 🔍 Aperçu

NutritIA est une application web **single-file** (HTML + CSS + JavaScript, aucune dépendance externe hormis les polices Google Fonts) qui agit comme une diététicienne experte. Elle analyse le profil physique et les habitudes alimentaires de l'utilisateur pour générer des plans nutritionnels personnalisés, des menus variés avec recettes détaillées et une liste de courses automatique.

L'intelligence est fournie par le modèle **Claude Sonnet** (Anthropic) via appel API direct depuis le navigateur.

---

## ✨ Fonctionnalités

### 👤 Profil utilisateur
- Saisie des données physiques (sexe, âge, taille, poids)
- Choix du niveau d'activité et de l'objectif (perte, maintien, prise de masse)
- Préférences alimentaires : régime, allergies, aliments non aimés, préférences de goût
- Personnalisation du petit-déjeuner et du nombre de repas journaliers

### 📊 Analyse nutritionnelle
- **IMC** avec indicateur visuel gradué et statut coloré
- **BMR** (Métabolisme de base) via la formule **Mifflin-St Jeor**
- **TDEE** (Dépense Énergétique Totale) ajustée selon l'activité physique
- **Macronutriments** optimisés (Protéines / Lipides / Glucides) selon OMS & EFSA
- Conseils personnalisés générés par l'IA

### 🥗 Génération de menus
- Plans de **2 jours à 2 semaines**
- Structure configurable : entrée, plat, dessert
- Génération par **lots séquentiels** (2 jours/appel) pour garantir des JSON complets
- Variété assurée entre les lots grâce à la liste des plats déjà utilisés
- Fruits & légumes de **saison** intégrés automatiquement
- **Mode 😋 Plaisir** : version gourmande dans les mêmes macros (sauces, alternatives savoureuses)

### 🍽️ Recettes complètes
Chaque repas inclut :
- Nom du plat
- Liste des ingrédients avec quantités précises
- Étapes de préparation numérotées
- Valeurs nutritionnelles détaillées (kcal, P / L / G)
- Conseil pratique du chef

### 🛒 Liste de courses
- Générée automatiquement à partir des menus
- Consolidation des quantités identiques
- Classée en 6 catégories : Fruits & Légumes · Protéines · Féculents & Céréales · Produits Laitiers · Matières Grasses · Épicerie & Condiments
- Cases à cocher interactives avec compteur de progression
- Impression directe

### 🧊 Mode Frigo
- Saisie libre des ingrédients disponibles
- Génération de 3 recettes adaptées aux stocks
- Indication des ingrédients optionnels manquants

### 💾 Persistance & UX
- Sauvegarde automatique dans le `localStorage` du navigateur
- Mode sombre / clair avec persistance
- Impression CSS optimisée
- Interface responsive (mobile & desktop)
- Notifications toast non-intrusives

---

## 🔐 Accès & Sécurité

L'application est protégée par un **code d'accès professionnel**.

### Connexion
Au premier lancement (ou après expiration de session), une fenêtre de connexion s'affiche. Entrez le code d'accès fourni par votre administrateur.

> ⚠️ Le code d'accès **n'est pas communiqué dans cette documentation** pour des raisons de sécurité.  
> Contactez l'administrateur de l'application pour l'obtenir.

### Session
- La session est **conservée localement pendant 8 heures** après une connexion réussie.
- Aucune reconnexion n'est nécessaire durant cette fenêtre, même en cas de fermeture et réouverture de l'onglet.
- Au-delà de 8 heures, la fenêtre de connexion se réaffiche automatiquement.

### Sécurité du code
- Le mot de passe n'est **jamais stocké en clair** dans le code source ni dans le `localStorage`.
- Il est vérifié via un **double hachage SHA-256** (Web Crypto API native du navigateur) avec sel fixe.
- Seul l'horodatage d'expiration de session est conservé localement.
- Après 3 tentatives incorrectes, un message d'alerte invite à contacter l'administrateur.

---

## 🚀 Installation

Aucune installation, aucun serveur, aucune dépendance à installer.

### Prérequis
- Un navigateur moderne : Chrome 90+, Firefox 88+, Safari 15+, Edge 90+
- Une connexion internet (pour l'API Claude et les polices Google Fonts)

### Lancement

**Option 1 — Ouverture directe**
```
Double-cliquer sur nutritia-ai.html
```

**Option 2 — Serveur local (recommandé)**
```bash
# Python 3
python3 -m http.server 8080
# puis ouvrir http://localhost:8080/nutritia-ai.html
```

```bash
# Node.js / npx
npx serve .
```

```bash
# PHP
php -S localhost:8080
```

**Option 3 — Hébergement statique**

Le fichier peut être déployé sur n'importe quel hébergeur statique :
- GitHub Pages
- Netlify (glisser-déposer le fichier)
- Vercel
- Tout serveur web classique (Apache, Nginx)

---

## 📖 Utilisation

### 1️⃣ Connexion
Entrez le code d'accès fourni par l'administrateur. La session restera ouverte 8 heures.

### 2️⃣ Profil (onglet 👤 Profil)
Remplissez vos informations physiques, votre niveau d'activité, votre objectif et vos préférences alimentaires.  
Cliquez sur **"Calculer mon profil nutritionnel"**.

> 💡 Un bouton **"Essayer avec un profil démo"** est disponible pour tester rapidement l'application.

### 3️⃣ Nutrition (onglet 📊 Nutrition)
Consultez votre IMC, votre BMR, votre TDEE et la répartition optimale de vos macronutriments.  
Des conseils personnalisés sont générés par l'IA en quelques secondes.

### 4️⃣ Menus (onglet 🥗 Menus)
- Sélectionnez la durée (2 jours → 2 semaines)
- Choisissez la structure des repas
- Cliquez sur **"Générer mes menus"**

> La génération se fait par lots successifs — une barre de progression indique l'avancement.  
> Chaque fiche repas est cliquable pour afficher la recette complète.

### 5️⃣ Courses (onglet 🛒 Courses)
La liste est générée automatiquement après la création des menus. Cochez les articles au fur et à mesure de vos achats.

### 6️⃣ Frigo (onglet 🧊 Frigo)
Ajoutez vos ingrédients disponibles et générez des recettes sur mesure en 1 clic.

---

## 🏗️ Architecture technique

```
nutritia-ai.html
│
├── <style>          CSS complet (variables, thème, composants)
│
├── HTML             Structure de l'application (5 sections)
│   ├── #pwGate          Portail de connexion
│   ├── #section-profile Formulaire profil
│   ├── #section-nutrition Analyse & statistiques
│   ├── #section-menus   Générateur de menus
│   ├── #section-courses Liste de courses
│   └── #section-frigo   Mode frigo
│
└── <script>         Logique applicative
    ├── State management (appState)
    ├── Calculs nutritionnels (BMR / TDEE / Macros)
    ├── Générateur de menus par lots (batchs de 2j)
    ├── Réparateur de JSON tronqué (repairTruncatedJSON)
    ├── Gestion courses & mode frigo
    ├── Persistance localStorage
    └── Portail de sécurité (double SHA-256, session 8h)
```

### Flux de génération des menus

```
Utilisateur clique "Générer"
        │
        ▼
Découpage en lots de 2 jours
        │
        ▼ (pour chaque lot)
Appel API Claude Sonnet ──► Prompt allégé (≤4 ingrédients, ≤3 étapes)
        │
        ├─► JSON valide ──► Ajout au tableau allDays
        │
        └─► JSON tronqué ──► repairTruncatedJSON() ──► Fallback simplifié
                │
                ▼
        Fusion allDays → renderMenus()
                │
                ▼
        generateShoppingList() en arrière-plan
```

---

## 🔬 Calculs nutritionnels

### Formule BMR — Mifflin-St Jeor
```
Homme : BMR = (10 × poids_kg) + (6.25 × taille_cm) − (5 × âge) + 5
Femme : BMR = (10 × poids_kg) + (6.25 × taille_cm) − (5 × âge) − 161
```

### Coefficients d'activité (TDEE)
| Niveau | Coefficient |
|--------|-------------|
| Sédentaire | × 1.20 |
| Léger (1-3j/sem) | × 1.375 |
| Modéré (3-5j/sem) | × 1.55 |
| Intense (6-7j/sem) | × 1.725 |

### Ajustement calorique selon objectif
| Objectif | Ajustement |
|----------|-----------|
| Perte de poids | − 500 kcal/j → ~0.5 kg/sem |
| Maintien | ± 0 kcal |
| Prise de masse | + 300 kcal/j |

### Répartition des macronutriments
| Macro | Calcul | Base scientifique |
|-------|--------|-------------------|
| **Protéines** | 1.6–2.0 g/kg (selon objectif) | EFSA, nutrition sportive |
| **Lipides** | ~27% des calories totales | OMS (min. physiologique) |
| **Glucides** | Calories restantes ÷ 4 | Recommandations EFSA |

---

## 🛠️ Technologies

| Technologie | Usage |
|-------------|-------|
| **HTML5** | Structure, sémantique |
| **CSS3** | Variables custom, Grid, Flexbox, animations |
| **JavaScript ES2022** | Logique applicative, async/await |
| **Web Crypto API** | Hachage SHA-256 natif (sécurité portail) |
| **Claude Sonnet API** | Génération IA des conseils, menus, recettes |
| **localStorage** | Persistance profil, menus, session |
| **Google Fonts** | Cormorant Garamond + Outfit |

---

## 🔒 Confidentialité

- **Aucune donnée n'est envoyée à un tiers** autre que l'API Anthropic pour la génération de contenu.
- Les données du profil utilisateur, les menus générés et les préférences sont stockés **uniquement dans le navigateur local** (`localStorage`).
- L'API Anthropic reçoit les données nécessaires à la génération (profil anonymisé + macros cibles) mais ne les conserve pas selon la politique de confidentialité d'Anthropic.
- Le code d'accès n'est jamais transmis sur le réseau — la vérification s'effectue entièrement **côté client** par comparaison de hachages.

---

## 📄 Licence

Application développée pour usage professionnel interne.  
Toute redistribution ou modification nécessite l'accord de l'administrateur.

---

*NutritIA — Powered by Claude (Anthropic) · Interface by EPS Nutrition*
