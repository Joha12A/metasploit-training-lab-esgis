# Fiche Vulnérabilité N°07 — Apache CGI Shellshock (CVE-2014-6271)

## 1. Contexte et Identification
- **Service cible** : Serveur web Apache avec script CGI
- **Port d'écoute** : `8888/tcp`
- **Point d'accès (Endpoint)** : `/cgi-bin/test.sh`
- **Référence CVE** : `CVE-2014-6271` (Vulnérabilité *Shellshock*)
- **Score CVSS v3** : `9.8 (Critique)` — Vecteur : `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

---

## 2. Observations Techniques
- **Description du composant** : Serveur Apache exécutant un script Bash sous forme de script CGI (`test.sh`).
- **Vecteur d'exposition** : Mauvaise interprétation des variables d'environnement par l'interpréteur GNU Bash lors de la déclaration de fonctions trailing (`() { :;};`).
- **Module Metasploit associé** : `exploit/multi/http/apache_mod_cgi_bash_env_exec`

---

## 3. Preuves Réelles
*Emplacements réservés aux captures d'écran et sorties console :*
- Capture de configuration : `screenshots/04-vulnerabilites/vuln-07-exec.png` *(En attente)*
- Preuve PoC : `screenshots/05-resultats/vuln-07-poc.png` *(En attente)*

---

## 4. Mesures Correctives et Remédiation
- **Correctif d'environnement** : Mettre à jour le paquet `bash` vers une version corrigée neutralisant l'évaluation automatique des définitions de fonctions dans les variables d'environnement.
- **Réduction de surface** : Remplacer l'usage de scripts CGI Bash par des architectures modernes plus sécurisées (FastCGI, API conteneurisées).
- **Principe de moindre privilège** : Restreindre les droits du processus d'exécution Apache (`www-data`).

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
