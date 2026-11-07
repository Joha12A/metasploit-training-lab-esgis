# Fiche Vulnérabilité N°05 — Apache Struts 2 (S2-045)

## 1. Contexte et Identification
- **Service cible** : Serveur web d'applications Apache Struts 2
- **Port d'écoute** : `8081/tcp`
- **Point d'entrée (Endpoint)** : `/struts2/index.action`
- **Référence CVE** : `CVE-2017-5638` (Bulletin de sécurité Apache : `S2-045`)
- **Score CVSS v3** : `9.8 (Critique)` — Vecteur : `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

---

## 2. Observations Techniques
- **Description du composant** : Application web développée avec le framework Java Apache Struts 2.
- **Vecteur d'exposition** : Analyseur d'en-tête Jakarta Multipart parser défaillant lors de la réception d'en-têtes HTTP `Content-Type` invalides contenant du code OGNL (Object-Graph Navigation Language).
- **Module Metasploit associé** : `exploit/multi/http/struts2_content_type_ognl`

---

## 3. Preuves Réelles
*Emplacements réservés aux captures d'écran et sorties console :*
- Capture de configuration : `screenshots/04-vulnerabilites/vuln-05-exec.png` *(En attente)*
- Preuve PoC : `screenshots/05-resultats/vuln-05-poc.png` *(En attente)*

---

## 4. Mesures Correctives et Remédiation
- **Mise à jour logicielle** : Mettre à jour Apache Struts vers les versions 2.3.32 ou 2.5.10.1 (ou versions supérieures).
- **Filtrage applicatif (WAF)** : Déployer un Web Application Firewall (ModSecurity) pour inspecter et bloquer les en-têtes HTTP contenant des expressions OGNL.
- **Durcissement serveur** : Exécuter le conteneur de servlets Tomcat sous un utilisateur système dédié non privilégié (`tomcat`).

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
