# Calulis — Téléchargement & Mises à jour

Application de gestion ULIS (Unité Localisée pour l'Inclusion Scolaire).
Suivi des élèves, adultes, réunions, emplois du temps, statistiques.

## 📥 Téléchargement

🌐 **Page de téléchargement (adresse stable, à partager)** :
<https://kalimoucho08.github.io/calulis-releases/> — elle est **fabriquée à partir de
`manifest.json`** par `scripts/generer-page-telechargement.py` (dépôt principal), jamais écrite à la
main : elle ne peut pas annoncer une autre version que celle que le lanceur installe.

**Dernière version : v1.15** (lanceur **1.0.12**)

[Télécharger Calulis v1.15](https://e.pcloud.link/publink/show?code=XZicnk7Z4BAH4IhjUyjWnPIq5coa2bX9HhOX) (~228 Mo, portable)

Nouveautés de la 1.15 :

- **Suivi des élèves** : des notes datées et rattachées à un élève, avec un type (observation,
  objectif, réussite, alerte, action). Filtres par élève, type ou période, sélection par case et
  impression en PDF — pour préparer une ESS, un PAI ou un livret.
- **Tâches** : un tableau de post-its en cinq colonnes (à faire, plus tard, en cours, fait, annulé)
  et une liste triable ; échéance, priorité, six couleurs, lien vers un élève ou un adulte. Le
  statut se change en glissant une carte ou par le menu « Déplacer vers », qui marche au clavier.
  Une tâche terminée ou annulée n'est plus signalée « en retard ».
- **Impression des tâches** : ce qui reste à faire, ce qui a été fait sur une période, ou une
  sélection cochée.
- **Tableau de bord** : les tâches du jour (retard compris), avec une option pour celles de demain.
- **Emploi du temps** : l'« Agenda » change de nom, et la barre latérale est rangée par fréquence
  d'usage, le suivi et les tâches juste sous le tableau de bord.
- **Correction RGPD** : les durées de conservation annoncées étaient fausses. Un élève suivi en
  ULIS y reste cinq à sept ans et toutes ses données sont conservées pendant ce temps ; après sa
  sortie, deux ans. Les comptes rendus de réunions suivent désormais l'élève.
- La **base de démonstration** est enrichie : les deux nouveaux écrans sont visibles dès le premier
  lancement.

> Le ZIP complet embarque **le lanceur 1.0.12** : plus rien à télécharger au premier démarrage. Le
> paquet contient aussi `THIRD-PARTY-NOTICES.md` (licences des composants).

1. Extraire le ZIP n'importe où (clic droit → « Extraire tout »)
2. Double-clic sur `Calulis.bat`
3. Dans la fenêtre du lanceur, cliquer sur **Démarrer**
4. Choisir **Base Démo** (données d'exemple) ou **Base Vierge** (départ à zéro)
5. L'application s'ouvre sur http://127.0.0.1:8088

Aucune installation — tout est embarqué (MySQL, PHP, interface web, runtime Visual C++).

⚠️ Windows demande l'autorisation **pare-feu** au premier lancement (MySQL et PHP écoutent
**uniquement en 127.0.0.1**) : « Annuler » est sans conséquence. Le premier démarrage peut être
lent (initialisation de la base) ; les attentes du lanceur sont de 180 s.

## 🆘 Calulis ne démarre plus ? Sauvegarder vos données

Un **outil de sauvegarde**, séparé de l'application, met vos données à l'abri quand Calulis refuse
de s'ouvrir : il cherche votre installation, **copie d'abord** le dossier `runtime\data` (la base),
recopie les journaux utiles au diagnostic, puis déplace le lancement automatique dans la sauvegarde.
Il ne supprime rien, ne désinstalle rien, et ne coupe jamais la base de données.

[⬇️ Télécharger l'outil de sauvegarde (14 Ko)](https://e.pcloud.link/publink/show?code=XZdn0k7ZLRfJIYkWjjB5AzqzuUwPVm09p67k)

Un double-clic suffit (une confirmation est demandée avant toute action) ; le dossier de sauvegarde
s'ouvre sur le Bureau à la fin. Envoyez alors `rapport-secours-calulis.txt`.

Empreinte SHA-256 : `1d07f5ed0c7a920a9240292decff1db25b00fdd37da139152341895a96d8f011` (outil v2.2).
La [page de téléchargement](https://kalimoucho08.github.io/calulis-releases/#secours) rappelle la
version et l'empreinte de l'outil en cours : c'est elle qui fait foi.

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

C'est ce qui est arrivé deux fois, et c'est pourquoi la 1.15 publie **cinq** routes :

| Version installée | Route vers la 1.15 |
|---|---|
| `1.14` (distribuée depuis le 01/10) | `patch-1.14-1.15.zip` |
| `1.13` (distribuée du 29/09 au 01/10) | `patch-1.13-1.15.zip` |
| `1.12.1` (distribuée du 28/09 au 29/09) | `patch-1.12.1-1.15.zip` |
| `1.12` (distribuée du 22 au 28/09) | `patch-1.12-1.15.zip` |
| `1.11` (distribuée du 07 au 22/09) | `patch-1.11-1.15.zip` |

Les routes plus anciennes (`1.0.x`, `1.10`) ne sont plus applicables : leurs postes doivent
réinstaller le ZIP complet (les données se restaurent par Sauvegarde/Restauration).

## 📁 Structure du dépôt

- `manifest.json` — versions disponibles, patchs, lien de téléchargement complet
- `patches/` — archives des patchs incrémentaux
- `launcher/` — archives du lanceur (`Calulis.exe`, remplacé automatiquement)

## 📦 Repo principal

Le code source et le développement sont sur [Kalimoucho08/calulis](https://github.com/Kalimoucho08/calulis).
