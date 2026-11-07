# Fiche Vulnérabilité N°08 — PHP 7.4.3 / Apache (CVE-2024-4577)

## 1. Contexte et Identification
- **Service cible** : Apache HTTP Server + PHP 7.4.3
- **Port d'écoute** : `8080/tcp`
- **Version détectée** : Apache 2.4.41 (Ubuntu) + PHP 7.4.3
- **Référence CVE** : `CVE-2024-4577`
- **Score CVSS v3** : `9.8 (Critique)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description** : Serveur web Apache avec PHP 7.4.3, détecté lors du scan Nmap.
- **Vecteur d'exposition** : Injection de paramètres CLI via `Content-Type` (spécifique à Windows).
- **Module Metasploit** : `exploit/windows/http/php_cgi_arg_injection_rce_cve_2024_4577`

## 3. Démarche survolée
- Le module Metasploit a été testé mais a échoué (`The target is not exploitable`).
- Analyse : la CVE-2024-4577 est **spécifique à Windows** (conversion Unicode). La cible étant sous Linux, elle n'est pas applicable.

## 4. Mesures Correctives
- **Mise à jour** : PHP ≥ 8.1.29, 8.2.20, 8.3.8.
- **Filtrage** : WAF bloquant les `Content-Type` suspects.
- **Surveillance** : Auditer les versions PHP exposées.

---
**Statut** : ⏳ **En attente** — CVE Windows-only, cible Linux ; à réévaluer avec un autre vecteur.