# Calulis — Téléchargement & Mises à jour

Application de gestion ULIS (Unité Localisée pour l'Inclusion Scolaire).
Suivi des élèves, adultes, réunions, emplois du temps, statistiques.

## 📥 Téléchargement

**Dernière version : v1.12.1** (lanceur **1.0.11**)

[Télécharger Calulis v1.12.1](https://e.pcloud.link/publink/show?code=XZtIzk7ZUl5n83C3F455gIY5SzEMEJCWkkD7) (~228 Mo, portable)

> Le ZIP complet embarque le lanceur **1.0.10** : au premier démarrage, Calulis propose le
> lanceur **1.0.11** (~60 Mo) — il s'installe tout seul et sera actif au démarrage suivant.

1. Extraire le ZIP n'importe où (clic droit → « Extraire tout »)
2. Double-clic sur `Calulis.bat`
3. Au 1er lancement, choisir **Démo** (base pré-remplie) ou **Vierge** (départ à zéro)
4. L'application s'ouvre sur http://127.0.0.1:8088

Aucune installation — tout est embarqué (MySQL, PHP, interface web, runtime Visual C++).

⚠️ Windows demande l'autorisation **pare-feu** au premier lancement (MySQL et PHP écoutent
**uniquement en 127.0.0.1**) : « Annuler » est sans conséquence. Le premier démarrage peut être
lent (initialisation de la base) ; les attentes du lanceur sont de 180 s.

## 🔄 Mises à jour automatiques

À chaque démarrage, Calulis vérifie si une nouvelle version est disponible.
Si oui, il propose de la télécharger et de l'installer **automatiquement** :

- ✅ Patchs **incrémentaux** (quelques Ko) — seuls les fichiers modifiés sont téléchargés
- ✅ Vérification SHA-256 (quand le hash est renseigné dans le manifeste)
- ✅ Backup automatique avant chaque mise à jour
- ✅ Pas besoin de retélécharger le ZIP complet

Chaque version publiée a une route de mise à jour vers la dernière. Cas particulier : la route
`1.12 → 1.12.1` a été **ajoutée le 28/09/2026** — sans elle, un poste resté en **1.12** (version
distribuée du 22 au 26/09/2026) se voyait répondre « À jour (1.12) » et n'apprenait jamais
l'existence de la 1.12.1.

## 📁 Structure du dépôt

- `manifest.json` — versions disponibles, patchs, lien de téléchargement complet
- `patches/` — archives des patchs incrémentaux
- `launcher/` — archives du lanceur (`Calulis.exe`, remplacé automatiquement)

## 📦 Repo principal

Le code source et le développement sont sur [Kalimoucho08/calulis](https://github.com/Kalimoucho08/calulis).
