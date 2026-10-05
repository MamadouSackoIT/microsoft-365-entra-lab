# 🟦 Lab Microsoft 365 & Microsoft Entra ID

## 📌 Présentation

Ce projet présente la mise en place d'un laboratoire **Microsoft 365 / Microsoft Entra ID** réalisé dans le cadre de ma montée en compétences en **support informatique et administration systèmes & réseaux**.

L'objectif était de reproduire plusieurs tâches rencontrées dans un environnement professionnel : gestion des utilisateurs, administration des licences, gestion de la messagerie avec Exchange Online, MFA, groupes, rôles administratifs, appareils, accès conditionnel et diagnostic d'incidents.

L'environnement repose sur une entreprise fictive nommée **NovaTech**.

Plusieurs incidents ont également été simulés afin d'appliquer une méthodologie de support :

**Incident → Diagnostic → Analyse des journaux → Identification de la cause → Correction → Validation**

---

# 🛠️ Technologies utilisées

- Microsoft 365 Admin Center
- Microsoft Entra ID
- Exchange Online
- Microsoft Authenticator
- Microsoft Entra Conditional Access
- Windows 11
- VirtualBox

---

# 🏢 Environnement NovaTech

Pour reproduire un environnement d'entreprise, plusieurs comptes et ressources ont été créés.

### Utilisateurs

- Mamadou Sacko — Administrateur
- Sophie Martin — Utilisatrice / compte de test
- Lucas Bernard — Utilisateur de test

### Ressources

- Boîte aux lettres partagée **Support NovaTech**
- Groupe de distribution **Équipe Marketing**
- Groupe de sécurité **Support IT**
- Groupe dynamique **Support IT - Dynamique**

---

# 👤 1. Gestion des utilisateurs Microsoft 365

Création et administration de plusieurs utilisateurs depuis le centre d'administration Microsoft 365.

Manipulations réalisées :

- Création de comptes utilisateurs
- Modification des informations utilisateur
- Réinitialisation des mots de passe
- Blocage et déblocage des connexions
- Suppression d'un utilisateur
- Gestion des licences
- Test de connexion avec différents comptes

Ces manipulations permettent de reproduire les opérations courantes réalisées par un technicien support lors de l'arrivée, de la modification ou du départ d'un collaborateur.

CLiquez ici : Pt 1 Présentation de l’environnement Microsoft 365.png

---

# 🔑 2. Gestion des licences Microsoft 365

Administration des licences depuis le Microsoft 365 Admin Center.

J'ai notamment travaillé sur :

- Attribution d'une licence à un utilisateur
- Retrait d'une licence
- Vérification des applications et services associés
- Vérification de la disponibilité des licences
- Diagnostic d'un utilisateur ne disposant d'aucune licence
- Vérification de l'accès à Exchange Online après attribution d'une licence

Un incident a notamment été simulé avec **Lucas Bernard**.

Le compte pouvait s'authentifier sur Microsoft 365 mais ne disposait pas de boîte aux lettres Outlook.

Le diagnostic a permis d'identifier :

**Licences : 0**

Après attribution d'une licence contenant **Exchange Online**, la boîte aux lettres de Lucas a été provisionnée et l'accès à Outlook a été validé.

---

# 📧 3. Administration Exchange Online

Plusieurs fonctionnalités de messagerie Microsoft 365 ont été configurées.

### Boîte aux lettres partagée

Création de la boîte :

**Support NovaTech**

Configuration de droits permettant à un utilisateur autorisé :

- d'accéder à la boîte partagée ;
- de consulter les messages ;
- d'envoyer des messages au nom de la boîte.

Les permissions **Full Access** et **Send As** ont été étudiées.

---

## Groupe de distribution

Création du groupe :

**Équipe Marketing**

Objectif : permettre l'envoi d'un message à plusieurs utilisateurs à partir d'une seule adresse.

La réception de messages provenant d'expéditeurs externes a également été testée.

---

## Alias de messagerie

Configuration et test d'alias afin de permettre à une boîte aux lettres de recevoir des messages via plusieurs adresses.

---

## Transfert de courrier

Simulation du départ d'un collaborateur avec configuration d'un transfert de ses messages vers une autre boîte.

Cette manipulation permet de reproduire une partie d'une procédure d'**offboarding**.

---

# ☁️ 4. Administration Microsoft Entra ID

Microsoft Entra ID a été utilisé pour administrer les identités de l'environnement NovaTech.

Manipulations réalisées :

- Gestion des utilisateurs
- Gestion des groupes
- Gestion des propriétés utilisateurs
- Gestion des rôles administratifs
- Gestion des méthodes d'authentification
- Consultation des journaux de connexion
- Gestion des appareils
- Mise en place de stratégies d'accès conditionnel

---

# 👥 5. Groupes de sécurité

## Groupe statique

Création du groupe :

**Support IT**

Type :

**Security / Assigned**

Les utilisateurs sont ajoutés manuellement au groupe.

---

## Groupe dynamique

Création du groupe :

**Support IT - Dynamique**

Une règle dynamique a été utilisée afin d'ajouter automatiquement les utilisateurs appartenant au département **Support**.

Exemple de règle :

```text
(user.department -eq "Support")
```

Après modification du département de Sophie Martin vers **Support**, son compte a automatiquement rejoint le groupe dynamique.

Cette manipulation permet de comprendre l'automatisation de la gestion des appartenances dans Microsoft Entra ID.

---

# 🛡️ 6. Authentification multifacteur — MFA

Configuration et test de l'authentification multifacteur avec **Microsoft Authenticator**.

Manipulations réalisées :

- Configuration de Microsoft Authenticator
- Validation d'une connexion avec MFA
- Utilisation du number matching
- Consultation des méthodes d'authentification
- Réinitialisation des méthodes MFA
- Réenregistrement de Microsoft Authenticator

Un scénario de **changement/perte de téléphone** a notamment été simulé.

L'ancienne méthode d'authentification a été supprimée puis Microsoft Authenticator a été enregistré de nouveau.

---

# 👮 7. Rôles administratifs et moindre privilège

Étude du principe de **Least Privilege / moindre privilège**.

Au lieu d'utiliser systématiquement un compte **Global Administrator**, un rôle administratif limité a été attribué à Sophie Martin :

**Helpdesk Administrator**

Ce rôle a ensuite été testé.

Sophie pouvait effectuer certaines opérations de support sur un utilisateur standard comme Lucas Bernard.

Une tentative de réinitialisation du mot de passe du compte Global Administrator a également été effectuée.

L'opération a été refusée en raison du niveau de privilège insuffisant.

Cela permet d'illustrer le principe :

> Un technicien doit disposer uniquement des permissions nécessaires à ses missions.

---

# 💻 8. Gestion des appareils Microsoft Entra

Un poste Windows 11 appartenant au laboratoire Active Directory NovaTech a été enregistré dans Microsoft Entra ID.

Le poste était déjà joint au domaine :

```text
novatech.local
```

Le compte professionnel de Sophie Martin a ensuite été ajouté au poste.

Dans Microsoft Entra, l'appareil est apparu avec le type :

**Microsoft Entra Registered**

Cette manipulation a permis d'étudier les différences entre :

- Microsoft Entra Registered
- Microsoft Entra Joined
- Microsoft Entra Hybrid Joined

Elle permet également de comprendre la différence entre un environnement **Active Directory local** et un environnement d'identité **cloud Microsoft Entra ID**.

---

# 🔐 9. Conditional Access

Plusieurs stratégies d'accès conditionnel ont été créées afin de comprendre comment Microsoft Entra peut adapter les exigences d'authentification selon le contexte de connexion.

Pour éviter de perturber le laboratoire, les stratégies ont principalement été utilisées en :

**Report-only / Rapport uniquement**

Cela permet d'observer ce qu'aurait fait une stratégie sans réellement bloquer l'utilisateur.

---

## Politique MFA

Création d'une stratégie ciblant Sophie Martin avec :

- Utilisateur : Sophie Martin
- Ressource : Office 365
- Contrôle d'accès : MFA

Les résultats ont ensuite été vérifiés dans les journaux de connexion.

---

## MFA selon la plateforme

Une deuxième stratégie a été utilisée afin d'étudier l'application du MFA selon la plateforme de l'appareil.

Exemple :

**Windows → MFA**

La stratégie a ensuite été observée dans les journaux en mode **Report-only**.

---

# 🌐 10. Conditional Access selon l'emplacement réseau

Création d'un **Named Location / Emplacement nommé** :

```text
LAB - Réseau NovaTech
```

L'adresse IP publique utilisée par le laboratoire a été ajoutée à cet emplacement.

L'objectif était de distinguer :

**Connexion depuis le réseau NovaTech**

et

**Connexion depuis un autre réseau**

Une stratégie a ensuite été créée selon la logique :

```text
Utilisateur : Sophie Martin
        ↓
Ressource : Office 365
        ↓
Depuis n'importe quel emplacement
        ↓
SAUF : LAB - Réseau NovaTech
        ↓
Exiger MFA
```

---

## Test avec différentes adresses IP

Une connexion depuis le réseau initial a été observée avec l'adresse publique :

```text
86.252.222.214
```

Une autre connexion a ensuite été réalisée depuis un réseau disposant d'une autre adresse publique :

```text
78.242.54.32
```

Les journaux Microsoft Entra ont permis de vérifier quelle stratégie Conditional Access aurait été appliquée.

Cette manipulation m'a également permis de faire le lien entre :

- adressage IP privé ;
- NAT ;
- adresse IP publique ;
- identification d'un réseau dans Microsoft Entra.

---

# 📊 11. Journaux de connexion Microsoft Entra

Les journaux de connexion ont été utilisés comme outil de diagnostic.

Informations analysées :

- Utilisateur
- Date et heure
- Application
- Adresse IP
- Emplacement
- Statut de connexion
- Exigence d'authentification
- Code d'erreur
- Accès conditionnel
- Informations sur l'appareil

Ils ont notamment permis de vérifier les stratégies Conditional Access en mode **Report-only**.

---

# 🧰 12. Résolution d'incidents

Plusieurs incidents ont été reproduits afin de travailler une méthodologie de troubleshooting.

## Incident 1 — Impossible de se connecter

### Symptôme

Lucas Bernard ne parvient plus à se connecter à Microsoft 365.

### Diagnostic

Consultation des journaux de connexion Microsoft Entra.

Plusieurs tentatives apparaissent en échec avec le code :

```text
50126
```

Microsoft Entra indique :

```text
Error validating credentials due to invalid username or password.
```

### Cause

Identifiants incorrects.

### Résolution

Réinitialisation du mot de passe de Lucas avec un compte disposant des privilèges Helpdesk appropriés.

### Validation

Nouvelle connexion avec Lucas :

**Connexion réussie.**

---

# 🧰 13. Incident Exchange Online

## Symptôme

Lucas peut se connecter à Microsoft 365 mais ne dispose pas de sa messagerie Outlook.

## Diagnostic

Vérification du compte depuis :

**Microsoft 365 Admin Center → Utilisateurs actifs → Lucas Bernard → Licences et applications**

Résultat :

```text
Licences : 0
Applications : 0
```

## Cause

Aucune licence permettant d'utiliser Exchange Online n'était attribuée à Lucas.

## Résolution

Attribution d'une licence Microsoft 365 comprenant Exchange Online.

## Validation

Connexion à Outlook avec Lucas Bernard.

La boîte aux lettres est accessible.

**Incident résolu.**

---

# 🔄 14. Méthodologie de troubleshooting

Les différents exercices m'ont permis d'appliquer une méthodologie structurée :

```text
1. Identifier le symptôme
        ↓
2. Reproduire le problème
        ↓
3. Consulter les journaux
        ↓
4. Identifier la cause
        ↓
5. Appliquer une correction
        ↓
6. Tester avec l'utilisateur
        ↓
7. Valider la résolution
```

L'objectif est d'éviter d'appliquer directement une correction sans avoir identifié la cause de l'incident.

---

# 🧠 Compétences travaillées

Ce laboratoire m'a permis de travailler les compétences suivantes :

### Microsoft 365

- Administration des utilisateurs
- Gestion des licences
- Administration des services Microsoft 365
- Onboarding / Offboarding

### Exchange Online

- Boîtes aux lettres utilisateurs
- Boîtes partagées
- Alias
- Groupes de distribution
- Délégations
- Transfert de courrier

### Microsoft Entra ID

- Utilisateurs et groupes
- Groupes statiques et dynamiques
- Rôles administratifs
- RBAC
- Principe du moindre privilège
- Gestion des appareils

### Sécurité

- MFA
- Microsoft Authenticator
- Conditional Access
- Named Locations
- Analyse des connexions
- Analyse des adresses IP

### Support / Troubleshooting

- Analyse des journaux
- Codes d'erreur Entra
- Diagnostic d'authentification
- Diagnostic Exchange Online
- Réinitialisation de mots de passe
- Résolution et validation d'incidents

---

# 🚀 Conclusion

Ce laboratoire m'a permis de découvrir l'administration d'un environnement **Microsoft 365 / Microsoft Entra ID** en reproduisant des opérations courantes d'un service informatique.

Au-delà de la configuration des services, une attention particulière a été portée au **diagnostic des incidents**, à l'analyse des journaux et à l'application du **principe du moindre privilège**.

Ce projet complète mes autres laboratoires orientés **Active Directory, Windows Server, GLPI, réseau et support informatique**, avec une approche davantage orientée vers l'administration des services Microsoft Cloud.
