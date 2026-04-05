# 🎫 Zendesk Helpdesk Lab — Simulation Support IT N1/N2

> Environnement de lab simulé sur compte Zendesk trial, reproduisant les workflows d'un support IT en entreprise (PME / secteur médico-social). Utilisateurs et organisations fictifs, tickets construits sur des cas réels rencontrés en support N1/N2.

---

## 🏢 Contexte du lab

| Élément | Détail |
|---|---|
| **Outil** | Zendesk Support (compte trial) |
| **Agent** | Mina OUAAZIZ — Support IT N1/N2 |
| **Clients simulés** | Thomas DUPONT, Julie LEROY, Sophie Martin |
| **Organisations** | StartupTech Paris, PME Conseil & Co, Cabinet Médical Saint-Cloud |
| **Objectif** | Simuler un helpdesk IT complet : réception, traitement, escalade et résolution de tickets |

---

## 🗂️ Structure du repo

```
Zendesk-Helpdesk-Lab/
├── README.md
├── macros/
│   └── README.md
├── tickets/
│   ├── reset-mdp/
│   ├── vpn/
│   ├── escalade-n2/
│   └── installation-logiciel/
```

---

## ⚡ Macros configurées

Les macros sont des réponses préformatées permettant à l'agent de répondre rapidement et de manière standardisée. J'ai créé 4 macros correspondant aux incidents les plus fréquents en support IT N1/N2.

| Macro | Déclencheur | Action automatique |
|---|---|---|
| `Reset mot de passe AD` | Demande de réinitialisation mdp | Réponse + Statut → En attente |
| `Problème VPN – diagnostic initial` | Incident VPN signalé | Réponse diagnostic + Statut → En attente |
| `Ticket reçu – accusé de réception` | Ouverture de ticket | Confirmation SLA + Statut → Ouvert |
| `Escalade N2` | Incident hors périmètre N1 | Notification escalade + Statut → En attente + Priorité → Haute |

> **Choix de conception :** chaque macro intègre une action de changement de statut pour automatiser le workflow agent et éviter les oublis de mise à jour. Le message de la macro `Accusé de réception` inclut les délais SLA différenciés par priorité (Urgente / Haute / Normale) pour aligner les attentes utilisateur dès l'ouverture du ticket.

---

## 🎫 Tickets traités

Vue d'ensemble des 4 tickets résolus dans ce lab :

![Tableau de bord tickets résolus](https://github.com/user-attachments/assets/e2123e1c-7fc6-4515-b346-fee18f6f9c6b)

---

### Ticket #6 — Reset mot de passe Active Directory

**Demandeur :** Thomas DUPONT — StartupTech Paris
**Type :** Incident | **Priorité :** Élevée
**Marqueurs :** `reset-mdp` `active-directory` `n1`

**Scénario :** L'utilisateur ne peut plus se connecter à son poste Windows depuis le matin. Mot de passe refusé, rendez-vous client dans 2h — ticket urgent.

**Workflow appliqué :**
1. Réception du ticket → macro *Reset mot de passe AD* appliquée → demande de vérification d'identité
2. Statut → **En attente** de la réponse utilisateur
3. Réception des infos (nom, identifiant Windows `t.dupont`, service Commercial)
4. Réinitialisation du mot de passe AD + fourniture du mot de passe temporaire
5. Ticket → **Résolu**

**Étape 1 — Macro appliquée, statut En attente :**

![Reset mdp – En attente](https://github.com/user-attachments/assets/17ff4675-e690-49dd-bac2-abaab39fa15d)

**Étape 2 — Ticket résolu :**

![Reset mdp – Résolu](https://github.com/user-attachments/assets/f7b380d6-ea67-4641-80c3-3d399237e6f5)

---

### Ticket #7 — Problème VPN en télétravail

**Demandeur :** Julie LEROY — PME Conseil & Co
**Type :** Incident | **Priorité :** Normale
**Marqueurs :** `vpn` `télétravail` `n1`

**Scénario :** L'utilisatrice est en télétravail et ne peut plus se connecter au VPN. Erreur "Connexion refusée". Problème survenant aussi en 4G → indique une issue de configuration côté client VPN, pas réseau local.

**Workflow appliqué :**
1. Réception du ticket → macro *Problème VPN – diagnostic initial* appliquée → collecte d'informations
2. Statut → **En attente**
3. Réception des infos (client : Cisco AnyConnect, OS : Windows 10 22H2, problème depuis lundi, présent aussi en 4G)
4. Diagnostic : problème côté configuration VPN → préconisation désinstallation/réinstallation Cisco AnyConnect
5. Ticket → **Résolu**

**Macro appliquée, statut En attente :**

![VPN – En attente](https://github.com/user-attachments/assets/84118486-eb8d-448f-b92f-750aec27b4b2)

---

### Ticket #8 — Serveur de fichiers inaccessible (Escalade N2)

**Demandeur :** Sophie Martin — Cabinet Médical Saint-Cloud
**Type :** Problème | **Priorité :** Urgente
**Marqueurs :** `serveur` `escalade-n2` `critique`

**Scénario :** Le lecteur réseau Z: est inaccessible pour toute l'équipe depuis 9h. 15 personnes bloquées, dossiers patients inaccessibles — incident critique nécessitant une escalade N2 immédiate.

**Workflow appliqué :**
1. Réception → macro *Escalade N2* appliquée → notification à l'utilisatrice + transfert au groupe N2
2. Statut → **En attente**, Priorité → **Urgente**
3. Intervention N2 : service SMB arrêté suite à une mise à jour automatique nocturne → redémarrage du service + vérification des droits sur Z:
4. Confirmation de résolution par l'utilisatrice
5. Ticket → **Résolu**

> **Note de gestion :** Ce ticket illustre la procédure d'escalade N1→N2 : le technicien N1 collecte les informations, qualifie l'incident comme hors périmètre N1, applique la macro d'escalade et transfère avec le contexte complet pour éviter toute perte d'information.

**Escalade N2 appliquée, statut En attente :**

![Escalade N2 – En attente](https://github.com/user-attachments/assets/a597223e-abdd-4610-8e54-c8421074535f)

**Ticket résolu après intervention N2 :**

![Escalade N2 – Résolu](https://github.com/user-attachments/assets/463684a4-444f-4701-b1e0-d96ce567ace2)

---

### Ticket #9 — Installation logiciel Adobe Reader

**Demandeur :** Thomas DUPONT — StartupTech Paris
**Type :** Question | **Priorité :** Basse
**Marqueurs :** `installation` `logiciel` `n1`

**Scénario :** Demande d'installation d'Adobe Reader pour consultation de documents PDF client. Traitement N1 simple, résolution rapide.

**Workflow appliqué :**
1. Réception → macro *Ticket reçu – accusé de réception* appliquée
2. Installation à distance d'Adobe Reader
3. Confirmation de bon fonctionnement par l'utilisateur
4. Ticket → **Résolu**

**Ticket résolu :**

![Adobe Reader – Résolu](https://github.com/user-attachments/assets/41ebcf24-5c54-4f8d-aea9-de8a5a3689b3)

---

## 📊 Synthèse

| Ticket | Type | Priorité | Macro utilisée | Résultat |
|---|---|---|---|---|
| Reset mdp AD | Incident | Élevée | Reset mot de passe AD | ✅ Résolu N1 |
| VPN télétravail | Incident | Normale | Problème VPN | ✅ Résolu N1 |
| Serveur fichiers | Problème | Urgente | Escalade N2 | ✅ Résolu N2 |
| Installation logiciel | Question | Basse | Accusé de réception | ✅ Résolu N1 |

---

## 🔧 Stack & compétences démontrées

- **Zendesk Support** — configuration de macros, gestion du cycle de vie des tickets, workflow agent
- **Support IT N1/N2** — diagnostic, escalade, communication utilisateur
- **Gestion des priorités et SLA** — qualification des incidents par type et urgence
- **Active Directory** — procédure de reset mot de passe
- **VPN / réseau** — diagnostic Cisco AnyConnect
- **Secteurs couverts** — PME, startups, médico-social

---

## Auteure

**Mina OUAAZIZ** — Technicienne Supérieure Systèmes et Réseaux  
Passionnée par la cybersécurité défensive, l'administration système et le support IT.
