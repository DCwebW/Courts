# Courts

> Application mobile communautaire pour trouver, référencer et organiser des matchs sur des terrains de basketball en accès libre.

![React Native](https://img.shields.io/badge/React_Native-0.76-61DAFB?logo=react)
![Expo](https://img.shields.io/badge/Expo-52.0-000020?logo=expo)
![Firebase](https://img.shields.io/badge/Firebase-10.11-FFCA28?logo=firebase)
![License](https://img.shields.io/badge/License-Private-red)
![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS-lightgrey)

---

## A propos du projet

**Courts** est une application mobile développée avec React Native et Expo qui permet aux passionnés de basketball de localiser des terrains de proximité, de les référencer sur une carte interactive, et d'organiser des matchs en quelques secondes.

Le problème résolu est simple : trouver un terrain disponible et rassembler des joueurs est souvent laborieux. Courts centralise ces informations en un seul endroit. Les utilisateurs peuvent soumettre de nouveaux terrains (avec photo, adresse géolocalisée et type de filet), les sauvegarder en favoris, puis créer des matchs qui déclenchent automatiquement des notifications push vers tous les abonnés du terrain concerné.

L'application est construite autour d'une architecture **MVVM** (Model-View-ViewModel) claire : la logique métier est isolée dans le dossier `ModelView/`, les vues dans `components/screens/`, et les données sont persistées dans **Firebase Firestore** en temps réel. Les **Firebase Cloud Functions** assurent l'envoi automatique de notifications via le service Expo Push Notifications dès qu'un match est organisé sur un terrain suivi.

---

## Fonctionnalites

- Authentification par email/mot de passe avec Firebase Auth, réinitialisation de mot de passe et connexion OAuth Google
- Inscription avec validation côté client (format email, force du mot de passe, confirmation)
- Carte interactive affichant tous les terrains enregistrés avec marqueurs personnalisés (basketball) et cercle de proximité autour de la position de l'utilisateur
- Recherche de terrain par nom avec barre de recherche en temps réel, intégrée à la carte
- Fiche détaillée de chaque terrain : photo, adresse, type de filet (filet / chaînes / sans filet), bouton favori, signalement de présence, abonnement aux notifications
- Ajout de terrain communautaire avec saisie du nom, sélection du type de filet, géolocalisation via carte interactive et upload de photo vers Firebase Storage
- Organisation de matchs : sélection de la date, de l'heure, du type de match (via radio buttons) et du terrain parmi ses favoris
- Notifications push automatiques via Firebase Cloud Functions et Expo Server SDK lors de la création d'un match sur un terrain suivi
- Page d'accueil personnalisée affichant les terrains favoris de l'utilisateur (défilement horizontal) et ses matchs organisés
- Profil utilisateur avec modification du nom, prénom, photo de profil (Firebase Storage) et suppression de compte sécurisée (réauthentification obligatoire)
- Navigation hybride : drawer latéral + bottom tabs avec effet blur sur la barre de navigation
- Politique de confidentialité RGPD intégrée accessible depuis l'écran de connexion
- Conseils sport affichés en carrousel sur la page d'accueil

---

## Stack technique

### Frontend mobile
| Technologie | Version | Role |
|---|---|---|
| React Native | 0.76 | Framework mobile cross-platform |
| Expo | 52.0 | Toolchain et services natifs |
| React | 18.3.1 | Bibliotheque UI |
| React Navigation | 6.x | Navigation (Stack, Drawer, Bottom Tabs) |
| React Native Paper | 5.12 | Composants Material Design |
| React Native Maps | 1.20 | Carte interactive (Google Maps) |
| React Native Reanimated | 3.16 | Animations fluides |
| Expo Linear Gradient | 14.0 | Dégradés visuels |
| Expo Blur | 14.0 | Effet blur sur la bottom tab bar |
| Expo Image Picker | 16.0 | Sélection de photos depuis la galerie |
| Expo Location | 18.0 | Géolocalisation de l'utilisateur |
| Expo Notifications | 0.29 | Notifications push |
| React Native Modern Datepicker | 1.0 | Sélecteur de date |
| React Native Timer Picker | 1.5 | Sélecteur d'heure |
| Expo Google Fonts (Kanit, Inter) | 0.2 | Polices personnalisées |
| Moment.js | 2.30 | Manipulation de dates |

### Backend et données
| Technologie | Version | Role |
|---|---|---|
| Firebase Auth | 10.11 | Authentification utilisateurs |
| Firebase Firestore | 10.11 | Base de données NoSQL temps réel |
| Firebase Storage | 10.11 | Stockage des photos (terrains, profils) |
| Firebase Cloud Functions | 6.3 | Envoi automatique des notifications push |
| Expo Server SDK | 3.13 | Service de notifications push Expo |

### DevOps et CI/CD
| Technologie | Role |
|---|---|
| Docker Compose | Conteneurisation de Jenkins et SonarQube |
| Jenkins (LTS) | Serveur CI/CD avec webhook GitHub |
| SonarQube 9.9 Community | Analyse statique de la qualite du code |
| PostgreSQL | Base de données de SonarQube |
| GitHub Actions | Pipeline automatise de tests (branche master) |
| EAS (Expo Application Services) | Build APK Android (preview / production) |
| ngrok | Tunnel pour exposer Jenkins en local |

### Tests
| Technologie | Version | Role |
|---|---|---|
| Jest | 29.4 | Framework de tests unitaires |
| React Testing Library (RN) | 13.0 | Tests de composants React Native |
| Babel Jest | 29.7 | Transpilation pour les tests |

---

## Structure du projet

```
ApplicationCourts/           <- Racine du depot (documentation, maquettes, UML)
|
|-- DiagrammesUML/           <- Diagrammes UML du projet (StarUML)
|-- Wireframes et Maquette Graphique/
|-- Documentation mise en production/
|-- docker-compose.yml       <- Infrastructure CI/CD (Jenkins + SonarQube + PostgreSQL)
|
+-- ApplicationCourts/       <- Code source de l'application mobile
    |
    |-- App.js               <- Point d'entree : gestion auth et navigation racine
    |-- index.js             <- Enregistrement du composant racine Expo
    |-- ConfigFirebase2.js   <- Initialisation Firebase (Auth, Firestore, Storage)
    |-- app.json             <- Configuration Expo (permissions, icones, Google Maps API)
    |-- eas.json             <- Configuration des builds EAS (preview APK, production)
    |-- jest.config.js       <- Configuration Jest
    |-- babel.config.js      <- Configuration Babel
    |-- sonar-project.properties <- Cle du projet SonarQube
    |
    |-- components/
    |   |-- screens/         <- Toutes les pages de l'application (20 ecrans)
    |   |   |-- Login.js
    |   |   |-- Inscription.js
    |   |   |-- Home.js
    |   |   |-- AjoutTerrain.js
    |   |   |-- AjoutMatch.js
    |   |   |-- FicheTerrain.js
    |   |   |-- FicheMatch.js
    |   |   |-- ChangerInfos.js
    |   |   |-- TerrainsFavorisSelection.js
    |   |   |-- PolitiqueRGPD.js
    |   |   +-- ...
    |   |
    |   |-- navigation/     <- Navigateurs (DrawerNavigator, BottomTabNavigator, stacks)
    |   |-- Maps/           <- Composants carte (RechercheTerrainMap, marqueurs, choix adresse)
    |   |-- PageAccueil/    <- Widgets accueil (TerrainsFavoris, MatchsOrganises)
    |   |-- Modals/         <- Modales reutilisables (DatePicker, TimePicker, ChoixTerrain)
    |   |-- ThemeContext/   <- Contexte de theme global (FontContext, CustomText)
    |   |-- drawer/         <- Contenu du drawer lateral (CustomDrawerContent, ImagePicker)
    |   |-- ManipulationImages/
    |   |-- RadioButtonsGroup/
    |   |-- Logo/
    |   |-- BoutonValider.js
    |   +-- SignalementPresence.js
    |
    |-- ModelView/           <- Couche ViewModel (logique metier, appels Firestore)
    |   |-- fetchTerrains.js
    |   |-- EnvoiMatchDB.js
    |   |-- ajoutFavori.js
    |   |-- removeFavori.js
    |   |-- abonnementTerrainButton.js
    |   |-- SearchBarComponent.js
    |   +-- getFirebaseInstallationId.js
    |
    |-- functions/           <- Firebase Cloud Functions
    |   +-- index.js         <- Trigger Firestore : notification push a la creation d'un match
    |
    |-- tests/               <- Tests unitaires Jest
    |   |-- BoutonRetour.test.js
    |   |-- ConseilsSport.test.js
    |   |-- DrawerNavigation.test.js
    |   |-- SignInTest.test.js
    |   +-- createUser.test.js
    |
    |-- __mocks__/           <- Mocks Firebase et composants natifs pour Jest
    +-- assets/              <- Images, icones, polices
```

---

## Demarrage rapide

### Prerequis

- [Node.js](https://nodejs.org/) >= 18
- [npm](https://www.npmjs.com/) ou [yarn](https://yarnpkg.com/)
- [Expo CLI](https://docs.expo.dev/more/expo-cli/) : `npm install -g expo-cli`
- [EAS CLI](https://docs.expo.dev/build/setup/) (pour les builds) : `npm install -g eas-cli`
- Compte [Firebase](https://firebase.google.com/) avec un projet configure (Auth, Firestore, Storage, Functions)
- Compte [Expo](https://expo.dev/) (pour les notifications push)
- Cle API Google Maps (Android + iOS)

### Installation

1. Cloner le depot :
   ```bash
   git clone <url-du-depot>
   cd ApplicationCourts/ApplicationCourts
   ```

2. Installer les dependances :
   ```bash
   npm install
   ```

3. Configurer Firebase en modifiant `ConfigFirebase2.js` avec les identifiants de votre projet Firebase :
   ```js
   const firebaseConfig = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "..."
   };
   ```

4. Renseigner votre cle API Google Maps dans `app.json` (champs `ios.config.googleMapsApiKey` et `android.config.googleMaps.apiKey`).

5. Mettre a jour le `projectId` Expo dans `app.json` et `eas.json` avec l'identifiant de votre projet Expo.

### Lancement en developpement

```bash
# Demarrer le serveur de developpement Expo
npm start

# Lancer directement sur Android
npm run android

# Lancer directement sur iOS
npm run ios
```

Utiliser [Expo Go](https://expo.dev/go) sur un appareil physique ou un emulateur pour tester l'application.

### Build APK Android (avec EAS)

```bash
# Build preview (APK telechargeable)
eas build --profile preview --platform android

# Build release
eas build --profile production --platform android
```

### Lancer les tests

```bash
cd ApplicationCourts
npm test
```

### Deployer les Cloud Functions Firebase

```bash
cd ApplicationCourts/functions
npm install
firebase deploy --only functions
```

---

## Infrastructure CI/CD

Le projet inclut une infrastructure CI/CD complete pilotee par Docker Compose, documentee visuellement dans le dossier racine.

### Lancer l'environnement CI/CD local

```bash
# Depuis la racine du depot
docker-compose up -d
```

Cela demarre :
- **Jenkins** sur `http://localhost:8080` — serveur d'integration continue connecte a GitHub via webhook
- **SonarQube** sur `http://localhost:9000` — analyse statique de la qualite du code (cle projet : `Courts`)
- **PostgreSQL** — base de donnees interne a SonarQube

Le pipeline GitHub Actions (`.github/workflows/tests.yml`) se declenche a chaque push sur la branche `master` et execute automatiquement les tests unitaires Jest.

---

## Modele de donnees (Firestore)

| Collection | Documents | Description |
|---|---|---|
| `clients` | `{uid}` | Profil utilisateur (nom, prenom, email, photo) |
| `terrains` | `{terrainId}` | Terrain (nom, adresse, lat/lng, type filet, image, abonnements) |
| `terrainsfavoris` | `{docId}` | Liste des favoris par utilisateur (idUtilisateur, terrains[]) |
| `matchs` | `{matchId}` | Match organise (useruid, date, heure, terrain, terrainId, typematch) |

---

## Contribuer

Les contributions sont les bienvenues. Merci de creer une branche feature a partir de `main`, de vous assurer que les tests passent (`npm test`) et de soumettre une pull request avec une description claire des changements apportes.

---

## Licence

Projet prive — tous droits reserves.
Auteur : Cointre, Courts — 5 rue Jules Guesde, 94260 Fresnes.
