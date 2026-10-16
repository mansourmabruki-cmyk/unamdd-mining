# UNAMDD Mining Sarl — Application de cartographie minière (RDC)

APK Android de cartographie du cadastre minier **CAMI** (RDC), hors-ligne d'abord,
inspirée d'Ovital mais enrichie de couches métier (sites IPIS, vallées alluviales,
carrés CAMI, assistant Géo-IA). Toute l'application est dans `www/index.html`.

**UNAMDD Mining Sarl** — Union Nationale des Marginalisés pour un Développement Durable
**Chef du bureau technique : Ir MANSOUR MAB**

---

## ✅ Obtenir l'APK sans rien installer (recommandé)

Ce dépôt compile l'APK tout seul grâce à **GitHub Actions**.

1. Créez un dépôt GitHub et poussez-y ce dossier :
   ```bash
   git init
   git add .
   git commit -m "UNAMDD Mining — app initiale"
   git branch -M main
   git remote add origin https://github.com/<votre-compte>/unamdd-mining.git
   git push -u origin main
   ```
2. Sur GitHub, ouvrez l'onglet **Actions**. Le workflow
   *« Build Android APK (UNAMDD Mining) »* se lance automatiquement
   (ou cliquez **Run workflow**).
3. À la fin, ouvrez l'exécution terminée > section **Artifacts** >
   téléchargez **UNAMDD-Mining-APK** : c'est votre fichier `.apk`.
4. Pour créer en plus une **Release** publique avec l'APK, poussez un tag :
   ```bash
   git tag v1.0.0 && git push origin v1.0.0
   ```

Installez l'APK sur un téléphone Android (activez « Sources inconnues »).

---

## 💻 Compiler en local (optionnel)

Voir `CONSTRUIRE_L_APK.md` (prerréquis Android Studio + 3 commandes Cordova).

---

## 📁 Structure

```
.github/workflows/build-apk.yml   # CI : compile l'APK automatiquement
www/index.html                    # L'application complète (UI, carte, Géo-IA)
config.xml                        # Config Cordova (nom, permissions GPS)
package.json                      # Dépendances Cordova
CONSTRUIRE_L_APK.md               # Guide de build local + travaux restants
```

## 🚧 Vers la version production

L'interface est complète ; restent (voir dossier de conception) :
fonds de carte hors-ligne (MBTiles/PMTiles), vraies données CAMI/IPIS/OSM dans
SQLite embarqué, synchro incrémentale sur le backend FastAPI/PostGIS, imagerie
satellite licenciée. Les données actuelles sont des échantillons de démonstration.
