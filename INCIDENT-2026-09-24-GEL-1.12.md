# Gel de diffusion — Calulis 1.12

**Date :** 24 septembre 2026  
**Statut :** gel d’urgence réversible  
**Version automatiquement proposée :** 1.11

## Décision

La diffusion automatique de Calulis 1.12 est suspendue à titre conservatoire à la suite d’un signalement d’échec de démarrage et d’une boucle apparente de relance du lanceur après mise à jour.

Le manifeste public ne propose plus la transition `1.11 → 1.12` et annonce `1.11` comme dernière version. Le mécanisme ne doit effectuer aucun downgrade automatique : les installations déjà en 1.12 ne sont pas modifiées par ce gel.

## Périmètre exact

- Modifié : `manifest.json`, uniquement pour retirer l’entrée de patch `1.11 → 1.12` et fixer `latestVersion` à `1.11`.
- Ajouté : ce document de suivi.
- Non modifié : tous les ZIP publiés, y compris `patches/patch-1.11-1.12.zip` et `launcher/calulis-launcher-1.0.8.zip`.
- Non modifié : les données, bases et installations locales des utilisateurs.
- Non modifié : la section `full` du manifeste, qui référence encore le paquet complet 1.12. Elle est conservée intacte faute de paquet complet 1.11 validé et ne doit pas être utilisée pour installer ou restaurer la version 1.11.

## Effet attendu

- Un poste en 1.11 ne doit plus se voir proposer la 1.12.
- Les postes antérieurs peuvent encore suivre les patchs historiques jusqu’à 1.11.
- Un poste déjà en 1.12 reste en 1.12 : aucun retour arrière automatique n’est demandé.
- Aucun fichier de diffusion n’est supprimé ; la reprise ou l’annulation est possible par restauration du manifeste précédent.

## Conditions de reprise

La diffusion de la 1.12 ne pourra être rétablie qu’après :

1. reproduction et qualification du signalement ;
2. test sur une machine Windows représentative, incluant une mise à jour depuis 1.11 ;
3. vérification que le lanceur quitte puis redémarre une seule instance ;
4. sauvegarde et intégrité des données contrôlées ;
5. commit documenté rétablissant l’entrée `1.11 → 1.12` et `latestVersion: "1.12"`.

## Retour arrière du gel

Pour annuler ce gel, restaurer la version précédente de `manifest.json` depuis le commit immédiatement antérieur, puis valider sur un poste de test. Les archives n’ayant pas été supprimées, aucune republication de ZIP n’est nécessaire.

---

## MISE A JOUR 26/09/2026 (soir) — coherence retablie et gel rendu etanche

Audit realise par Harness/DeepSeek. Trois actions, toutes documentees et reversibles.

### 1. Coherence du manifeste (commit `39fc6e6`)

Le gel laissait `latestVersion: "1.11"` avec `full.version: "1.12"` : un utilisateur qui
telechargeait la version complete obtenait la 1.12, celle qui a casse le poste. La section `full`
pointe desormais sur le paquet complet **1.11** (`calulis-v1.11-portable.zip`,
sha256 `617e5c2ba57d49338eaa8026b5f712a1668565786532b0ed9b3691b108941cbe`, valeur du commit de
publication `a36eaac` — aucune valeur inventee).

Changement **semantique unique** verifie par diff JSON : `full` seulement. `latestVersion`,
`patches` (12), `launcher` et `manifestMirror` sont inchanges. Aucun ZIP supprime.

Le fichier, que l'action d'urgence avait reecrit sur une seule ligne, est de nouveau indente.

### 2. Miroir pCloud `manifest.json` mis a jour

Le miroir pCloud (`XZC7j77ZNc031KDTpbj02hQIUO9SNYkYXHuy`) servait encore le manifeste 1.12. Il a
ete remplace par le manifeste gele et coherent (verifie en telechargeant via le lien public).

### 3. Gel rendu etanche : patch `1.11 -> 1.12` neutralise dans le miroir pCloud

Le lanceur memorise le manifeste dans `runtime/update-cache.json`. Si GitHub est injoignable
(frequent en etablissement), il reutilise ce manifeste memorise — qui pouvait encore contenir
l'entree `1.11 -> 1.12` — et telechargeait alors le patch depuis son **miroir pCloud**, toujours en
ligne. Le gel n'etait donc pas etanche.

Le fichier du miroir a ete remplace par un texte neutre (876,1 Ko -> 647 octets) :

- le SHA-256 servi ne correspond plus a celui annonce dans le manifeste, donc le lanceur
  **refuse** le telechargement (`Hash invalide`) : l'echec est sur, aucune installation partielle ;
- **aucun ZIP n'a ete supprime** : `patches/patch-1.11-1.12.zip` reste intact dans ce depot
  (sha256 `a92c47a9a86a334a4a951d4e10000eeded26cd818be6be1035b32214fbf4a114`) ;
- **pour retablir** : re-televerser `patches/patch-1.11-1.12.zip` de ce depot dans le dossier
  pCloud `calluis-partage/calulis-update/patches/` (meme nom de fichier).

### Ce qui reste a faire avant toute reprise de diffusion

- Reproduire la panne sur un banc Windows (protocole `tests/protocole-test-secours-calulis.md`,
  phase 2) et valider les correctifs du lanceur.
- Ne pas restaurer `full` en 1.12 ni le miroir pCloud du patch avant que la 1.12 (ou une version
  corrective) soit validee sur un Windows propre.
- Validateur a utiliser avant chaque publication :
  `scripts/valider-manifest.sh` (depot `calulis`). Il refuse l'incoherence
  `latestVersion` / `full.version` qui est a l'origine de cette mise a jour.
