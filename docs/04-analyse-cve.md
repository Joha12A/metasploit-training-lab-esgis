# 04 - Analyse des Vulnérabilités et Référencement CVE

## 1. Objectif
Associer chaque service détecté lors de la phase de reconnaissance à des vulnérabilités connues (CVE) documentées dans les bases de référence (NVD, Exploit-DB, SecurityFocus) afin de qualifier leur niveau de criticité (score CVSS).

## 2. Prérequis
- Rapport de reconnaissance et versions exactes des services (`reports/nmap-services.txt`).
- Outils de recherche de vulnérabilités : `searchsploit`, bases CVE officielles.

## 3. Procédure
1. Recherche des références de vulnérabilités par service et version exacte :
   ```bash
   searchsploit "<Nom_Service> <Version>"
   ```
2. Consultation des fiches de sécurité NIST NVD pour extraire le score CVSS v3 et les vecteurs d'attaque associés.
3. Synthèse et documentation unitaire dans les fiches du dossier `docs/vulnerabilites/`.

## 4. Captures d'écran
*Emplacements réservés aux captures d'écran :*
- Recherches Searchsploit : `screenshots/04-vulnerabilites/01-searchsploit.png` *(En attente)*
- Fiches de vulnérabilités CVE : `screenshots/04-vulnerabilites/02-cve-details.png` *(En attente)*

## 5. Résultat observé
Synthèse des dix services cibles identifiés lors de la phase de reconnaissance réseau sur `10.1.0.1` :

| N° | Service identifié | Port | Version logicielle | Référence CVE | CVSS | Statut | Fiche détaillée |
| :---: | :--- | :---: | :--- | :--- | :---: | :---: | :--- |
| **01** | FTP | `21` | `vsftpd 2.3.4` | CVE-2011-2523 | 9.8 | ⏳ En attente | [vuln-01.md](vulnerabilites/vuln-01.md) |
| **02** | FTP alternatif | `2121` | `ProFTPD 1.3.5a` | CVE-2015-3306 | 9.8 | ⏳ En attente | [vuln-02.md](vulnerabilites/vuln-02.md) |
| **03** | IRC | `6667` | `UnrealIRCd 3.2.8.1` | CVE-2010-2075 | 9.8 | ⏳ En attente | [vuln-03.md](vulnerabilites/vuln-03.md) |
| **04** | AJP13 | `8009` | `Apache Jserv Protocol v1.3` | CVE-2020-1938 | 9.8 | ⏳ En attente | [vuln-04.md](vulnerabilites/vuln-04.md) |
| **05** | HTTP / Tomcat | `8081` | `Apache Tomcat 7.0.109` | CVE-2017-12615 | 8.1 | ⏳ En attente | [vuln-05.md](vulnerabilites/vuln-05.md) |
| **06** | REST API | `9200` | `Elasticsearch 1.1.1` | CVE-2014-3120 | 7.5 | ⏳ En attente | [vuln-06.md](vulnerabilites/vuln-06.md) |
| **07** | HTTP / Apache | `8888` | `Apache httpd 2.4.41 (cgi-bin)` | CVE-2021-41773 | 7.5 | ⏳ En attente | [vuln-07.md](vulnerabilites/vuln-07.md) |
| **08** | HTTP / PHP | `8080` | `Apache 2.4.41 / PHP 7.4.3` | CVE-2024-4577 | 9.8 | ⏳ En attente | [vuln-08.md](vulnerabilites/vuln-08.md) |
| **09** | HTTPS / WebUI | `443` | `nginx (Open WebUI)` | CVE-2024-37032 | 8.8 | ⏳ En attente | [vuln-09.md](vulnerabilites/vuln-09.md) |
| **10** | SSH | `22` | `OpenSSH 8.2p1` | CVE-2020-15778 | 7.8 | ⏳ En attente | [vuln-10.md](vulnerabilites/vuln-10.md) |

## 6. Analyse technique
Les services exposés présentent des vulnérabilités critiques documentées, couvrant un large spectre d'impacts : lecture arbitraire de fichiers sensibles, exécution de commandes non authentifiée, ou exposition de protocoles d'administration.

## 7. Recommandations éventuelles
- Prioriser les correctifs en commençant par les services présentant un score CVSS critique (≥ 9.0).
- Désactiver les protocoles non chiffrés ou obsolètes (ex. IRC, FTP non sécurisé).
