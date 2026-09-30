# Calulis — Téléchargement & Mises à jour

Application de gestion ULIS (Unité Localisée pour l'Inclusion Scolaire).
Suivi des élèves, adultes, réunions, emplois du temps, statistiques.

## 📥 Téléchargement

🌐 **Page de téléchargement (adresse stable, à partager)** :
<https://kalimoucho08.github.io/calulis-releases/> — elle est **fabriquée à partir de
`manifest.json`** par `scripts/generer-page-telechargement.py` (dépôt principal), jamais écrite à la
main : elle ne peut pas annoncer une autre version que celle que le lanceur installe.

**Dernière version : v1.13** (lanceur **1.0.11**)

[Télécharger Calulis v1.13](https://e.pcloud.link/publink/show?code=XZiEQk7ZdVzQJnrpdWQuo0hi82lGvQOd1AX0) (~228 Mo, portable)

> Le ZIP complet embarque cette fois **le lanceur 1.0.11** : plus rien à télécharger au premier
> démarrage. Le paquet contient aussi `THIRD-PARTY-NOTICES.md` (licences des composants).

1. Extraire le ZIP n'importe où (clic droit → « Extraire tout »)
2. Double-clic sur `Calulis.bat`
3. Dans la fenêtre du lanceur, cliquer sur **Démarrer**
4. Choisir **Base Démo** (données d'exemple) ou **Base Vierge** (départ à zéro)
5. L'application s'ouvre sur http://127.0.0.1:8088

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

Chaque version publiée a une route de mise à jour **directe** vers la dernière. Ce n'est pas un
confort : le lanceur **refuse** un patch dont la version d'arrivée est plus ancienne que
`latestVersion` (garde-fou contre la redistribution d'une version retirée). Autrement dit, dès que
`latestVersion` avance, **toutes** les routes existantes deviennent inapplicables : une version sans
route directe reste bloquée, sans message.

C'est ce qui est arrivé deux fois, et c'est pourquoi la 1.13 publie **trois** routes :

| Version installée | Route vers la 1.13 |
|---|---|
| `1.12.1` (distribuée depuis le 28/09) | `patch-1.12.1-1.13.zip` |
| `1.12` (distribuée du 22 au 28/09) | `patch-1.12-1.13.zip` |
| `1.11` (distribuée du 07 au 22/09) | `patch-1.11-1.13.zip` |

Les routes plus anciennes (`1.0.x`, `1.10`) ne sont plus applicables : leurs postes doivent
réinstaller le ZIP complet (les données se restaurent par Sauvegarde/Restauration).

## 📁 Structure du dépôt

- `manifest.json` — versions disponibles, patchs, lien de téléchargement complet
- `patches/` — archives des patchs incrémentaux
- `launcher/` — archives du lanceur (`Calulis.exe`, remplacé automatiquement)

## 📦 Repo principal

Le code source et le développement sont sur [Kalimoucho08/calulis](https://github.com/Kalimoucho08/calulis).
