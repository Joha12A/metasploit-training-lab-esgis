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
3. Synthèse et documentation détaillée dans les fiches unitaires du répertoire `docs/vulnerabilites/`.

## 4. Captures d'écran
*Emplacement réservé aux captures d'écran :*
- Recherches Searchsploit : `screenshots/04-vulnerabilites/01-searchsploit.png` *(En attente)*
- Fiches de vulnérabilités CVE : `screenshots/04-vulnerabilites/02-cve-details.png` *(En attente)*

## 5. Résultat observé
> [!NOTE]
> Le tableau ci-dessous et les fiches unitaires associées seront renseignés au fur et à mesure des tests réels.

| N° | Service | Port | CVE | CVSS | Statut | Fiche détaillée |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **01** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-01.md](vulnerabilites/vuln-01.md) |
| **02** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-02.md](vulnerabilites/vuln-02.md) |
| **03** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-03.md](vulnerabilites/vuln-03.md) |
| **04** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-04.md](vulnerabilites/vuln-04.md) |
| **05** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-05.md](vulnerabilites/vuln-05.md) |
| **06** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-06.md](vulnerabilites/vuln-06.md) |
| **07** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-07.md](vulnerabilites/vuln-07.md) |
| **08** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-08.md](vulnerabilites/vuln-08.md) |
| **09** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-09.md](vulnerabilites/vuln-09.md) |
| **10** | À identifier | — | À identifier | — | ⏳ En attente | [vuln-10.md](vulnerabilites/vuln-10.md) |

## 6. Analyse technique
*(Section en attente d'évaluation de l'impact des vulnérabilités identifiées)*

## 7. Recommandations éventuelles
- Maintenir une veille de vulnérabilités active sur les composants logiciels déployés.
- Prioriser les correctifs en fonction du score CVSS et de l'exploitabilité réseau.
