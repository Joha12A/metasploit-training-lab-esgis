# Fiche Vulnérabilité N°03 — UnrealIRCd 3.2.8.1 (CVE-2010-2075)

## 1. Contexte et Identification
- **Service cible** : UnrealIRCd (serveur IRC)
- **Port d'écoute** : `6667/tcp`
- **Version détectée** : `UnrealIRCd 3.2.8.1`
- **Référence CVE** : `CVE-2010-2075`
- **Score CVSS v3** : `9.8 (Critique)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description** : Serveur IRC UnrealIRCd, identifié via le scan Nmap (`reports/nmap-services.txt`).
- **Vecteur d'exposition** : Port réseau direct accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Module Metasploit** : `exploit/unix/irc/unreal_ircd_3281_backdoor`

## 3. Démarche survolée
- Le module Metasploit a confirmé que la cible était vulnérable (`[+] The target appears to be vulnerable. UnrealIRCd detected in banner`) et a envoyé la commande malveillante (`[*] Sending IRC backdoor command`).
- Cependant, aucune session interactive n'a été obtenue (backdoor dite "aveugle" : exécution sans retour).
- Un test avec un payload `cmd/unix/reverse_bash` n'a pas non plus abouti.

## 4. Mesures Correctives
- **Mise à jour logicielle** : Remplacer UnrealIRCd 3.2.8.1 par une version maintenue et exempte de backdoor.
- **Contrôle d'intégrité** : Vérifier les signatures GPG et les sommes SHA-256 des paquets.
- **Filtrage réseau** : Restreindre l'accès au port `6667/tcp` aux réseaux d'administration.
- **Surveillance** : Auditer les bannières des services IRC et détecter les versions obsolètes.

---
**Statut** : ⏳ **En attente** — Backdoor confirmée, session non obtenue ; à réévaluer avec une autre approche.