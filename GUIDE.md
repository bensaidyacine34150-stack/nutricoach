# 🚀 GUIDE COMPLET — Publier NutriCoach AI sur l'App Store

## ✅ CE QUE TU AS DANS CE DOSSIER

```
nutricoach-capacitor/
├── www/
│   └── index.html          ← Ton application complète
├── ios-config/
│   └── Info.plist          ← Configuration iOS (permissions, etc.)
├── capacitor.config.json   ← Configuration Capacitor
├── package.json            ← Dépendances npm
└── GUIDE.md                ← Ce fichier
```

---

## 🛠️ ÉTAPE 0 — CE DONT TU AS BESOIN

Avant de commencer, installe ces outils sur ton Mac :

### 1. Xcode (OBLIGATOIRE — Mac uniquement)
- Ouvre l'**App Store** sur ton Mac
- Cherche **Xcode** et installe-le (c'est gratuit, ~12 Go)
- Lance Xcode une fois pour accepter les licences

### 2. Node.js
- Va sur https://nodejs.org
- Télécharge la version **LTS** et installe-la
- Vérifie : ouvre le Terminal et tape `node --version`

### 3. CocoaPods
```bash
sudo gem install cocoapods
```

### 4. Compte Développeur Apple (99$/an)
- Va sur https://developer.apple.com/programs/
- Clique "Enroll" et suis les étapes
- Paye les 99$/an (obligatoire pour publier)

---

## 📦 ÉTAPE 1 — INSTALLER CAPACITOR

Ouvre le **Terminal** sur ton Mac, puis :

```bash
# Va dans le dossier du projet
cd ~/Downloads/nutricoach-capacitor

# Installe les dépendances
npm install

# Vérifie que Capacitor est bien installé
npx cap --version
```

---

## 📱 ÉTAPE 2 — CRÉER LE PROJET IOS

```bash
# Ajouter la plateforme iOS
npx cap add ios

# Synchroniser les fichiers web vers iOS
npx cap sync ios
```

---

## ⚙️ ÉTAPE 3 — CONFIGURER XCODE

```bash
# Ouvre le projet dans Xcode automatiquement
npx cap open ios
```

Xcode s'ouvre. Dans Xcode :

### 3a. Sélectionne ton équipe de développement
- Clique sur **"App"** dans le panneau gauche
- Onglet **"Signing & Capabilities"**
- Dans **"Team"**, sélectionne ton compte Apple
- Xcode va créer automatiquement le profil de signature

### 3b. Remplace le fichier Info.plist
- Dans Xcode, ouvre `App/App/Info.plist`
- Remplace son contenu par celui du fichier `ios-config/Info.plist`
  fourni dans ce dossier

### 3c. Configure l'identifiant de l'app
- Dans **"Signing & Capabilities"**
- **Bundle Identifier** : `com.nutricoach.ai`
  (si ce nom est pris, essaie `com.tonnom.nutricoach`)

### 3d. Configure la version
- **Version** : 1.0.0
- **Build** : 1

---

## 🎨 ÉTAPE 4 — ICÔNES ET SPLASH SCREEN

### Icône de l'app
Tu as besoin d'une icône **1024×1024 pixels** en PNG (sans transparence).

**Créer l'icône gratuitement :**
1. Va sur https://www.canva.com
2. Crée un design 1024×1024px
3. Utilise le fond vert #c8f135 avec l'emoji 🥦 ou un design personnalisé
4. Exporte en PNG

**Intégrer l'icône dans Xcode :**
1. Dans Xcode, ouvre `App/App/Assets.xcassets`
2. Clique sur **"AppIcon"**
3. Glisse-dépose ton image 1024×1024 dans le carré **"App Store"** (1024pt)
4. Pour les autres tailles, utilise **https://appicon.co** — colle ton 1024px
   et télécharge le dossier complet

---

## 🔑 ÉTAPE 5 — CLÉ API ANTHROPIC

**IMPORTANT :** Pour que le Coach IA fonctionne, tu dois sécuriser la clé API.

### Option A — Mode démo (pour tester)
L'app fonctionne sans clé mais le chat IA affichera un message d'erreur.

### Option B — Avec clé API (recommandé pour production)
1. Va sur https://console.anthropic.com
2. Crée un compte et génère une clé API
3. Dans `www/index.html`, cherche la ligne :
   ```javascript
   headers: {'Content-Type': 'application/json'},
   ```
4. Ajoute ta clé :
   ```javascript
   headers: {
     'Content-Type': 'application/json',
     'x-api-key': 'sk-ant-XXXXXXXXXXXXXXXXX',
     'anthropic-version': '2023-06-01'
   },
   ```

### Option C — Backend sécurisé (professionnel)
Crée un petit serveur (Node.js/Express) qui masque la clé et fait proxy vers l'API Anthropic.
Contact un développeur ou utilise des services comme Render.com ou Railway.app (gratuits).

---

## 🧪 ÉTAPE 6 — TESTER SUR TON IPHONE

### Test sur simulateur (sans iPhone physique)
1. Dans Xcode, en haut, sélectionne **"iPhone 15 Pro"** comme device
2. Clique sur le bouton **▶ Run** (ou Cmd+R)
3. L'app se lance dans le simulateur

### Test sur ton iPhone physique
1. Branche ton iPhone en USB
2. Dans Xcode, sélectionne ton iPhone dans la liste des devices
3. Va dans **Settings > General > VPN & Device Management** sur ton iPhone
4. Fait confiance au certificat développeur
5. Clique ▶ Run dans Xcode

---

## 📋 ÉTAPE 7 — PRÉPARER LA SOUMISSION

### 7a. App Store Connect
1. Va sur https://appstoreconnect.apple.com
2. Connecte-toi avec ton compte développeur Apple
3. Clique **"My Apps"** → **"+"** → **"New App"**
4. Remplis :
   - **Platform** : iOS
   - **Name** : NutriCoach AI
   - **Primary Language** : French
   - **Bundle ID** : `com.nutricoach.ai`
   - **SKU** : `nutricoach-ai-001`

### 7b. Captures d'écran (OBLIGATOIRES)
Apple exige des screenshots pour chaque taille d'écran :
- **6.9" (iPhone 16 Pro Max)** : 1320×2868 pixels — 3 à 10 captures
- **6.5" (iPhone 14 Plus)** : 1242×2688 pixels — 3 à 10 captures
- **5.5" (iPhone 8 Plus)** : 1242×2208 pixels — optionnel mais recommandé

**Comment les faire :**
1. Lance l'app dans le simulateur Xcode (iPhone 16 Pro Max)
2. Parcours les écrans principaux (Accueil, Programme, Coach IA, Progrès)
3. Fais des captures (Cmd+S dans le simulateur)
4. Ou utilise https://screenshots.pro pour des mockups professionnels

### 7c. Description de l'app (à copier/adapter)
```
NutriCoach AI — Ton Coach Nutrition Personnel

Atteins tes objectifs de forme avec un programme 100% personnalisé, 
propulsé par l'intelligence artificielle.

🎯 PERSONNALISÉ POUR TOI
• Programme calculé selon ton poids, taille, âge et objectif
• Adapté à ton régime : standard, végétarien, vegan, keto
• Macronutriments optimisés (protéines, glucides, lipides)

🤖 COACH IA 24H/24
• Pose toutes tes questions nutrition à ton assistant IA
• Conseils personnalisés basés sur ton profil
• Recommandations de repas et de recettes

📊 SUIVI COMPLET
• Suivi des calories et macros en temps réel
• Journal alimentaire quotidien
• Courbe de poids et progrès dans le temps
• Tracker d'hydratation
• Calcul d'IMC

🍽️ PLANS REPAS ADAPTÉS
• Plan de repas hebdomadaire personnalisé
• Base d'aliments nutritifs et économiques
• Règles alimentaires de ton programme

💪 OBJECTIFS DISPONIBLES
• Perte de poids (déficit calorique intelligent)
• Prise de masse musculaire (surplus contrôlé)
• Maintien et équilibre alimentaire

Simple, beau et efficace — NutriCoach AI t'accompagne vers tes objectifs.
```

### 7d. Mots-clés (pour être trouvé)
```
nutrition,régime,calories,coach,fitness,minceur,masse,proteines,repas,poids,sante,imc,macro,musculation
```

### 7e. Catégories recommandées
- **Primaire** : Health & Fitness
- **Secondaire** : Food & Drink

---

## ⬆️ ÉTAPE 8 — SOUMETTRE L'APP

### 8a. Archiver l'app dans Xcode
1. Dans Xcode, **Product → Archive**
2. Attends la compilation (2-5 minutes)
3. La fenêtre **Organizer** s'ouvre
4. Clique **"Distribute App"**
5. Choisis **"App Store Connect"**
6. Clique **"Next"** jusqu'à la fin
7. L'archive est uploadée (quelques minutes)

### 8b. Soumettre pour révision
1. Retourne sur https://appstoreconnect.apple.com
2. Ton app apparaît avec le build uploadé
3. Dans **"Pricing and Availability"** : mets l'app en **Free**
4. Dans **"App Review Information"** :
   - Notes de révision : "Application de nutrition avec IA. Le chat requiert une connexion internet pour fonctionner."
5. Clique **"Submit for Review"**

---

## ⏱️ DÉLAIS ET RÉSULTATS

| Étape | Délai |
|-------|-------|
| Révision Apple | 1 à 7 jours |
| Publication après approbation | Immédiat ou date choisie |
| Disponibilité dans les stores | 24-48h après publication |

**Apple refusera si :**
- Pas assez de fonctionnalités (mais notre app en a assez ✅)
- Contenus médicaux non disclaimés → ajoute "Consulte un médecin"
- Bugs crashant l'app → teste bien avant

---

## 💰 COÛTS RÉSUMÉS

| Élément | Coût |
|---------|------|
| Compte développeur Apple | 99 $/an |
| Xcode + outils | Gratuit |
| Capacitor | Gratuit |
| Hébergement (si backend) | 0-10 $/mois |
| Clé API Anthropic | ~5-20 $/mois selon usage |

---

## ❓ PROBLÈMES FRÉQUENTS

**"No signing certificate"**
→ Dans Xcode → Preferences → Accounts → ajoute ton Apple ID

**"Bundle identifier already in use"**
→ Change `com.nutricoach.ai` en `com.TONNOM.nutricoach`

**"Missing compliance"**
→ Dans App Store Connect → ton app → coche "No" pour l'export compliance

**L'app se ferme au démarrage**
→ Vérifie les logs dans Xcode (panneau en bas) et corrige les erreurs

---

## 📞 BESOIN D'AIDE ?

Si tu es bloqué à une étape :
1. Cherche l'erreur exacte sur **stackoverflow.com**
2. Consulte la doc officielle : **capacitorjs.com/docs/ios**
3. Forums Apple Developer : **developer.apple.com/forums**

Bonne chance pour la publication ! 🚀
