# Metasploit Training Lab – ESGIS VulnBox

Projet académique et technique de cybersécurité offensive et défensive réalisé dans le cadre des travaux pratiques à **ESGIS**, en partenariat avec **OURITEK Security Labs**.

---

## 1. Contexte du Laboratoire

Ce laboratoire d'entraînement a pour objectif l'étude approfondie de vulnérabilités logicielles et systèmes courantes dans un environnement isolé et contrôlé.

- **Organisme** : OURITEK Security Labs
- **Cadre** : Travaux Pratiques de Cybersécurité – ESGIS
- **Auteur** : Johanes Amoussouga ([@Joha12A](https://github.com/Joha12A))

---

## 2. Objectifs Pédagogiques

- Maîtriser la démarche méthodologique d'un audit de sécurité offensif autorisé.
- Cartographier et analyser la surface d'attaque d'une cible réseau dédiée.
- Identifier et référencer les vulnérabilités applicatives (CVE) et évaluer leur criticité (CVSS).
- Manipuler avec rigueur le framework **Metasploit** (modules auxiliaires, scanners, exploits).
- Documenter fidèlement les démarches, preuves de concept et observations techniques.
- Formuler des recommandations de remédiation et durcissement adaptées aux standards de l'industrie.

---

## 3. Périmètre Autorisé et Règles d'Engagement

> [!IMPORTANT]
> **Règles d'engagement éthiques et légales :**
> L'ensemble des activités conduites dans ce dépôt s'inscrit strictement dans le cadre des travaux pratiques autorisés par l'ESGIS et encadrés par OURITEK Security Labs.
> - **Cible autorisée unique** : `10.1.0.1` (**ESGIS VulnBox**)
> - **Réseau de transit** : Tunnel sécurisé WireGuard dédié
> - Tout scan ou test hors de ce périmètre est formellement interdit.

---

## 4. Environnement Technique & Outils

| Composant | Rôle | Spécifications |
| :--- | :--- | :--- |
| **Machine Attaquante** | Station d'audit | Kali Linux (Rolling) |
| **Machine Cible** | Environnement d'entraînement | ESGIS VulnBox (`10.1.0.1`), 10 services vulnérables |
| **Connectivité** | Réseau d'accès sécurisé | WireGuard VPN |
| **Framework d'Exploitation** | Tests d'intrusion | Metasploit Framework (`msfconsole`) |
| **Outils de Reconnaissance** | Scanner réseau & vulnérabilités | Nmap, Searchsploit |
| **Gestion de Version** | Traçabilité et documentation | Git, GitHub |

---

## 5. Structure du Dépôt

```text
Metasploit-Lab/
├── README.md                   # Présentation générale du projet
├── LICENSE                     # Licence du projet (MIT)
├── .gitignore                  # Exclusion des fichiers sensibles et temporaires
├── docs/                       # Documentation méthodologique par phase
│   ├── 01-environnement.md     # Spécifications de l'environnement de travail
│   ├── 02-wireguard.md         # Configuration et connexion VPN
│   ├── 03-reconnaissance.md    # Reconnaissance réseau et scans de ports
│   ├── 04-analyse-cve.md       # Identification et qualification des CVE
│   ├── 05-metasploit.md        # Exploitation pédagogique et modules Metasploit
│   ├── 06-resultats.md         # Tableau de synthèse des PoC et résultats
│   └── 07-recommandations.md   # Mesures de durcissement et remédiation
├── screenshots/                # Captures d'écran et preuves visuelles
│   ├── 01-kali/                # Environnement Kali Linux
│   ├── 02-wireguard/           # Connexion VPN active
│   ├── 03-reconnaissance/      # Résultats Nmap
│   ├── 04-vulnerabilites/      # Recherches CVE et msfconsole
│   └── 05-resultats/           # Preuves de concept (PoC)
├── scripts/                    # Scripts d'automatisation ou d'aide à l'audit
└── reports/                    # Rapports formels d'évaluation
    └── README.md
```

---

## 6. Synthèse d'Avancement des Travaux

Les dix services vulnérables seront analysés et documentés au fur et à mesure de l'avancement du laboratoire.

| Phase | Description | Statut |
| :--- | :--- | :--- |
| **Phase 1** | Configuration de l'environnement & Dépôt Git | ✅ **Terminé** |
| **Phase 2** | Connexion VPN WireGuard & Test d'accès | ⏳ *En attente* |
| **Phase 3** | Reconnaissance réseau & Identification des 10 services | ⏳ *En attente* |
| **Phase 4** | Analyse CVE & Qualification des vulnérabilités | ⏳ *En attente* |
| **Phase 5** | Tests pédagogiques Metasploit | ⏳ *En attente* |
| **Phase 6** | Collecte des preuves et formalisation des résultats | ⏳ *En attente* |
| **Phase 7** | Rédaction du plan de remédiation & Durcissement | ⏳ *En attente* |

---

## 7. Recommandations Préliminaires de Sécurité

Dans l'attente des analyses approfondies sur les dix services de la VulnBox :
- **Cloisonnement strict** : Isoler les environnements vulnérables sur des segments réseau non routés vers la production.
- **Protection des secrets** : Ne jamais stocker de fichiers de configuration VPN (`*.conf`), clés privées ou jetons d'accès dans un dépôt public.
- **Sensibilisation continue** : Appliquer les principes de sécurité dès la conception (*Security by Design*).
