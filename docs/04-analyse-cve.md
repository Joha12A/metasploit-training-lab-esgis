# 04 - Analyse des Vulnérabilités et Référencement CVE

## 1. Objectif
Associer chaque service détecté lors de la phase de reconnaissance à des vulnérabilités connues (CVE) documentées dans les bases de référence (NVD, Exploit-DB, SecurityFocus) afin de qualifier leur niveau de criticité (score CVSS).

## 2. Prérequis
- Rapport de reconnaissance et versions exactes des services (`reports/nmap-services.txt`).
- Précisions architecturales officielles fournies par l'encadrement pédagogique OURITEK / ESGIS.
- Outils de recherche : `searchsploit`, bases CVE officielles.

## 3. Procédure
1. Recherche des références de vulnérabilités par service et version exacte :
   ```bash
   searchsploit "<Nom_Service> <Version>"
   ```
2. Consultation des fiches de sécurité NIST NVD pour extraire le score CVSS v3 et les vecteurs d'attaque associés.
3. Synthèse et documentation unitaire dans les fiches du dossier `docs/vulnerabilites/`.

## 4. Captures d'écran
*Emplacements réservés aux captures d'écran :*
- Recherches Searchsploit : `screenshots/04-vulnerabilites/01-searchsploit.png`
- Fiches de vulnérabilités CVE : `screenshots/04-vulnerabilites/02-cve-details.png`

## 5. Résultat observé
Synthèse des dix services cibles du laboratoire d'entraînement sur `10.1.0.1` :

| N° | Service identifié | Port | Spécificité / Endpoint | Référence CVE | CVSS | Statut | Fiche détaillée |
| :---: | :--- | :---: | :--- | :--- | :---: | :---: | :--- |
| **01** | FTP (vsftpd) | `21` | `vsftpd 2.3.4` | CVE-2011-2523 | 9.8 | ✅ Validé | [vuln-01.md](vulnerabilites/vuln-01.md) |
| **02** | FTP (ProFTPD) | `2121` | `ProFTPD 1.3.5a (mod_copy)` | CVE-2015-3306 | 9.8 | ⏳ En cours | [vuln-02.md](vulnerabilites/vuln-02.md) |
| **03** | IRC (UnrealIRCd) | `6667` | `UnrealIRCd 3.2.8.1` | CVE-2010-2075 | 9.8 | ⏳ En attente | [vuln-03.md](vulnerabilites/vuln-03.md) |
| **04** | AJP13 (Tomcat) | `8009` | `Apache Jserv Protocol v1.3` | CVE-2020-1938 | 9.8 | ⏳ En attente | [vuln-04.md](vulnerabilites/vuln-04.md) |
| **05** | Apache Struts 2 | `8081` | `/struts2/index.action` | CVE-2017-5638 | 9.8 | ⏳ En attente | [vuln-05.md](vulnerabilites/vuln-05.md) |
| **06** | REST API | `9200` | `Elasticsearch 1.1.1` | CVE-2014-3120 | 7.5 | ⏳ En attente | [vuln-06.md](vulnerabilites/vuln-06.md) |
| **07** | Apache CGI (Shellshock) | `8888` | `/cgi-bin/test.sh` | CVE-2014-6271 | 9.8 | ⏳ En attente | [vuln-07.md](vulnerabilites/vuln-07.md) |
| **08** | HTTP / PHP | `8080` | `Apache 2.4.41 / PHP 7.4.3` | CVE-2024-4577 | 9.8 | ⏳ En attente | [vuln-08.md](vulnerabilites/vuln-08.md) |
| **09** | HTTPS / WebUI | `443` | `nginx (Open WebUI)` | CVE-2024-37032 | 8.8 | ⏳ En attente | [vuln-09.md](vulnerabilites/vuln-09.md) |
| **10** | SSH | `22` | `OpenSSH 8.2p1` | CVE-2020-15778 | 7.8 | ⏳ En attente | [vuln-10.md](vulnerabilites/vuln-10.md) |

## 6. Analyse technique
Les précisions fournies par l'équipe pédagogique confirment la présence de failles majeures :
- **Port 8081** : Apache Struts 2 (S2-045, CVE-2017-5638), vulnérabilité d'analyse des en-têtes HTTP `Content-Type`.
- **Port 8888** : Vulnérabilité Bash Shellshock (CVE-2014-6271) via le script CGI `/cgi-bin/test.sh`.

## 7. Recommandations éventuelles
- Prioriser les correctifs en commençant par les services présentant un score CVSS critique (≥ 9.0).
- Surveiller la stabilité des services qui redémarrent automatiquement toutes les 30 minutes.
