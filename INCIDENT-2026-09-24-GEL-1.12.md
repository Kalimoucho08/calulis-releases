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
