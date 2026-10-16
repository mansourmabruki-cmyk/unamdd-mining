# UNAMDD Mining Sarl — Générer l'APK

Projet mobile prêt à compiler (Apache Cordova) de l'application de cartographie
minière hors-ligne du cadastre CAMI (RDC). Toute l'application se trouve dans
`www/index.html` (interface, carte, couches, relevés, Géo-IA).

> **Pourquoi l'APK n'est pas déjà compilée dans la livraison ?**
> La compilation d'une APK Android exige le SDK Android + Gradle, non
> disponibles dans mon environnement de génération (et sans accès Internet pour
> les installer). Je livre donc le **projet complet prêt à compiler** : la
> commande ci-dessous produit le fichier `.apk` en une seule étape sur votre
> poste.

---

## Prérequis (une seule fois)

1. **Node.js** (≥ 16) : https://nodejs.org
2. **JDK 17** (ou 11) : https://adoptium.net
3. **Android Studio** (fournit le SDK + Gradle) : https://developer.android.com/studio
   - Dans Android Studio > SDK Manager, installez : *Android SDK Platform 34*,
     *Android SDK Build-Tools 34*, *Android SDK Command-line Tools*.
   - Définissez la variable d'environnement `ANDROID_SDK_ROOT` vers le dossier SDK
     (ex. `~/Android/Sdk`).
4. **Cordova** :
   ```bash
   npm install -g cordova
   ```

## Compiler l'APK (3 commandes)

Depuis ce dossier :

```bash
cordova platform add android     # ajoute la plateforme Android
cordova build android            # APK de débogage
```

L'APK de débogage est générée ici :
```
platforms/android/app/build/outputs/apk/debug/app-debug.apk
```
Copiez ce fichier sur un téléphone Android et installez-le
(activez « Sources inconnues »).

### APK signée pour distribution (release)
```bash
cordova build android --release -- --keystore=unamdd.keystore --alias=unamdd
```
(Créez d'abord la clé : `keytool -genkey -v -keystore unamdd.keystore -alias unamdd -keyalg RSA -keysize 2048 -validity 10000`.)

## Alternative sans installer le SDK : build dans le cloud
- GitHub Actions (workflow Android), ou un service de build Cordova/Capacitor en
  ligne. Poussez ce dossier dans un dépôt et lancez le workflow.

---

## État de cette version et travaux restants pour le « très complet »

Cette version est une **maquette fonctionnelle complète côté interface** :
accueil globe+logo, sélection de province, carte multi-couches (plan OSM +
satellite Esri), villages/rivières, vallées alluviales, sites IPIS, carrés CAMI,
GPS, fiche de site, relevé de terrain, mesure de superficie, assistant Géo-IA.

Pour la version **production** réellement hors-ligne et alimentée en vraies
données, il reste à réaliser (détaillé dans le dossier de conception) :

1. **Fonds de carte hors-ligne** : embarquer des tuiles locales MBTiles/PMTiles
   (plan + corridors satellite 5–10 km) et servir Leaflet/MapLibre en local au
   lieu des CDN.
2. **Données réelles** dans une base SQLite embarquée : import de l'export
   officiel du cadastre CAMI, des jeux IPIS et des extraits OpenStreetMap
   (actuellement : échantillons de démonstration générés localement).
3. **Synchro incrémentale** branchée sur le backend cloud (FastAPI/PostGIS déjà
   conçu) pour l'actualisation des carrés à chaque connexion.
4. **Imagerie satellite** avec droits de rediffusion en production (Esri = démo).

---
UNAMDD Mining Sarl — Union Nationale des Marginalisés pour un Développement Durable
Chef du bureau technique : Ir MANSOUR MAB
