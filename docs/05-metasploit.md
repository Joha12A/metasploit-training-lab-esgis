# 05 - Exploitation Pédagogique et Modules Metasploit

## 1. Objectif
Comprendre et utiliser le framework Metasploit (msfconsole) pour tester de manière contrôlée et autorisée les vulnérabilités identifiées sur la cible **ESGIS VulnBox** (`10.1.0.1`), en vérifiant le comportement des modules (auxiliaires, exploits, payloads).

## 2. Prérequis
- Metasploit Framework initialisé (`msfdb init` / `msfconsole`).
- Connectivité réseau établie vers la cible `10.1.0.1`.
- Références CVE et modules associés identifiés.

## 3. Procédure
Pour chaque vulnérabilité étudiée :
1. Démarrage de la console Metasploit :
   ```bash
   msfconsole -q
   ```
2. Recherche du module adapté :
   ```text
   search cve:<ANNEE>-<NUMERO>
   ```
3. Sélection et inspection du module :
   ```text
   use <chemin_du_module>
   show info
   show options
   ```
4. Configuration des paramètres du module (`RHOSTS`, `RPORT`, `LHOST`, `LPORT`) :
   ```text
   set RHOSTS 10.1.0.1
   ```
5. Test de vérification d'éligibilité (si disponible) :
   ```text
   check
   ```
6. Exécution contrôlée de l'action autorisée.

## 4. Captures d'écran
*Emplacement réservé aux captures d'écran :*
- Démarrage de msfconsole et vérification de la base : `screenshots/04-vulnerabilites/msf-init.png` *(En attente)*
- Configuration et exécution des modules : `screenshots/04-vulnerabilites/msf-module-exec.png` *(En attente)*

## 5. Résultat observé
*(Section en attente : aucune exploitation n'a encore été réalisée)*

## 6. Analyse technique
*(Section en attente : analyse du vecteur de transmission du payload et de la réponse applicative)*

## 7. Recommandations éventuelles
- Appliquer le principe de moindre privilège aux services applicatifs pour limiter l'impact d'une exploitation réussie.
- Mettre en œuvre une surveillance comportementale et une détection d'intrusion (IDS/IPS).
