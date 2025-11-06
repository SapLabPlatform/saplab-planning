# 🍁 SapLab - TODO Master (MIS À JOUR 2025-11-06)

**Projet:** Système de monitoring acéricole IoT avec Django/Ionic  
**Status Actuel:** Backend Auth ✅ | Design Sprint ✅ | Frontend Setup → NEXT

---

## ✅ ACCOMPLISSEMENTS 2025-01-13

### Milestone 1a - Backend Auth COMPLÉTÉ
- [x] App `users` authentication complète (11 tests passing)
- [x] JWT tokens (access 15min, refresh 7 jours)
- [x] Endpoints: `/api/auth/login/`, `/api/auth/refresh/`, `/api/users/me/`
- [x] UserManager + password hashing + validations
- [x] Factory pattern pour tests

### Milestone 1b - Design Sprint COMPLÉTÉ  
- [x] Wireframes (Login + Dashboard Mobile)
- [x] Palette couleurs Dark Mode finalisée
- [x] Stack confirmé (Ionic React + Tailwind + Recharts + Zustand + React Query)
- [x] Navigation décidée (Header + Bottom Nav 3 items)
- [x] 6 Widgets MVP identifiés
- [x] Documentation (4 fichiers, 42 KB)

### Hardware Évaporateur PT100 - EN COURS (Nov 2024 démarré)
- [x] Architecture thermowell DIY finalisée (5 Nov 2024)
- [x] PT100 3-wire + lead wire 40" PFA acheté
- [x] Tube inox 316L 3/8" × 6 pieds acheté ($2.70 deal!)
- [x] End caps inox 316 achetés
- [x] Configuration: Over-the-top clamp, 13" longueur, 0-300°F
- [x] 6 recettes pré-définies (sirop, tire, beurre, sucres, bonbons)
- [ ] Pratique TIG + thermowell final (Décembre 2024)
- [ ] Installation + calibration (Janvier 2025)
- [ ] Production saison 2025! (Février-Avril 2025)

---

## 🎯 MILESTONE 1c - Frontend Setup & Login (PROCHAINE ÉTAPE)

**Estimation:** 2-3h | **Objectif:** Login page fonctionnelle connectée au backend

### Setup Projet
- [ ] `ionic start saplab-app blank --type=react`
- [ ] Installer Tailwind + dépendances (recharts, lucide-react, zustand, react-query, axios)
- [ ] Config Tailwind (couleurs maple, dark mode)
- [ ] Config CSS global (Ionic dark theme variables)
- [ ] Structure dossiers (pages/, components/, services/, stores/, hooks/, types/)

### Types & Services
- [ ] Types TypeScript (User, LoginFormData, AuthResponse, AuthStore)
- [ ] API service (axios + interceptors)
- [ ] Auth service (login, logout, refreshToken, getCurrentUser)
- [ ] Auth store Zustand (user, tokens, isAuthenticated, actions)

### Login Page
- [ ] Component Login.tsx (UI dark mode)
- [ ] Form: email + password + "remember me" checkbox
- [ ] Validation (email format, password min 8 chars)
- [ ] Button "Se connecter" (loading state)
- [ ] Error handling & display
- [ ] Link "Mot de passe oublié"

### Routing
- [ ] IonReactRouter config
- [ ] Routes: `/login`, `/dashboard`, `/`
- [ ] Auth guard (redirect si non authentifié)
- [ ] Test redirect dashboard après login

**Critères succès:** Login responsive, connexion backend OK, tokens stockés, redirect fonctionne

---

## 📱 MILESTONE 1d - Dashboard Skeleton

- [ ] Layout: Header (Logo + Menu + Notifs + User) + BottomNav (3 items)
- [ ] Dashboard page avec dummy widgets
- [ ] QuotaWidget, WeatherWidget (données statiques)
- [ ] Responsive (1 col mobile, 2-3 cols desktop)

---

## 📊 MILESTONE 1e - Premier Widget Fonctionnel

- [ ] Backend: Endpoint quota `/api/production/quota/current/`
- [ ] Frontend: React Query hook + vraies données
- [ ] Loading/error states
- [ ] Progress bar dynamique + couleurs selon %

---

## 🔌 MILESTONE 1f - Backend IoT + Hardware

- [ ] Backend: App `iot` (Device, Sensor, SensorReading models)
- [ ] Endpoints: provisioning + ingestion readings
- [ ] ESP32: Code production (WiFi reconnect, deep sleep, batch envoi)
- [ ] Frontend: Widget pression (Recharts 24h)

---

## 🎯 MILESTONE 2 - Production Features

- [ ] Gestion voyages d'eau (CRUD + quota calc)
- [ ] Gestion barils (fermeture + étiquette PDF + QR code)
- [ ] Timeline saison (événements)

---

## 🎯 MILESTONE 3 - Moniteur Brix (Hiver 2026)

- [ ] Hardware: Chambre mesure 120cm + calibration 7 points
- [ ] ESP32: Code Brix (filtrage, correction temp, détection anomalies)
- [ ] Frontend: Gauge + graphique + alarmes

---

## 🎯 MILESTONE 4 - Évaporateur PT100 (EN PARALLÈLE - Saison 2025!)

**Status:** Hardware EN COURS (Novembre 2024 démarré) | Backend/Frontend À FAIRE  
**Timeline:** Nov 2024 - Avril 2025 (utilisation production saison 2025!)

### ✅ Hardware PT100 - ACCOMPLISSEMENTS (Nov 2024)

**Architecture Finalisée:**
- [x] Décisions architecture complètes (5 Nov 2024)
- [x] PT100 3-wire acheté (40" lead wire PFA) ✅
- [x] Tube inox 316L acheté (3/8" OD × 0.28" ID × 6 pieds) ✅
- [x] End caps inox 316 (3/8") achetés ✅
- [x] Soudeuse TIG 200A disponible ✅
- [x] Configuration: Thermowell DIY over-the-top (clamp ajustable)
- [x] Longueur: 13" total (10" au-dessus + 2-3" immersion)
- [x] Plage mesure: 0-300°F (sirop + produits dérivés)

### 🛠️ Hardware PT100 - À FAIRE (Décembre 2024 - Janvier 2025)

**Semaine 1-2 (Maintenant - Mi-Nov):**
- [ ] Commander baguette ER316L 1/16" (~$12) **PRIORITÉ #1**
- [ ] Commander brosse inox dédiée (~$8)
- [ ] Prendre photos évaporateur (ensemble, rebord, profondeur)
- [ ] Découper tube en sections (6× 6", 2× 12", 1× 13")

**Semaine 3-4 (Mi-Nov - Fin Nov) - Pratique TIG:**
- [ ] Pratique soudure TIG sur 4-6 sections 6"
  - Settings: 30-40A (tube mince ~0.5mm wall)
  - Baguette ER316L 1/16"
  - Technique: Arc length 1.5-2mm, lent et constant
  - Post-flow 5 sec (protection inox)
- [ ] Souder 2-3 end caps (tests étanchéité)
- [ ] Maîtriser technique (avant thermowell final)

**Décembre 2024 - Prototypes & Électronique:**
- [ ] Prototype thermowell 12" (test complet)
- [ ] Si succès: Thermowell final 13"
- [ ] Test étanchéité (15 min immersion eau)
- [ ] Installer gland fitting 3/8" étanche
- [ ] Polir/finition thermowell
- [ ] Commander MAX31865 amplificateur (~$15)
- [ ] Commander lab clamp ajustable (~$25)
- [ ] Commander gaine spirale 1/4" (~$5)

**Décembre 2024 - Tests Électroniques:**
- [ ] Assembler: PT100 + MAX31865 + ESP32
- [ ] Code ESP32 lecture PT100
  - Interface SPI avec MAX31865
  - Filtrage: Moyenne mobile 10 lectures
  - Conversion RTD → température
  - Alarme critique hardcodée >160°C (sécurité)
- [ ] Tests bench eau bouillante
- [ ] Calibration point 1: Eau bouillante ~99.3°C (altitude Sainte-Marie)
- [ ] Tests précision: ±0.5°C minimum

**Janvier 2025 - Installation & Calibration:**
- [ ] Monter clamp ajustable sur rebord panne
- [ ] Installer thermowell (position: sensing 0.75-1" du fond)
- [ ] Installer PT100 dans thermowell (fit serré naturel)
- [ ] Câblage propre vers ESP32
  - Lead wire protégé par thermowell (zone chaude)
  - Gaine spirale après thermowell (zone fraîche)
  - Éviter zones très chaudes
- [ ] Calibration point 2: Sirop 66°Brix = 219°F (avec réfractomètre)
- [ ] Validation complète: Erreur <0.5°C sur 100-150°C
- [ ] Tests finaux avant saison

**Budget Hardware Total:** ~$130-150 CAD

### 🔧 Backend - Évaporateur (À FAIRE Post-Milestone 1)

**Models & API:**
- [ ] **App `production`** - Recettes & Sessions
  - [ ] Model CookingRecipe (6 recettes pré-configurées)
    - Sirop: 219°F (104°C)
    - Tire: 235-238°F
    - Beurre: 242-245°F
    - Sucre mou: 246-250°F
    - Sucre dur: 260-265°F
    - Bonbons: 290-300°F
  - [ ] Model CookingSession
    - Fields: recipe, start_time, end_time, notes, user
    - Relation: SensorReadings (tracking température)
    - Events: start, temp_reached, alarm, finish
  - [ ] Serializers + ViewSets
  - [ ] Endpoints:
    - `GET /api/production/recipes/` (liste recettes)
    - `POST /api/production/sessions/start/` (démarrer session)
    - `POST /api/production/sessions/{id}/finish/` (terminer)
    - `GET /api/production/sessions/{id}/readings/` (graph data)

- [ ] **SensorType "evaporator_temp_syrup"**
  - [ ] Plage: 0-300°F (0-150°C)
  - [ ] SensorReading avec metadata (alarmes, événements)
  - [ ] Index optimisés (timestamp, session_id)

- [ ] **Alarmes Configurables**
  - [ ] Model Alert (sensor_id, alert_type, severity, threshold)
  - [ ] Types alarmes:
    - Critique: >160°C (hardcoded ESP32 + backend)
    - Warning: Approche température cible (±5°F)
    - Info: Température cible atteinte
  - [ ] WebSocket push alarmes temps réel
  - [ ] Email/SMS notifications (optionnel Phase 2)

- [ ] **Analytics Sessions**
  - [ ] Calcul taux évaporation (L/h) si données volume
  - [ ] Temps cuisson total par session
  - [ ] Historique sessions (comparaison)
  - [ ] Export CSV données sessions

### 📱 Frontend - Dashboard Évaporateur (À FAIRE Post-Milestone 1)

**Page Évaporateur Principale:**
- [ ] Layout IonPage (Header + Content + BottomNav)
- [ ] Sélecteur recette (Dropdown avec 6 recettes)
  - Affiche température cible
  - Active alarmes selon recette sélectionnée

**Widget Température Temps Réel:**
- [ ] Gauge circulaire 0-300°F (Recharts ou custom)
  - Zones colorées selon recette:
    - Vert: Zone cible ±5°F
    - Jaune: Approche cible (±10°F)
    - Rouge: >160°C (danger)
  - Aiguille température actuelle
  - Texte digital: "235.4°F"

**Graphique Historique Session:**
- [ ] LineChart Recharts (temps vs température)
  - Axe X: Temps session (format HH:mm:ss)
  - Axe Y: Température (0-300°F)
  - Line stroke: maple-500
  - Grid dark mode (stone-700)
  - Marqueurs événements (démarrage, alarmes, fin)
  - Ligne horizontale: Température cible recette
  - Zone verte: ±5°F de cible
- [ ] Fenêtre temporelle: 2h glissantes
- [ ] Update temps réel (polling 5 sec ou WebSocket)

**Indicateurs Session:**
- [ ] Durée session en cours (chronomètre)
- [ ] Température actuelle (grande taille)
- [ ] Température cible (recette sélectionnée)
- [ ] Écart vs cible (+5.2°F / -3.1°F)
- [ ] Status: "En cours", "Température atteinte", "Terminée"

**Contrôles Session:**
- [ ] Bouton "Démarrer Session" (sélectionne recette)
  - Modal: Choisir recette + notes optionnelles
  - Commence tracking + chronomètre
- [ ] Bouton "Terminer Session" (actif seulement si session en cours)
  - Enregistre session complète avec données
  - Option: Ajouter notes finales
- [ ] Indicateur: "Session en cours" (badge orange)

**Alarmes Visuelles:**
- [ ] Toast notifications (IonToast)
  - Warning: "Approche température cible - 235°F"
  - Success: "Température cible atteinte! 🎯"
  - Danger: "ALERTE CRITIQUE - Température >160°C!" (rouge vif)
- [ ] Badge alarmes actives (header notification bell)
- [ ] Son alarme (optionnel, PWA notification API)
- [ ] Vibration mobile (Capacitor Haptics)

**Historique Sessions:**
- [ ] Liste sessions passées (filtre date)
- [ ] Card par session:
  - Recette utilisée
  - Date + durée
  - Température min/max/moyenne
  - Graphique miniature (sparkline)
  - Bouton "Voir détails" → Page session complète
- [ ] Page détails session:
  - Graphique complet temps vs temp
  - Timeline événements
  - Notes session
  - Export CSV session

**Page Analytics (Bonus Future):**
- [ ] Statistiques globales
  - Nombre sessions par recette
  - Durée moyenne par recette
  - Graphiques tendances (qualité, efficacité)
- [ ] Comparaison sessions (overlay graphiques)
- [ ] Corrélations (si données additionnelles futures)

### 🎯 Success Criteria Évaporateur - Saison 2025

**Minimum Viable (Must Have):**
- [ ] PT100 + thermowell installés, lectures stables (±0.5°C)
- [ ] ESP32 alarme critique >160°C fonctionne (sécurité hardware)
- [ ] Frontend affiche température temps réel
- [ ] Sélection recette + alarmes configurables
- [ ] Données sessions sauvegardées (historique complet)
- [ ] **ZÉRO batch brûlé grâce au monitoring!** 🎯

**Nice to Have (Bonus Saison 2025):**
- [ ] Précision ±0.2-0.3°C (avec bonne calibration)
- [ ] Export CSV sessions fonctionnel
- [ ] Historique sessions avec graphiques propres
- [ ] Comparaison sessions

**Future (Saison 2026+):**
- [ ] Capteur niveau ultrasonique (profondeur sirop)
- [ ] Capteur porte évaporateur (open/closed)
- [ ] Capteur débit eau (cooling coil)
- [ ] Analytics avancées (taux évaporation, efficacité)
- [ ] Automation optionnelle (valve eau motorisée PID)
- [ ] Classification IA qualité produits

### ⚠️ Points Critiques PT100

**Soudure TIG (CRITIQUE):**
- ⚠️ Pratiquer d'abord! 6× sections 6" avant thermowell final
- ⚠️ Settings bas (30-40A) - tube mince = burn-through facile
- ⚠️ Nettoyer impeccablement (acétone + brosse inox dédiée)
- ⚠️ Post-flow 5 sec obligatoire (protection inox chaud)
- ⚠️ Test étanchéité 15 min eau immersion AVANT installation

**Calibration (CRITIQUE):**
- ⚠️ Point 1: Eau bouillante ~99.3°C (ajusté altitude)
- ⚠️ Point 2: Sirop 66°Brix = 219°F (avec réfractomètre précis)
- ⚠️ Validation: Erreur <0.5°C sur plage 100-150°C
- ⚠️ Recalibration si dérive détectée (check hebdomadaire)

**Installation (CRITIQUE):**
- ⚠️ Position sensing: 0.75-1" du fond (toujours immergé niveau variable)
- ⚠️ Clamp stable: Bien serré, pas de vibration panne
- ⚠️ Lead wire protégé: Thermowell protège zone chaude (10"), gaine spirale après
- ⚠️ Gland étanche: Pas d'infiltration vapeur dans thermowell

**Probabilité Succès:** 85-95% avec pratique TIG (6× essais)  
**Backup Plan:** Atelier local soudure (~$30-50) si vraiment bloqué

---

## 🎯 MILESTONE 5 - Classification IA (Post-Saison 2026)

- [ ] Collecte données entraînement
- [ ] Modèle TensorFlow/PyTorch
- [ ] API prédiction + frontend

---

## 📅 TIMELINE RÉVISÉE (Avec PT100 en Parallèle)

### Janvier 2025 (EN COURS)
- ✅ Backend Auth complété
- ✅ Design Sprint complété
- ⏳ Frontend Login (cette semaine!)
- 🔧 PT100: Pratique TIG + thermowell final (en parallèle)

### Février 2025
- Frontend: Dashboard + Widget fonctionnel
- Backend: App IoT + organisations
- 🔧 PT100: Installation + calibration évaporateur
- **Milestone 1 complété: Dashboard MVP fonctionnel** ✅

### Mars 2025
- Milestone 2: Voyages d'eau + Barils + Quota
- 🔧 PT100: Tests finaux + ajustements

### Avril-Mai 2025 - SAISON DES SUCRES! 🍁
- **UTILISATION PRODUCTION RÉELLE**
- Monitoring: Thermomètre atmo + PT100 évaporateur ✅
- Gestion: Voyages d'eau + Barils + Quota
- **Collecte données pour analytics/IA future**

### Juin-Septembre 2025
- Milestone 3: Construction moniteur Brix (0-18°Brix)
- Calibration 7 points
- Code ESP32 Brix
- Frontend dashboard Brix

### Octobre 2025 - Janvier 2026
- Tests moniteur Brix hors saison
- Maintenance équipements
- Recalibration PT100 + Brix
- Préparation saison 2026

### Février-Mai 2026 - SAISON DES SUCRES 2026! 🍁
- **3 SYSTÈMES OPÉRATIONNELS:**
  1. Thermomètre atmosphérique ✅
  2. PT100 Évaporateur ✅
  3. Moniteur Brix 0-18°Brix ✅
- Collecte massive données
- Affinage algorithmes alarmes

### Post-Saison 2026
- Milestone 5: Classification IA
- Décision commercialisation

---

## 🎯 PRIORITÉS IMMÉDIATES (Option C: 9-12h/semaine)

### Cette Semaine (13-19 Janvier):
1. **Frontend Login** (3-4h) - PRIORITÉ #1
2. **PT100: Commander baguette ER316L** - PRIORITÉ #1
3. **Dashboard Skeleton** (3-4h)
4. **PT100: Photos évaporateur + découpe tube** (2h)

### Semaine Prochaine (20-26 Janvier):
1. **Widget fonctionnel** (3h)
2. **Backend IoT** (4h)
3. **PT100: Pratique TIG** (3-4h weekend)

### Fin Janvier:
- **Milestone 1 complété** ✅
- **PT100 thermowell final** (si pratique OK)

---

## 💪 PROBABILITÉ SUCCÈS TIMELINE

**Milestone 1 Frontend (Jan 2025):** 95% ✅  
- Tu codes 9-12h/semaine (Option C)
- Design déjà fait, backend prêt
- React learning curve incluse dans estimation

**PT100 Production (Fév 2025):** 85-90% ✅  
- Matériel déjà acheté
- Plan clair, progressif
- 6× essais pratique TIG avant final
- Backup: Atelier local si besoin

**Saison 2025 Opérationnelle:** 98% ✅  
- Timeline confortable (3 mois pour finaliser)
- PT100 + Dashboard = MVP suffisant
- Moniteur Brix non-critique pour 2025

**3 Systèmes Saison 2026:** 90% ✅  
- 1 an complet pour moniteur Brix
- Expérience saison 2025 acquise
- Hardware + Software maîtrisés

---

**Prochaine session:** Milestone 1c - Setup Ionic + Login Page  
**Documents prêts:** DESIGN_SPRINT_SUMMARY.md + QUICK_REFERENCE.md + SESSION_RECAP.md + NEXT_CONVERSATION_START.md + TODO_UPDATED.md  
**Hardware PT100:** Architecture finalisée, matériel acheté, prêt pour pratique TIG!  
**Let's ship! 🚀🔥**
