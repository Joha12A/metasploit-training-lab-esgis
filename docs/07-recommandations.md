# 07 - Recommandations Stratégiques et Plan de Remédiation

## 1. Objectif
Définir une feuille de route de remédiation technique et organisationnelle visant à corriger les vulnérabilités identifiées sur le système cible et à durcir sa posture globale de sécurité (Hardening).

## 2. Prérequis
- Analyse complète des vulnérabilités (scores CVSS, vecteurs d'attaque).
- Synthèse des impacts techniques observés dans `docs/06-resultats.md`.

## 3. Procédure
1. Classification des actions correctives par niveau de priorité (Immédiate, Court terme, Moyen terme).
2. Élaboration de mesures de durcissement défensives (segmentation réseau, gestion des correctifs, surveillance).
3. Proposition de contrôles de sécurité post-remédiation.

## 4. Captures d'écran
*Emplacement réservé aux éventuelles preuves de remédiation ou durcissement :*
- Configuration durcie : `screenshots/05-resultats/hardening-config.png` *(En attente)*

## 5. Résultat observé
*(Section en attente : sera alimentée suite aux conclusions des tests d'audit)*

## 6. Analyse technique
Les axes directeurs de remédiation recommandés s'articulent autour des piliers suivants :
- **Mise à jour et Patch Management** : Application systématique des correctifs éditeurs sur les logiciels tiers et le système d'exploitation.
- **Réduction de la surface d'attaque** : Fermeture des services réseau non indispensables aux besoins métier.
- **Principe de moindre privilège** : Exécution des démons réseau sous des comptes de service restreints et sans droit `root`.
- **Segmentation réseau & Filtrage** : Mise en place de règles de pare-feu étanches et d'un bastion d'administration.
- **Journalisation & Supervision** : Centralisation des journaux (SIEM) et détection des comportements anormaux (EDR / IDS).

## 7. Recommandations éventuelles
- Mettre en place un cycle d'audit et de scan de vulnérabilités récurrent.
- Sensibiliser les équipes d'administration système et réseau aux bonnes pratiques de durcissement (guides ANSSI / CIS Benchmarks).
