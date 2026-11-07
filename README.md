# Metasploit Training Lab – ESGIS VulnBox

Projet académique et technique de cybersécurité offensive et défensive réalisé dans le cadre des travaux pratiques à **ESGIS**, en partenariat avec **OURITEK Security Labs**.

---

## 1. Contexte du Laboratoire

Ce laboratoire d'entraînement a pour objectif l'étude approfondie de vulnérabilités logicielles et systèmes courantes dans un environnement isolé et contrôlé.

- **Organisme** : OURITEK Security Labs
- **Cadre** : Travaux Pratiques de Cybersécurité – ESGIS
- **Auteur** : Johanes Amoussouga ([@Joha12A](https://github.com/Joha12A))
- **Licence** : Projet distribué sous [Licence MIT](LICENSE) à visée académique et éducative.

---

## 2. Objectifs Pédagogiques

- Maîtriser la démarche méthodologique d'un audit de sécurité offensif autorisé.
- Cartographier et analyser la surface d'attaque d'une cible réseau dédiée.
- Identifier et référencer les vulnérabilités applicatives (CVE) et évaluer leur criticité (CVSS).
- Manipuler avec rigueur le framework **Metasploit** (modules auxiliaires, scanners, exploits).
- Documenter fidèlement les démarches, preuves de concept et observations techniques.
- Formuler des recommandations de remédiation et de durcissement conformes aux standards de l'industrie.

---

## 3. Périmètre Autorisé et Règles d'Engagement

> [!IMPORTANT]
> **Règles d'engagement éthiques et légales :**
> L'ensemble des activités conduites dans ce dépôt s'inscrit strictement dans le cadre des travaux pratiques autorisés par l'ESGIS et encadrés par OURITEK Security Labs.
> - **Cible autorisée unique** : `10.1.0.1` (**ESGIS VulnBox**)
> - **Réseau de transit** : Tunnel sécurisé WireGuard dédié
> - Tout scan, test ou tentative d'accès hors de ce périmètre est formellement interdit.
> - Les configurations WireGuard, clés privées et secrets ne sont jamais publiés ni suivis sur ce dépôt.

---

## 4. Environnement Technique & Outils

| Composant | Rôle | Spécifications |
| :--- | :--- | :--- |
| **Machine Attaquante** | Station d'audit | Kali Linux (Rolling) |
| **Machine Cible** | Environnement d'entraînement | ESGIS VulnBox (`10.1.0.1`), 10 services vulnérables |
| **Connectivité** | Réseau d'accès sécurisé | WireGuard VPN |
| **Framework d'Exploitation** | Tests d'intrusion pédagogiques | Metasploit Framework (`msfconsole`) |
| **Outils de Reconnaissance** | Scanner réseau & vulnérabilités | Nmap, Searchsploit |
| **Gestion de Version** | Traçabilité et documentation | Git, GitHub |

---

## 5. Méthodologie d'Analyse des Vulnérabilités

Pour chacun des dix services vulnérables hébergés sur la cible, la démarche méthodologique respecte rigoureusement le cycle suivant :

1. **Identification du service** : Détection du port ouvert, de la bannière et de la version logicielle exacte via Nmap.
2. **Recherche de la CVE associée** : Corrélation de la version logicielle avec les bases officielles de vulnérabilités (NVD, VulnDB, Exploit-DB).
3. **Étude de la criticité CVSS** : Analyse du score CVSS v3 (vecteur d'attaque, complexité, privilèges requis, impact CIA).
4. **Analyse du module Metasploit correspondant** : Recherche et inspection du code source du module (auxiliaire ou exploit) sous `msfconsole`.
5. **Test autorisé dans le laboratoire** : Exécution contrôlée de la vérification (`check`) ou du test sur `10.1.0.1`.
6. **Collecte des preuves** : Captures d'écran horodatées et consignation des sorties consoles brutes.
7. **Analyse des résultats** : Interprétation technique du comportement applicatif et de l'impact réel.
8. **Recommandations de correction** : Proposition de correctifs éditeurs, de règles de filtrage pare-feu et de guides de durcissement.

---

## 6. Tableau de Suivi des Dix Vulnérabilités

> [!NOTE]
> Les informations ci-dessous sont issues de la cartographie réseau Nmap réalisée sur `10.1.0.1`. Les tests et vérifications effectives seront consignés progressivement.

| N° | Service | Port | CVE | CVSS | Statut | Fiche détaillée |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **01** | `vsftpd 2.3.4` (FTP) | 21 | CVE-2011-2523 | 9.8 | ✅ Validé | [Fiche 01](docs/vulnerabilites/vuln-01.md) |
| **02** | `ProFTPD 1.3.5a` (FTP alt) | 2121 | CVE-2015-3306 | 9.8 | ✅ Validé | [Fiche 02](docs/vulnerabilites/vuln-02.md) |
| **03** | `UnrealIRCd 3.2.8.1` (IRC) | 6667 | CVE-2010-2075 | 9.8 | ⏳ En attente | [Fiche 03](docs/vulnerabilites/vuln-03.md) |
| **04** | `Apache Jserv AJP13` (AJP) | 8009 | CVE-2020-1938 | 9.8 | ✅ Validé | [Fiche 04](docs/vulnerabilites/vuln-04.md) |
| **05** | `Apache Struts 2` (/struts2/) | 8081 | CVE-2017-5638 | 9.8 | ⏳ En attente | [Fiche 05](docs/vulnerabilites/vuln-05.md) |
| **06** | `Elasticsearch 1.1.1` (API) | 9200 | CVE-2014-3120 | 7.5 | ✅ Validé | [Fiche 06](docs/vulnerabilites/vuln-06.md) |
| **07** | `Apache Shellshock` (test.sh) | 8888 | CVE-2014-6271 | 9.8 | ✅ Validé | [Fiche 07](docs/vulnerabilites/vuln-07.md) |
| **08** | `PHP 7.4.3 / Apache` (HTTP) | 8080 | CVE-2024-4577 | 9.8 | ⏳ En attente | [Fiche 08](docs/vulnerabilites/vuln-08.md) |
| **09** | `Open WebUI / nginx` (HTTPS) | 443 | CVE-2024-37032 | 8.8 | ⏳ En attente | [Fiche 09](docs/vulnerabilites/vuln-09.md) |
| **10** | `OpenSSH 8.2p1` (SSH) | 22 | CVE-2020-15778 | 7.8 | ⏳ En attente | [Fiche 10](docs/vulnerabilites/vuln-10.md) |

---

## 7. Structure du Dépôt

```text
Metasploit-Lab/
├── README.md                   # Présentation générale du projet et méthodologie
├── LICENSE                     # Licence du projet (MIT)
├── .gitignore                  # Exclusion stricte des secrets et fichiers temporaires
├── docs/                       # Documentation méthodologique globale
│   ├── 01-environnement.md     # Spécifications de l'environnement de travail
│   ├── 02-wireguard.md         # Configuration et connexion VPN
│   ├── 03-reconnaissance.md    # Reconnaissance réseau et scans de ports
│   ├── 04-analyse-cve.md       # Identification et qualification des CVE
│   ├── 05-metasploit.md        # Exploitation pédagogique et modules Metasploit
│   ├── 06-resultats.md         # Tableau de synthèse des PoC et résultats
│   ├── 07-recommandations.md   # Mesures de durcissement et remédiation
│   └── vulnerabilites/         # Fiches individuelles d'analyse
│       ├── README.md           # Index des 10 fiches
│       ├── vuln-01.md          # Fiche technique Vulnérabilité 01
│       └── ...                 # Fiches techniques Vulnérabilités 02 à 10
├── screenshots/                # Captures d'écran et preuves visuelles
│   ├── 01-kali/                # Environnement Kali Linux
│   ├── 02-wireguard/           # Connexion VPN active
│   ├── 03-reconnaissance/      # Résultats Nmap
│   ├── 04-vulnerabilites/      # Recherches CVE et exécution Metasploit
│   └── 05-resultats/           # Preuves de concept (PoC) réelles
├── scripts/                    # Scripts d'automatisation ou d'aide à l'audit
└── reports/                    # Rapports formels d'évaluation
    └── README.md
```

---

## 8. Synthèse d'Avancement des Travaux

| Phase | Description | Statut |
| :--- | :--- | :--- |
| **Phase 1** | Configuration de l'environnement, structure & Dépôt Git | ✅ **Terminé** (publié sur GitHub) |
| **Phase 2** | Connexion VPN WireGuard & Validation de l'accès à 10.1.0.1 | ✅ **Terminé** (validé et documenté) |
| **Phase 3** | Reconnaissance réseau & Identification des 10 services | ✅ **Terminé** (cartographie Nmap validée) |
| **Phase 4** | Analyse CVE & Qualification des vulnérabilités | ✅ **Terminé** (10 services référencés) |
| **Phase 5** | Tests pédagogiques Metasploit | ⏳ *En cours (5/10 validés)* |
| **Phase 6** | Collecte des preuves et formalisation des résultats | ⏳ *En cours (PoC 01 02 04 06 & 07intégrés)* |
| **Phase 7** | Rédaction du plan de remédiation & Durcissement | ⏳ *En attente* |

---

## 9. Recommandations Préliminaires de Sécurité

Dans l'attente des analyses approfondies sur les dix services de la VulnBox :
- **Cloisonnement strict** : Isoler les environnements vulnérables sur des segments réseau non routés vers la production.
- **Protection absolue des secrets** : Ne jamais stocker de fichiers de configuration VPN (`*.conf`), clés privées ou jetons d'accès dans un dépôt public.
- **Sensibilisation continue** : Appliquer les principes de sécurité dès la conception (*Security by Design*).
