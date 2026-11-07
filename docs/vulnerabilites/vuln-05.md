# Fiche Vulnérabilité N°05 — Apache Struts 2 (CVE-2017-5638)

## 1. Contexte et Identification
- **Service cible** : Apache Struts 2 (Showcase)
- **Port d'écoute** : `8081/tcp`
- **Point d'accès** : `/struts2/index.action`
- **Version détectée** : Struts2 Showcase sur Tomcat 7.0.109
- **Référence CVE** : `CVE-2017-5638`
- **Score CVSS v3** : `9.8 (Critique)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description** : Application Struts2 Showcase exposée sur le port 8081.
- **Vecteur d'exposition** : En-tête HTTP `Content-Type` malveillant contenant une expression OGNL.
- **Module Metasploit** : `exploit/multi/http/struts2_code_exec_showcase`

## 3. Démarche survolée
- Le module Metasploit a confirmé l'exécution de code (`[+] Command executed`), mais le reverse shell n'a pas abouti.
- Un test manuel avec `curl` a renvoyé une erreur OGNL (`No result defined for action...`), confirmant l'interprétation de l'expression, sans retour de commande.

## 4. Mesures Correctives
- **Mise à jour** : Struts 2 ≥ 2.3.32 ou ≥ 2.5.10.1.
- **WAF** : Bloquer les `Content-Type` contenant `%{...}`.
- **Suppression** : Retirer les applications de démonstration en production.

---
**Statut** : ⏳ **En cours** — RCE partiellement confirmée, session non obtenue.