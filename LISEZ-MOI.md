# Cube Dash : fabriquer le fichier AAB pour Google Play

Ce dossier contient le jeu (www/index.html) et la configuration Capacitor.
Il faut un ordinateur (Windows, Mac ou Linux). Le fichier AAB ne peut pas être
créé dans le chat : il faut les outils Android et ta propre clé de signature.

## 1. Installer les outils (une seule fois)
- Node.js (version LTS) : https://nodejs.org
- Android Studio : https://developer.android.com/studio

## 2. Préparer le projet (dans un terminal, dans ce dossier)
    npm install @capacitor/core @capacitor/android
    npm install -D @capacitor/cli
    npx cap add android
    npx cap sync android

Avant de continuer, ouvre capacitor.config.json et remplace "com.tonnom.cubedash"
par un identifiant à toi, unique et définitif (exemple : com.tonpseudo.cubedash).
Fais-le AVANT « npx cap add android » : il ne pourra plus changer après publication.

## 3. Verrouiller le mode portrait
Ouvre android/app/src/main/AndroidManifest.xml et ajoute dans la balise <activity> :
    android:screenOrientation="portrait"

## 4. Icône de l'appli
Dans Android Studio : clic droit sur « app » > New > Image Asset, puis choisis ton icône.
Ne reprends pas le logo ni le nom d'un autre jeu.

## 5. Générer l'AAB signé
    npx cap open android
Puis dans Android Studio : Build > Generate Signed App Bundle / APK > Android App Bundle.
- Crée une clé (« Create new keystore ») et SAUVEGARDE le fichier et les mots de passe
  en plusieurs endroits : sans eux, tu ne pourras plus mettre à jour l'appli.
- Choisis « release ». Le fichier .aab est créé dans android/app/release/.
- Avant chaque mise à jour, augmente versionCode (et versionName) dans android/app/build.gradle.

## 6. Publier sur Google Play
1. Crée un compte développeur sur https://play.google.com/console (paiement unique, vérification d'identité).
2. Crée l'application, puis dépose le fichier .aab dans une version (test interne d'abord).
3. Remplis les formulaires obligatoires : fiche du store (description, captures, icône 512x512,
   image de présentation), classification du contenu, public cible, « Sécurité des données »,
   et l'adresse d'une politique de confidentialité (une simple page web suffit).
4. Vérifie dans la console le niveau d'API cible exigé (il change chaque année) et mets à jour
   Capacitor si besoin : npm install @capacitor/core@latest @capacitor/android@latest @capacitor/cli@latest
5. Les comptes personnels récents doivent d'abord faire un test fermé avec un minimum de testeurs
   pendant une durée minimale avant la publication : lis les règles actuelles dans la console.

## Points légaux à vérifier
- N'utilise pas « Geometry Dash » (ni ses images, sons, musiques, icônes) dans le nom,
  la description ou les captures : c'est une marque d'un autre studio. Vérifie aussi que le
  nom « Cube Dash » n'est pas déjà pris sur le Play Store.
- Les pièces bleues du jeu sont virtuelles et gratuites (aucun achat réel dans l'appli).
- Le jeu enregistre seulement ta progression dans l'appareil : indique-le dans la politique
  de confidentialité et dans « Sécurité des données ».
