# 04 - Analyse des Vulnérabilités et Référencement CVE

## 1. Objectif
Associer chaque service détecté lors de la phase de reconnaissance à des vulnérabilités connues (CVE) documentées dans les bases de référence (NVD, Exploit-DB, SecurityFocus) afin de qualifier leur niveau de criticité (score CVSS).

## 2. Prérequis
- Rapport de reconnaissance et versions exactes des services (`reports/nmap-full-scan.txt`).
- Outils de recherche de vulnérabilités : `searchsploit`, bases CVE officielles.

## 3. Procédure
1. Recherche des exploits et vulnérabilités par service et version :
   ```bash
   searchsploit "<Nom_Service> <Version>"
   ```
2. Consultation des fiches CVE sur le NIST NVD (National Vulnerability Database) pour extraire le score CVSS et le vecteur d'attaque.
3. Synthèse des dix vulnérabilités cibles sous forme de tableau comparatif.

## 4. Captures d'écran
*Emplacement réservé aux captures d'écran :*
- Recherches Searchsploit : `screenshots/04-vulnerabilites/01-searchsploit.png` *(En attente)*
- Fiches de vulnérabilités CVE : `screenshots/04-vulnerabilites/02-cve-details.png` *(En attente)*

## 5. Résultat observé
*(Section en attente : le tableau ci-dessous sera complété dès la phase de reconnaissance validée)*

| Service identifié | Port | Version | Référence CVE | Score CVSS | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Service 1 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 2 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 3 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 4 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 5 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 6 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 7 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 8 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 9 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |
| Service 10 | *À renseigner* | *À renseigner* | *En attente* | *En attente* | À analyser |

## 6. Analyse technique
*(Section en attente d'évaluation de l'impact des vulnérabilités identifiées)*

## 7. Recommandations éventuelles
- Maintenir une veille de vulnérabilités active sur les composants logiciels déployés.
- Prioriser les correctifs en fonction du score CVSS et de l'exploitabilité réseau.
