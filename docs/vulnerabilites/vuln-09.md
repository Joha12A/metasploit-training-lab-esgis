# Fiche Vulnérabilité N°09 — Ollama (CVE-2024-37032)

## 1. Contexte et Identification
- **Service cible** : Ollama (serveur d'IA) derrière Open WebUI
- **Port d'écoute** : `443/tcp` (via nginx/Open WebUI)
- **Version détectée** : `Ollama 0.11.4`
- **Référence CVE** : `CVE-2024-37032`
- **Score CVSS v3** : `8.8 (Élevé)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description** : Ollama est un serveur d'exécution de modèles d'IA, souvent utilisé avec Open WebUI.
- **Vecteur d'exposition** : Port 443 (HTTPS) via nginx/Open WebUI.
- **Module Metasploit** : `exploit/linux/http/ollama_rce_cve_2024_37032`

## 3. Démarche survolée
- Le module Metasploit a été testé mais a échoué (`Ollama 0.11.4 (patched)`).
- Analyse : la version 0.11.4 intègre le correctif de la CVE-2024-37032. La vulnérabilité n'est pas exploitable.

## 4. Mesures Correctives
- **Maintien à jour** : Version 0.11.4 déjà corrigée.
- **Filtrage réseau** : Restreindre l'accès au port 443 aux réseaux d'administration.

---
**Statut** : ⏳ **En attente** — Version corrigée (Ollama 0.11.4) ; à réévaluer.