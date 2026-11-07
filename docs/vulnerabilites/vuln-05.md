# Fiche Vulnérabilité N°05 — Apache Tomcat

## 1. Contexte et Identification
- **Service cible** : Apache Tomcat
- **Port d'écoute** : `8081/tcp`
- **Version détectée** : `Apache Tomcat 7.0.109`
- **Référence CVE** : `CVE-2017-12615`
- **Score CVSS v3** : `8.1 (Élevé)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description du composant** : Service identifié via le scan de bannières Nmap (`reports/nmap-services.txt`).
- **Vecteur d'exposition** : Port réseau direct accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Module Metasploit associé** : `exploit/multi/http/tomcat_jsp_upload_bypass`

## 3. Preuves Réelles
> [!NOTE]
> *Cette section sera complétée uniquement avec les captures d'écran et sorties console obtenues lors de l'exercice encadré.*

- **Capture d'écran de l'analyse** : `screenshots/04-vulnerabilites/vuln-05-exec.png` *(En attente)*
- **Preuve technique / Résultat** : `screenshots/05-resultats/vuln-05-poc.png` *(En attente)*
- **Extrait de journal / Sortie console** :
```text
[En attente de vérification sur 10.1.0.1]
```

## 4. Mesures Correctives et Remédiation
- **Mise à jour logicielle** : Appliquer les correctifs de sécurité fournis par l'éditeur pour la version `Apache Tomcat 7.0.109`.
- **Principe de moindre privilège** : Exécuter le service sous un compte non privilégié.
- **Filtrage réseau** : Restreindre l'accès au port `8081` aux seuls hôtes d'administration autorisés.

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
