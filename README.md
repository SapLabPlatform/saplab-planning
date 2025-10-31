# saplab-planning
# 🍁 SapLab - TODO Master

**Projet:** Système de monitoring acéricole IoT avec Django/Ionic  
**Timeline:** 2025-2026 (Classification IA post-saison 2026)  
**Objectif Saison 2026:** 3 systèmes IoT opérationnels + fonctionnalités production essentielles

---

## 🎯 MILESTONE 1 (Cible: ~1 mois) - Quick Win Démontrable

**Objectif:** Dashboard fonctionnel avec auth + graphique pression atmosphérique en temps réel

### Backend Core (Django)
- [ ] **App `users`** - Authentification email custom
  - [ ] Model User (email login, pas username)
  - [ ] JWT tokens (django-rest-framework-simplejwt)
  - [ ] Endpoints: `/api/auth/login/`, `/api/auth/logout/`, `/api/auth/refresh/`
  - [ ] Tests unitaires auth
  
- [ ] **App `organizations`**
  - [ ] Model Organization (nom, type, info contact)
  - [ ] Model Cabane (lié à Organization, adresse, capacité)
  - [ ] Model Site (optionnel multi-sites)
  - [ ] Model Membership (User ↔ Organization, roles)
  - [ ] Serializers + ViewSets REST
  - [ ] Permissions (owner, admin, viewer)

- [ ] **App `iot`** - Infrastructure devices
  - [ ] Model Device (UUID, MAC address, type, cabane_id)
  - [ ] Model Sensor (lié à Device, type: température, pression, etc.)
  - [ ] Model SensorReading (timestamp, sensor_id, value, unit)
  - [ ] Endpoint provisioning: `POST /api/iot/devices/provision/`
    - Input: MAC address → Output: API token hashé
  - [ ] Endpoint ingestion: `POST /api/iot/readings/`
    - Auth: Device API token
    - Bulk insert optimisé (batch readings)
  - [ ] Index DB optimisés (timestamp, sensor_id)

- [ ] **Django Channels Configuration**
  - [ ] Redis channel layers configuré
  - [ ] WebSocket consumer pour readings temps réel
  - [ ] Route `/ws/sensors/{sensor_id}/`
  - [ ] Broadcasting: nouvelle lecture → push WebSocket clients connectés

- [ ] **App `equipment`** - Modélisation équipements physiques
  - [ ] Model EquipmentType (enum: osmose, évaporateur, réservoir, etc.)
  - [ ] Model Equipment (lié à Cabane, type, specs techniques)
  - [ ] Relation Equipment ↔ Device (1 équipement peut avoir N devices)

### Frontend Core (Ionic PWA)
- [ ] **Setup projet Ionic**
  - [ ] Init Ionic React/Vue (ton choix)
  - [ ] Configuration environnements (dev/prod API URLs)
  - [ ] Service Worker pour PWA (offline basic)
  - [ ] Splash screen + icônes

- [ ] **Auth Flow**
  - [ ] Page Login (email + password)
  - [ ] Service Auth (store JWT, refresh token)
  - [ ] Guards routes (redirect si non authentifié)
  - [ ] Page Logout

- [ ] **Dashboard Principal**
  - [ ] Layout responsive (header, sidebar, content)
  - [ ] Widget "Ma Cabane" (nom, température actuelle)
  - [ ] Graphique pression atmosphérique
    - [ ] Chart.js ou Recharts intégré
    - [ ] Axe X: temps (dernières 24h)
    - [ ] Axe Y: Pression (hPa)
    - [ ] WebSocket: update temps réel toutes les 10 sec
  - [ ] Indicateurs clés: température actuelle, dernière mise à jour

- [ ] **Navigation**
  - [ ] Menu: Dashboard, Devices, Production (placeholder), Paramètres
  - [ ] Page "Mes Devices" (liste devices provisionnés)

### Hardware - Thermomètre Atmosphérique
- [x] **Prototype fonctionnel** (ESP32 + BMP280 connectés)
- [ ] **Code ESP32 Production**
  - [ ] WiFi auto-reconnect robuste
  - [ ] Deep sleep entre lectures (économie batterie)
  - [ ] Envoi batch readings (buffer 10 mesures)
  - [ ] Gestion erreurs API (retry avec backoff exponentiel)
  - [ ] OTA updates (optionnel mais recommandé)
  
- [ ] **Provisioning Device**
  - [ ] Appeler `/api/iot/devices/provision/` avec MAC address
  - [ ] Stocker API token en EEPROM/NVS
  - [ ] LED status: bleu (connexion), vert (OK), rouge (erreur)

- [ ] **Boîtier & Installation**
  - [ ] Boîtier étanche IP65
  - [ ] Alimentation stable (USB ou batterie + panneau solaire?)
  - [ ] Montage cabane (position optimale)

### 🎁 BONUS: Capteur Transformation (Noël)
- [ ] **Nouveau type de sensor: "transformation_status"**
  - [ ] ESP32 avec input GPIO (bouton ou capteur binaire)
  - [ ] Envoyer événement quand transformation démarre/arrête
  - [ ] Backend: Model TransformationSession (start_time, end_time, notes)
  
- [ ] **Frontend: Page Transformation**
  - [ ] Bouton "Démarrer transformation"
  - [ ] Chronomètre en cours
  - [ ] Historique transformations

---

## 🎯 MILESTONE 2 (Post-Milestone 1) - Fonctionnalités Production Essentielles

**Objectif:** Système utilisable quotidiennement même sans capteurs avancés

### App `production`
- [ ] **Gestion Voyages d'Eau**
  - [ ] Model WaterMeasurement
    - Fields: date, volume_litres, measurement_source ('manual' ou 'sensor'), notes
    - Relation: Organization, User (qui a saisi)
  - [ ] Endpoint CRUD: `/api/production/water-measurements/`
  - [ ] Calcul quota PPAQ automatique
  - [ ] Frontend: Page "Voyages d'Eau"
    - Form ajout manuel
    - Liste avec filtres (date, source)
    - Widget quota: "850 / 1200 L utilisés (71%)"

- [ ] **Gestion Barils**
  - [ ] Model Barrel
    - Fields: qr_code, volume_litres, brix_degres, date_closed, status (ouvert/fermé)
    - Relation: ProductionSession (optionnel)
  - [ ] Endpoint: `POST /api/production/barrels/{id}/close/`
  - [ ] Génération étiquette PDF
    - Template: Nom cabane, date, volume, °Brix, QR code
    - Library: ReportLab ou WeasyPrint
  - [ ] Frontend: Page "Mes Barils"
    - Scanner QR code (Ionic native camera)
    - Form fermeture baril (volume, Brix manuel)
    - Télécharger étiquette PDF
    - Liste barils (filtres: ouverts/fermés, saison)

- [ ] **Suivi Quota PPAQ**
  - [ ] Model QuotaPPAQ (saison, quota_litres, Organization)
  - [ ] Calcul automatique: somme WaterMeasurement par saison
  - [ ] Alarme si quota > 90%
  - [ ] Frontend: Widget Dashboard + page détaillée

- [ ] **Timeline Saison**
  - [ ] Model SeasonEvent
    - Types: entaillage, première_coulée, dernier_voyage, nettoyage, etc.
    - Fields: event_type, date, notes, photos (optionnel)
  - [ ] Frontend: Page "Ma Saison"
    - Timeline visuelle (bibliothèque timeline React/Vue)
    - Ajout événements manuels

---

## 🎯 MILESTONE 3 (Hiver 2026) - Moniteur Brix Osmose

**Objectif:** Monitoring précision 0-18°Brix en continu pendant production

### Hardware - Moniteur Brix
- [ ] **Construction Chambre de Mesure**
  - [ ] Tuyau PVC Schedule 40 (1.5"), hauteur 120 cm
  - [ ] Capteur pression 0-100 kPa (membrane affleurante)
  - [ ] Sonde température DS18B20 (mi-hauteur)
  - [ ] ADS1115 (ADC 16 bits I2C)
  - [ ] Vanne d'aiguille haute pression (>400 psi)
  - [ ] Piège à bulles cyclonique
  - [ ] Soupape sécurité 150 kPa
  - [ ] Supports anti-vibration
  - [ ] Raccordement osmose (entrée bas, trop-plein haut)

- [ ] **Calibration 7 Points (0, 3, 6, 9, 12, 15, 18°Brix)**
  - [ ] Préparer solutions selon recettes document
  - [ ] Mesurer P_raw et T pour chaque point
  - [ ] Régression polynomiale quadratique: Brix = a·P² + b·P + c
  - [ ] Vérifier R² > 0.9995
  - [ ] Tests validation (répétabilité, précision, stabilité thermique)

- [ ] **Code ESP32 Brix**
  - [ ] Lecture ADS1115 (pression haute résolution)
  - [ ] Lecture DS18B20 (température)
  - [ ] Filtrage: moyenne mobile 20 lectures
  - [ ] Correction température: ρ(20°C) = ρ(T) × [1 + 0.0002(T - 20)]
  - [ ] Conversion: Brix = a·P² + b·P + c
  - [ ] Détection anomalies:
    - Rejeter si Brix < -1 ou > 20
    - Alarme si changement > 2°Brix/sec (bulles)
    - Alarme si P_raw < 10 kPa ou > 22 kPa
  - [ ] Envoi MQTT ou HTTP vers API

### Backend - Intégration Brix
- [ ] **Nouveau SensorType: "brix"**
  - [ ] SensorReading: value = degrés Brix, metadata JSON (P_raw, T, alarmes)
  - [ ] Endpoint analytics: `/api/analytics/brix/stats/` (min/max/avg par période)

- [ ] **Alarmes intelligentes**
  - [ ] Model Alert (sensor_id, alert_type, severity, timestamp, resolved)
  - [ ] WebSocket push alarmes temps réel
  - [ ] Email/SMS notifications (Twilio ou autre service)

### Frontend - Dashboard Brix
- [ ] **Widget Brix Temps Réel**
  - [ ] Gauge circulaire 0-18°Brix (couleur gradient)
  - [ ] Graphique ligne 24h (Brix vs temps)
  - [ ] Indicateurs: P_raw, Température, status

- [ ] **Page Analytics Brix**
  - [ ] Graphiques historiques (jour/semaine/saison)
  - [ ] Statistiques: moyenne, min/max, écart-type
  - [ ] Export CSV données

- [ ] **Gestion Alarmes**
  - [ ] Liste alarmes actives
  - [ ] Historique alarmes
  - [ ] Bouton "Résoudre alarme" (acknowledge)

### Maintenance & Calibration
- [ ] **Protocoles maintenance**
  - [ ] CIP hebdomadaire (acide citrique 3%, 40°C, 15 min)
  - [ ] Rinçage quotidien (eau chaude 5 min)
  - [ ] Vérification calibration hebdomadaire (solution 12°Brix)
  - [ ] Recalibration complète mensuelle

- [ ] **Frontend: Page Maintenance**
  - [ ] Checklist maintenance quotidienne/hebdomadaire
  - [ ] Logging maintenance effectuée
  - [ ] Alertes maintenance overdue

---

## 🎯 MILESTONE 4 (Printemps 2026) - Évaporateur Monitoring

**Objectif:** Monitoring température, pression, niveau sirop évaporateur

### Hardware - Évaporateur
- [ ] **Capteurs**
  - [ ] Thermocouples Type K (température sirop, température fumée)
  - [ ] Capteur niveau ultrasonique (profondeur sirop)
  - [ ] Capteur pression différentielle (tirage cheminée)
  - [ ] ESP32 avec MAX31855 (amplificateur thermocouple)

- [ ] **Code ESP32 Évaporateur**
  - [ ] Lecture multi-capteurs
  - [ ] Alarmes critiques:
    - Température > 120°C (risque brûlure)
    - Niveau < seuil critique (risque brûlure plaque)
    - Perte tirage cheminée
  - [ ] Contrôle optionnel: valve admission air (PID)

### Backend - Intégration Évaporateur
- [ ] **Nouveaux SensorTypes**
  - [ ] "evaporator_temp_syrup", "evaporator_temp_smoke", "evaporator_level"
  - [ ] SensorReading avec metadata (alarmes, contexte)

- [ ] **Analytics Évaporateur**
  - [ ] Calcul taux d'évaporation (L/h)
  - [ ] Efficacité énergétique (L sirop / kg bois)
  - [ ] Temps cuisson par batch

### Frontend - Dashboard Évaporateur
- [ ] **Page Évaporateur**
  - [ ] Température sirop (gauge + graphique)
  - [ ] Niveau sirop (barre horizontale + alarme visuelle)
  - [ ] Indicateur tirage cheminée
  - [ ] Historique sessions évaporation

---

## 🎯 MILESTONE 5 (Post-Saison 2026) - Classification IA

**Objectif:** Prédiction qualité sirop (couleur, classification) basée sur données sensors

### App `classification`
- [ ] **Collecte données entraînement**
  - [ ] Model SyrupSample (photos, mesures réfractomètre, classification manuelle)
  - [ ] Association samples ↔ SensorReadings (conditions production)
  
- [ ] **Modèle IA**
  - [ ] TensorFlow/PyTorch: classification couleur sirop
  - [ ] Features: Brix, température, temps cuisson, etc.
  - [ ] Training pipeline (Jupyter notebooks)
  - [ ] API endpoint: `POST /api/classification/predict/`

- [ ] **Frontend**
  - [ ] Upload photo sirop
  - [ ] Prédiction classification automatique
  - [ ] Dashboard analytics: corrélations conditions ↔ qualité

---

## 📦 BACKLOG - Fonctionnalités Futures

### Priorité Moyenne
- [ ] **Multi-utilisateurs avancé**
  - [ ] Rôles granulaires (admin, opérateur, viewer)
  - [ ] Audit log (qui a fait quoi, quand)
  
- [ ] **Rapports PPAQ Automatiques**
  - [ ] Génération PDF rapport annuel
  - [ ] Export Excel données quotidiennes

- [ ] **Gestion Inventaire**
  - [ ] Stock sucre, produits finis
  - [ ] Alertes réapprovisionnement

- [ ] **Intégrations Externes**
  - [ ] Météo (API OpenWeatherMap)
  - [ ] Comptabilité (export QuickBooks/Sage)

### Basse Priorité
- [ ] **App Mobile Native** (si PWA insuffisante)
- [ ] **Tableau de bord public** (partage stats anonymes)
- [ ] **Marketplace équipements** (si commercialisation)

---

## 🛠️ Infrastructure & DevOps

### Setup Initial
- [x] Docker Compose (PostgreSQL, Redis, Django)
- [ ] **CI/CD Pipeline**
  - [ ] GitHub Actions: tests automatiques
  - [ ] Deploy staging automatique (push main)
  - [ ] Deploy production manuel (tag release)

### Production Readiness (Avant commercialisation 2027)
- [ ] **Sécurité**
  - [ ] HTTPS obligatoire (Let's Encrypt)
  - [ ] Rate limiting API (django-ratelimit)
  - [ ] Audit security (OWASP Top 10)
  
- [ ] **Monitoring**
  - [ ] Sentry (error tracking)
  - [ ] Prometheus + Grafana (métriques)
  - [ ] Uptime monitoring (UptimeRobot ou Pingdom)

- [ ] **Backups**
  - [ ] Backup PostgreSQL quotidien (S3 ou autre)
  - [ ] Backup Redis (si données critiques)
  - [ ] Plan disaster recovery

- [ ] **Documentation**
  - [ ] README installation
  - [ ] Guide utilisateur (vidéos?)
  - [ ] API documentation (Swagger/OpenAPI)

---

## 📅 Planning Saison 2026

### Décembre 2024 - Janvier 2025
- ✅ Milestone 1: Dashboard + Thermomètre atmo fonctionnel

### Février - Mars 2025
- Milestone 2: Fonctionnalités production (voyages, barils, quota)
- Milestone 3 (début): Construction chambre Brix, calibration

### Avril - Mai 2025 (Saison Sucres!)
- **UTILISATION RÉELLE EN PRODUCTION**
- Monitoring quotidien: thermomètre, voyages d'eau, barils
- Tests terrain moniteur Brix (si prêt)
- Collecte données pour IA

### Juin - Septembre 2025
- Milestone 3 (finition): Affinage Brix (dérive, maintenance)
- Milestone 4: Développement évaporateur

### Octobre 2025 - Janvier 2026
- Milestone 4 (finition): Tests évaporateur hors saison
- Préparation saison 2026 (maintenance équipements, recalibration)

### Février - Mai 2026 (Saison Sucres 2026)
- **3 SYSTÈMES OPÉRATIONNELS**
- Collecte massive données pour IA
- Affinage algorithmes alarmes

### Post-Saison 2026
- Milestone 5: Développement classification IA
- Décision commercialisation

---

## 📝 Notes & Décisions Architecturales

### Auth Devices ESP32
- Token statique (pas de refresh)
- Provisioning par MAC address
- Token hashé en DB (bcrypt ou Argon2)

### UUID vs ID Auto-increment
- **UUID:** User, Organization, Device, Sensor, Barrel (API publique)
- **ID:** Relations internes, time-series (performance)

### Gestion Temps
- Tous timestamps en UTC
- Frontend: conversion timezone utilisateur
- SensorReading: index composite (timestamp, sensor_id)

### WebSocket vs Polling
- WebSocket pour dashboard temps réel
- Polling fallback si WebSocket échoue
- Ionic: Capacitor Network plugin (détection connexion)

### Offline-First (Future)
- Service Worker cache API calls
- Queue lectures hors ligne (IndexedDB)
- Sync automatique au retour connexion

---

## ✅ Critères de Succès Saison 2026

### Fonctionnel
- [ ] Aucune perte de données capteurs (uptime >99%)
- [ ] Précision Brix: ±0.3°Brix en conditions réelles
- [ ] Alarmes critiques: 0 faux négatifs (pas de batch brûlé)

### Utilisabilité
- [ ] Temps ajout voyage d'eau: <30 secondes
- [ ] Dashboard chargé en <2 secondes (4G)
- [ ] 0 bugs bloquants en production

### Business (Si commercialisation)
- [ ] 3-5 producteurs beta-testeurs intéressés
- [ ] ROI démontré: économie temps >20h/saison
- [ ] Feedback utilisateurs: NPS >8/10

---

**Dernière mise à jour:** 2024-12-XX  
**Prochaine révision:** Fin Milestone 1
