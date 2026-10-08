# Calulis — Téléchargement & Mises à jour

Application de gestion ULIS (Unité Localisée pour l'Inclusion Scolaire).
Suivi des élèves, adultes, réunions, emplois du temps, statistiques.

## 📥 Téléchargement

🌐 **Page de téléchargement (adresse stable, à partager)** :
<https://kalimoucho08.github.io/calulis-releases/> — elle est **fabriquée à partir de
`manifest.json`** par `scripts/generer-page-telechargement.py` (dépôt principal), jamais écrite à la
main : elle ne peut pas annoncer une autre version que celle que le lanceur installe.

**Dernière version : v1.16** (lanceur **1.0.15**)

[Télécharger Calulis v1.16](https://e.pcloud.link/publink/show?code=XZGidk7ZIqhQ4ppkRSLrjgmxash15pNq9rYy) (~228 Mo, portable)

Nouveautés de la 1.16 — **les documents des élèves entrent dans Calulis** :

- **Rangez les papiers d'un élève dans l'application** : PDF, scan, photo, courrier, document
  Word ou texte, rattaché à un élève et à un type (notification MDPH, PPS, GEVA-Sco, compte rendu
  d'ESS, PAI, document médical, bilan d'un professionnel, bulletin…). Le fichier est **copié dans
  votre dossier Calulis** : même si l'original est déplacé, renommé ou supprimé, il reste
  consultable. Rien ne part sur Internet.
- **Aperçu intégré** (PDF, image, texte), y compris sans connexion. **Filtres** par élève, par
  type, avec ou sans fichier, et **recherche** par mot — le nom de l'élève comme celui du fichier
  d'origine. Le **poids** des fichiers est affiché, les colonnes se trient.
- **Un onglet Documents dans la fiche de l'élève**, et un **compteur cliquable** dans la liste.
- **« Emporter le dossier (ZIP) »** : tous les documents d'un élève dans un seul fichier, avec un
  index lisible qui dit, pour chaque pièce, son type et sa date — pour le transmettre.
- **Les types de documents vous appartiennent** : ajoutez, renommez, désactivez, supprimez.
  Supprimer un type encore utilisé est refusé, avec proposition de réaffecter ses documents.
- **Droit à l'effacement** : supprimer un élève propose d'abord d'emporter son dossier, puis
  efface ses documents et ses fichiers. La page « Mentions RGPD » a été revue de fond en comble.
- **Nouveau lanceur (1.0.15)** : quand Calulis refuse de démarrer, il propose une **réparation
  guidée** qui met les données à l'abri d'abord, répare, et écrit un compte rendu.

Nouveautés de la 1.15.1 — une version de **robustesse et de sécurité**, qui se propage
toute seule par la mise à jour automatique :

- **Une seule base, et c'est la vôtre** : Calulis ne propose plus de choisir entre plusieurs bases.
  Il ouvre celle que vous utilisez, et toutes les opérations portent sur elle.
- **Vos données sont sauvegardées avant tout remplacement** : importer un fichier `.sql` ou
  recharger une sauvegarde commence par une sauvegarde automatique, dont le dossier est affiché ;
  si elle échoue, **rien n'est remplacé**. La question nomme ce qui sera remplacé, et la réponse
  par défaut est « Non ».
- **Si vous aviez plusieurs bases** (anciens imports), Calulis propose de les exporter en `.sql`.
  Il n'en supprime ni n'en renomme aucune.
- **Sécurité** : la base MySQL embarquée n'a plus de compte sans mot de passe. Chaque installation
  reçoit des mots de passe tirés au hasard, conservés dans votre dossier Calulis
  (`runtime/mysql-credentials.json`) ; les installations existantes sont sécurisées au premier
  démarrage. Les fichiers de données et les outils internes ne sont plus accessibles depuis le
  navigateur, et Calulis ne répond plus qu'à votre ordinateur.

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

> Le ZIP complet embarque **le lanceur 1.0.14** : plus rien à télécharger au premier démarrage. Le
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

C'est ce qui est arrivé deux fois, et c'est pourquoi la 1.15.1 publie **six** routes — toutes les
versions encore installées reçoivent la correction de sécurité :

| Version installée | Route vers la 1.15.1 |
|---|---|
| `1.15` (distribuée le 04/10) | `patch-1.15-1.15.1.zip` |
| `1.14` (distribuée du 01/10 au 04/10) | `patch-1.14-1.15.1.zip` |
| `1.13` (distribuée du 29/09 au 01/10) | `patch-1.13-1.15.1.zip` |
| `1.12.1` (distribuée du 28/09 au 29/09) | `patch-1.12.1-1.15.1.zip` |
| `1.12` (distribuée du 22 au 28/09) | `patch-1.12-1.15.1.zip` |
| `1.11` (distribuée du 07 au 22/09) | `patch-1.11-1.15.1.zip` |

Les routes plus anciennes (`1.0.x`, `1.10`) ne sont plus applicables : leurs postes doivent
réinstaller le ZIP complet (les données se restaurent par Sauvegarde/Restauration).

## 📁 Structure du dépôt

- `manifest.json` — versions disponibles, patchs, lien de téléchargement complet
- `patches/` — archives des patchs incrémentaux
- `launcher/` — archives du lanceur (`Calulis.exe`, remplacé automatiquement)

## 📦 Repo principal

Le code source et le développement sont sur [Kalimoucho08/calulis](https://github.com/Kalimoucho08/calulis).
