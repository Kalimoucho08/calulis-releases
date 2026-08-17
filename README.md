# Calulis — Téléchargement & Mises à jour

Application de gestion ULIS (Unité Localisée pour l'Inclusion Scolaire).
Suivi des élèves, adultes, réunions, emplois du temps, statistiques.

## 📥 Téléchargement

**Dernière version : v1.0.2**

[Télécharger Calulis v1.0.2](https://e.pcloud.link/publink/show?code=XZAEny7ZpgIcmPxVmCSqLFE8fmcv4hOFmOAV) (230 Mo, portable)

1. Extraire le ZIP n'importe où
2. Double-clic sur `Calulis.bat`
3. Au 1er lancement, choisir **Démo** (base pré-remplie) ou **Vierge** (départ à zéro)
4. L'application s'ouvre sur http://127.0.0.1:8088

Aucune installation — tout est embarqué (MySQL, PHP, interface web).

## 🔄 Mises à jour automatiques

À chaque démarrage, Calulis vérifie si une nouvelle version est disponible.
Si oui, il propose de la télécharger et de l'installer **automatiquement** :

- ✅ Patchs **incrémentaux** (quelques Ko) — seuls les fichiers modifiés sont téléchargés
- ✅ Vérification SHA-256 (quand le hash est renseigné dans le manifeste)
- ✅ Backup automatique avant chaque mise à jour
- ✅ Pas besoin de retélécharger le ZIP complet

## 📁 Structure du dépôt

- `manifest.json` — versions disponibles, patchs, lien de téléchargement complet
- `patches/` — archives des patchs incrémentaux

## 📦 Repo principal

Le code source et le développement sont sur [Kalimoucho08/calulis](https://github.com/Kalimoucho08/calulis).
