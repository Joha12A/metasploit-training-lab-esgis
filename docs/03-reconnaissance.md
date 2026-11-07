# 03 - Reconnaissance et Cartographie Réseau

## 1. Objectif
Identifier les ports ouverts, les services actifs et leurs versions respectives sur la cible autorisée **ESGIS VulnBox** (`10.1.0.1`) afin de repérer les dix services vulnérables prévus dans le laboratoire.

## 2. Prérequis
- Tunnel WireGuard actif et connectivité établie vers `10.1.0.1`.
- Outils de reconnaissance disponibles sur Kali Linux (`nmap`, etc.).
- Respect strict du périmètre autorisé du laboratoire.

## 3. Procédure
1. Découverte d'hôtes et scan préliminaire des ports usuels :
   ```bash
   nmap -sS -Pn 10.1.0.1
   ```
2. Scan approfondi de détection de versions et de scripts par défaut sur les ports identifiés :
   ```bash
   nmap -sV -sC -Pn -p- 10.1.0.1 -oN reports/nmap-full-scan.txt
   ```

## 4. Captures d'écran
*Emplacement réservé aux captures d'écran de reconnaissance :*
- Résultat du scan Nmap initial : `screenshots/03-reconnaissance/01-nmap-initial.png` *(En attente)*
- Détection des services et versions : `screenshots/03-reconnaissance/02-nmap-services.png` *(En attente)*

## 5. Résultat observé
*(Section en attente de réalisation du scan réseau)*

## 6. Analyse technique
*(Section en attente d'inventaire des 10 services vulnérables identifiés)*

## 7. Recommandations éventuelles
- Restreindre l'exposition des ports d'administration sur des réseaux non fiables.
- Désactiver les services obsolètes ou inutilisés.
