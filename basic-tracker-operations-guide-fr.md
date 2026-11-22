# Basic Tracker

## Guide des opérations

Ce guide des opérations explique ce qu’est le **Basic Tracker**, comment y accéder et comment l’utiliser au mieux conformément au **Universal Confirmations Rulebook** et au **Stop and Recall for Case Management Rulebook** (pour les clients abonnés à **Case Management**).

Ce document s’adresse à tous les utilisateurs Swift éligibles qui souhaitent accéder au **Basic Tracker** afin de suivre et de confirmer, en partie, les paiements et de gérer les demandes d’investigation.

**27 mars 2026**

---

# Table des matières

**Préface**  
**Modifications importantes**

### 1. Introduction

1.1 Universal Confirmations  
1.2 Services Case Management  
1.3 Rich Data Access  
1.4 Network Interoperability  
1.5 Swift Go  
1.6 Basic Tracker  

### 2. Accéder au Basic Tracker

2.1 Configuration système requise  
2.2 Disponibilité du service  
2.3 Réseau et connectivité  
2.4 Règles de visibilité dans le Basic Tracker  

### 3. Utiliser le Basic Tracker

3.1 Page d’accueil  
3.2 Paiements en attente  
3.3 Paiements Swift Go en attente  
3.4 Stop and Recall en attente  
3.5 Vue de la transaction  
3.6 Vue de la transaction avec flux de retour  
3.7 Vue de la transaction avec une branche PMI  
3.8 Vue de la transaction avec une branche Network Interoperability  
3.9 Vue de la transaction avec abandons de messagerie  
3.10 Vue de la transaction avec opérations Stop and Recall  
3.11 Opérations manuelles dans l’interface graphique - Mises à jour des paiements  
3.12 Opérations manuelles dans l’interface graphique - Demandes Stop and Recall  
3.13 Opérations manuelles dans l’interface graphique - Fonction Rich Data Access  
3.14 Opérations manuelles dans l’interface graphique - Vue Transaction Copy  
3.15 Opérations manuelles dans l’interface graphique - Recherche Transaction Copy  
3.16 Score Universal Confirmations  
3.17 Statut de conformité Universal Confirmations des autres banques  
3.18 Score Case Management  
3.19 Score Swift Go  
3.20 Administrer les paramètres  

### 4. Utiliser les API du Tracker

### 5. Qualité des données du Tracker

### 6. Mise à niveau vers Swift GPI

### 7. Support

**Annexe A - Alertes du Tracker**  
A.1 Alertes du Tracker basées sur FIN MT  
A.2 Alertes du Tracker basées sur ISO trck  
A.3 Erreurs du Tracker  

**Annexe B - Traitement du Tracker dans l’environnement de test**

**Mentions légales**

---

# Préface

## À propos de ce document

Ce guide des opérations explique ce qu’est le **Basic Tracker**, comment y accéder et comment l’utiliser au mieux conformément au **Universal Confirmations Rulebook** et au **Stop and Recall for Case Management Rulebook** (pour les clients abonnés à **Case Management**).

Ce document s’adresse à tous les utilisateurs Swift éligibles qui souhaitent accéder au **Basic Tracker** afin de suivre et de confirmer, en partie, les paiements et de gérer les demandes d’investigation.

## Public cible

Ce document s’adresse aux utilisateurs **FIN** ou **SwiftNet** appartenant aux catégories d’utilisateurs **Supervised Financial Institutions (SUPE)** ou **Payments System Participants (PSPA)**.

Pour plus d’informations sur les catégories d’utilisateurs Swift, consultez les **Swift Corporate Rules**.

## Documentation associée

- Swift GPI Rulebook for Mandatory Services - GPI Customer Credit Transfer and GPI Cover Payments
- Stop and Recall for Case Management Rulebook
- Swift GPI Supplementary Message Format Validation Rules
- Swift GPI Service Description
- Standards MT General Information
- FIN Operations Guide
- FIN Service Description
- Universal Confirmations Rulebook
- Universal Confirmations - Customer Credit Transfer - Frequently Asked Question
- CBPR+ Data Integrity Market Practice Guidance

**Remarque :** pour accéder aux liens vers les documents, vidéos et supports de formation relatifs au déblocage des confirmations de paiement, consultez **Unlocking payment confirmations for all**.

## Conventions de lecture

Les termes suivants peuvent également être utilisés sous leur forme abrégée :

| Terme | Abréviation |
| --- | --- |
| Tracker for Swift GPI | (GPI) Tracker |
| Observer Insights for Swift GPI | (GPI) Observer Insights |
| Directory for Swift GPI | (GPI) Directory |
| Swift GPI customers | Clients GPI |
| Swift GPI services and products | Services et produits GPI |
| Swift GPI Contractual Documentation | Documentation contractuelle GPI |
| Swift Test Sparring Partner | TSP |
| Stop and Recall service | SRP |
| Universal Confirmations | UC |

---

# 1. Introduction

## 1.1 Universal Confirmations

**Universal Confirmations** contribue à l’objectif consistant à rendre les paiements rapides, transparents et traçables. Associé aux services **Swift Global Payments Innovation (GPI)**, il est conçu pour garantir que tous les paiements puissent être suivis de bout en bout et confirmés.

Une exigence essentielle d’**Universal Confirmations** impose aux agents du créancier qui reçoivent via Swift un message **ISO 20022 pacs.008** ou **FIN MT 103** de notifier le Tracker lorsque le compte du créancier a été crédité.

Lorsque le crédit ne peut pas être comptabilisé immédiatement, les clients doivent alternativement indiquer que le crédit est **en attente**, ou qu’il a été **rejeté**.

Une version simplifiée de l’interface graphique du Tracker est mise à la disposition des utilisateurs éligibles afin de permettre aux clients de fournir ces confirmations. Cette interface offre également une visibilité limitée sur les transactions de paiement.

D’autres canaux sont disponibles pour fournir les confirmations, notamment les messages **trck** ou les requêtes via **API**. Ces canaux sont destinés à prendre en charge les clients qui doivent fournir des confirmations de manière systématique, notamment lorsqu’ils traitent de gros volumes de virements de crédit client.

**Universal Confirmations** est obligatoire pour les clients éligibles qui ne sont pas abonnés aux services **Swift GPI**. Le respect du **Universal Confirmations Rulebook** est contrôlé par l’**Observer**, et les clients peuvent consulter directement leurs scores de confirmation dans le **Basic Tracker**.

Depuis décembre 2022, le Tracker assure également le suivi des flux de retour reposant sur les messages **ISO 20022 pacs.004**. Le suivi des retours est uniquement pris en charge pour les flux de paiement passant par Swift et ceux-ci sont visibles dans le **Basic Tracker**.

Les clients ne sont pas tenus, et ne peuvent pas, fournir de confirmations au Tracker concernant les transactions retournées.

Les clients **Universal Confirmations** peuvent suivre les paiements retournés conformément aux règles de visibilité restreinte applicables au **Basic Tracker**.

## 1.2 Services Case Management

Swift a développé plusieurs services destinés à réduire les difficultés rencontrées dans l’écosystème des paiements transfrontaliers.

Pour la gamme de produits **Case Management**, ces services sont :

- Le service **Stop and Recall (SRP)**, qui vise à arrêter immédiatement un paiement effectué de manière incorrecte ou frauduleuse.
- Le service **Case Orchestrator**, qui vise à résoudre rapidement une investigation liée à des informations de paiement manquantes ou incorrectes.

Bien que ces deux services aient initialement été proposés uniquement aux clients GPI, ils sont désormais étendus à tous les clients Swift appartenant aux catégories **Supervised Financial Institutions (SUPE)** ou **Payments System Participants (PSPA)**.

Plus précisément, les clients **SUPE/PSPA non-GPI** ont la possibilité de souscrire à la gamme de produits **Case Management**, qui comprend les services **SRP** et **Case Orchestrator**.

L’élargissement de la portée des services SRP et Case Orchestrator, en maximisant leur adoption et leur utilisation par les clients SUPE/PSPA non-GPI, permet aux clients :

- de contacter efficacement et de manière fluide leurs contreparties, qu’elles soient GPI ou non-GPI, lorsque des investigations doivent être traitées en urgence ;
- d’adopter des normes communes et des codes de demande harmonisés ;
- de s’appuyer sur des règles métier et des pratiques de marché similaires ;
- de bénéficier des fonctionnalités avancées du Tracker et de suivre attentivement l’état des demandes en cours ou clôturées.

En supprimant l’obligation de souscrire à Swift GPI et en permettant ainsi à tout client SUPE/PSPA d’opter pour les services SRP et Case Orchestrator, cette approche constitue une excellente solution tant pour les clients GPI que pour les clients Universal Confirmations.

Plus précisément :

- les clients GPI peuvent utiliser les fonctionnalités du Tracker ainsi que leurs investissements SRP et Case Orchestrator, leurs demandes pouvant être traitées de manière centralisée via le Tracker ;
- les clients SUPE/PSPA non-GPI peuvent utiliser l’application **Basic Tracker** et leur expertise en matière d’Universal Confirmations afin d’optimiser le traitement de leurs investigations.

Enfin, l’extension des services SRP et Case Orchestrator à tous les clients SUPE/PSPA est conforme à l’ambition de proposer aux clients une expérience cohérente, complète et universelle, sans friction, lorsqu’ils échangent des paiements transfrontaliers.

## 1.3 Rich Data Access

Afin d’aider les banques à mettre en œuvre les recommandations **CBPR+ Data Integrity Market Practice Guidance** et de favoriser une approche cohérente pour accéder aux données enrichies qui peuvent ne pas être transmises dans les paiements au format historique, Swift a développé la fonctionnalité **Rich Data Access**.

Cette fonctionnalité est disponible à l’ensemble des utilisateurs Swift concernés appartenant aux catégories **Supervised Financial Institutions (SUPE)** ou **Payments System Participants (PSPA)** qui peuvent avoir besoin d’accéder aux données enrichies **ISO 20022**.

La fonctionnalité **Rich Data Access** vise à proposer une alternative cohérente et plus efficace au processus bilatéral de **Request for Information (RFI)** décrit dans les recommandations CBPR+ Data Integrity Market Practice Guidance.

Elle est conçue pour permettre :

- au destinataire d’un message historique contenant une indication de troncature des données d’obtenir de manière cohérente les données enrichies directement auprès de Swift. Cela supprime la dépendance vis-à-vis de la banque précédente dans la transaction et accélère par conséquent la procédure RFI ;
- à l’émetteur de messages historiques qui ne peuvent pas transmettre les données enrichies ISO 20022 d’accéder à ces données enrichies via le Tracker. Cela aide les émetteurs de messages à créer tout message auxiliaire nécessaire pour transmettre les informations complètes au destinataire.

L’accès à la fonctionnalité **Rich Data Access** et son utilisation sont proposés sans frais supplémentaires.

La fonctionnalité est disponible via l’interface graphique (**GUI**) du **Swift GPI Tracker** et du **Basic Tracker**.

## 1.4 Network Interoperability

**Network Interoperability** crée un environnement standardisé permettant d’assurer le suivi de bout en bout des paiements impliquant des établissements financiers, des prestataires de services de paiement non bancaires (**NB-PSP**), des fournisseurs de portefeuilles (**WP**) et des infrastructures de marché des paiements (**PMI**).

Ses principaux composants comprennent :

- le respect de pratiques de marché standardisées pour les transferts de paiement ;
- le suivi de bout en bout des paiements, quels que soient les réseaux par lesquels la transaction est acheminée, y compris les réseaux situés en dehors de Swift ;
- les **confirmations on-behalf-of**, qui permettent aux clients, y compris les PMI, qui envoient des paiements aux agents du créancier via des réseaux hors Swift, de mettre à jour le **Basic Tracker** avec le résultat du transfert.

Que les messages circulent via les réseaux Swift ou via des réseaux non-Swift, ce service favorise des transactions fiables, sécurisées et traçables.

## 1.5 Swift Go

**Swift Go** prend en charge l’exécution de paiements transfrontaliers de faible montant en permettant aux PME (**petites et moyennes entreprises**) et aux particuliers d’effectuer des paiements transfrontaliers rapides, simples et prévisibles, de compte à compte.

Alors que ce service était initialement proposé uniquement aux clients GPI, il est désormais étendu à tous les clients Swift appartenant aux catégories **Supervised Financial Institutions (SUPE)** ou **Payments System Participants (PSPA)**.

Les clients SUPE/PSPA non-GPI peuvent notamment choisir de souscrire à **Swift Go**.

Ce parcours client permet aux clients non-GPI de mettre en œuvre Swift Go sans avoir à mettre en œuvre au préalable les services obligatoires GPI. Il leur permet également de continuer à confirmer leurs paiements à l’aide des spécifications **Universal Confirmations** dans certains cas, comme décrit dans les spécifications techniques du **Swift Go Rulebook**.

Tout client abonné à Swift Go peut échanger et suivre :

- les **MT 103** avec l’identifiant de type de service **009** ;
- les **pacs.008** avec le **Service Level G009** ;
- les paiements Swift Go effectués en dehors du réseau Swift.

Les clients Swift Go doivent envoyer ces paiements transfrontaliers de faible valeur (**MT 103/pacs.008**) et fournir leurs confirmations de statut au Tracker conformément au **Swift Go Rulebook**.

La prévisibilité est notamment assurée par l’insertion, par les clients Swift Go, d’entrées comportant l’identifiant de type de service **009** dans le **GPI Directory**.

## 1.6 Basic Tracker

Le **Basic Tracker** est une **interface graphique (GUI)** permettant aux utilisateurs Swift éligibles utilisant des messages de virement de crédit client (**MT 103 ou pacs.008**) d’appliquer de manière pratique les règles métier définies dans le **Universal Confirmations Rulebook**.

Le Basic Tracker est conçu pour :

- fournir aux utilisateurs un canal leur permettant de respecter manuellement le **Universal Confirmations Rulebook** et, pour les clients abonnés à **Swift Go**, de respecter manuellement le **Swift Go Rulebook** ;
- permettre les deux mises à jour de statut obligatoires :
  - confirmation du crédit (**ACCC**) ;
  - rejet du paiement (**RJCT**) ;
- permettre les mises à jour de statut recommandées :
  - paiement en attente (**ACSP/G002, ACSP/G003 et ACSP/G004**) ;
  - paiement transféré en dehors de FIN (**ACSP/G001**) ;
- permettre les mises à jour de statut facultatives, notamment les confirmations relatives aux instructions de paiement reçues en dehors de FIN ou SwiftNet et contenant une référence unique de transaction de bout en bout (**UETR**) ;
- permettre aux utilisateurs de suivre partiellement les instructions de paiement de virements de crédit client entrants et sortants et d’obtenir une visibilité restreinte sur leur activité de paiement ;
- permettre aux utilisateurs de mesurer leur propre niveau de conformité ainsi que celui de leurs contreparties commerciales aux règles métier définies dans le **Universal Confirmations Rulebook** et le **Swift Go Rulebook**.

Selon leurs volumes et leurs besoins, les utilisateurs peuvent confirmer les paiements par différents canaux. Outre le **Basic Tracker**, particulièrement adapté aux mises à jour manuelles des paiements, les confirmations peuvent également être fournies de manière automatisée.

Le Basic Tracker permet également aux utilisateurs abonnés à **Case Management** de traiter leurs demandes **Stop and Recall (SRP)** de manière centralisée, standardisée et optimisée.

Les clients **SUPE/PSPA non-GPI** abonnés à la gamme de produits **Case Management** peuvent utiliser le Basic Tracker pour :

- initier des demandes SRP conformément aux règles métier définies dans le **Stop and Recall for Case Management Rulebook** ;
- répondre aux demandes SRP conformément à ces mêmes règles ;
- analyser les statuts des demandes SRP qu’ils ont initiées et/ou reçues ;
- mesurer leur propre conformité ainsi que celle de leurs contreparties commerciales aux règles métier définies dans le Stop and Recall for Case Management Rulebook.

Selon leurs volumes et leurs besoins, les clients Case Management peuvent également traiter leurs demandes SRP via d’autres canaux. Outre le Basic Tracker, adapté aux opérations manuelles, les demandes peuvent être gérées via des canaux automatisés.

L’interface graphique du **Basic Tracker** permet également aux clients **SUPE** d’interroger la **Transaction Copy**.

Depuis l’introduction du suivi des retours de virements de crédit client à la fin de 2022, les utilisateurs peuvent également utiliser l’interface graphique du Basic Tracker pour suivre les retours, conformément aux règles de visibilité restreinte applicables à **Universal Confirmations**.

---

# 2. Accéder au Basic Tracker

## 2.1 Configuration système requise

Afin de garantir une utilisation optimale de l’interface graphique du **Basic Tracker**, les utilisateurs doivent respecter un ensemble minimal de prérequis système.

Ils doivent ensuite vérifier si leur infrastructure actuelle est suffisante ou si elle doit être mise à niveau ou renouvelée.

### 2.1.1 Exigences en matière de bande passante

Pour une utilisation optimale du Basic Tracker, Swift recommande une bande passante d’au moins **512 Kbit/s** disponible.

Cette bande passante est suffisante à condition que les navigateurs des utilisateurs finaux activent la mise en cache.

Si la bande passante disponible est inférieure, les utilisateurs doivent s’attendre à un processus de connexion plus lent, notamment lors de la première connexion.

Le processus de connexion est celui qui consomme le plus de données. Si les utilisateurs finaux ne se connectent pas tous simultanément, plusieurs utilisateurs peuvent travailler en parallèle avec une telle bande passante.

**512 Kbit/s suffisent pour 15 utilisateurs simultanés** travaillant activement sur le Basic Tracker.

Si plus de 15 utilisateurs travaillent régulièrement simultanément sur le Basic Tracker, l’institution devrait envisager une mise à niveau de son infrastructure.

### 2.1.2 Prérequis du poste utilisateur pour la GUI Basic Tracker

L’accès à l’interface graphique du Basic Tracker nécessite un navigateur Web approprié.

Les navigateurs pris en charge sont :

- Microsoft Edge ;
- Google Chrome ;
- Mozilla Firefox.

Lorsque l’utilisateur accède à la GUI Basic Tracker via **SwiftNet**, le navigateur doit être correctement configuré.

### 2.1.4 Exigences de contrôle d’accès

Les certificats **SwiftNet PKI** utilisés par les utilisateurs finaux doivent être configurés avec les rôles **RBAC** appropriés associés au **DN**.

L’utilisateur doit utiliser des certificats stockés sur un **HSM** ou sur un **personal token**.

Les utilisateurs finaux souhaitant accéder au Basic Tracker via **swift.com** doivent disposer des rôles Basic Tracker appropriés associés à leur utilisateur swift.com.

Ils doivent utiliser **MV-SIPN** comme réseau lorsqu’ils accèdent au Basic Tracker via leur adresse e-mail/mot de passe swift.com avec la vérification en deux étapes.

**Remarque :** les clients abonnés à **Case Management** ne peuvent pas gérer leurs demandes SRP via le Basic Tracker lorsqu’ils se connectent par swift.com.

Les certificats **SwiftNet PKI** sont nécessaires pour authentifier correctement les clients Case Management sur le Basic Tracker, car la fonctionnalité SRP est soumise à une signature de non-répudiation reposant sur les certificats SwiftNet PKI.

### Plusieurs BIC visibles via l’authentification swift.com

Un utilisateur peut se voir attribuer, dans swift.com, des rôles permettant d’accéder à plusieurs **BIC**.

Dans ce cas, l’utilisateur peut sélectionner, sur l’écran de connexion swift.com, le BIC qui doit être visible dans le Basic Tracker et pour lequel les statuts de paiement peuvent être mis à jour.

<img width="684" height="343" alt="image" src="https://github.com/user-attachments/assets/2e785c3d-f1d0-4c14-b9e1-618ad075d936" />

Pour sélectionner un autre BIC, l’utilisateur doit se déconnecter du Basic Tracker, puis se reconnecter via swift.com et sélectionner un autre BIC.

Pour voir simultanément tous les paiements provenant de plusieurs BIC dans le Basic Tracker, l’utilisateur doit utiliser soit un **token**, soit un certificat **HSM**.

<img width="628" height="322" alt="image" src="https://github.com/user-attachments/assets/a47a6526-34f4-4c80-9661-8f2e65e5f9a8" />

# 2.3.1 Accès au Basic Tracker à l’aide de certificats SwiftNet PKI

### Configuration pour les utilisateurs de certificats basés sur un token utilisant Internet comme réseau

1. Vous devez évaluer le nombre de tokens nécessaires pour votre institution, en tenant compte du nombre d’utilisateurs qui vont les utiliser. Prévoyez également suffisamment de tokens de réserve en cas de remplacement. Si nécessaire, vous pouvez commander des tokens personnels supplémentaires auprès de Swift.

2. Avant de pouvoir utiliser votre token personnel, vous devez installer le logiciel du token.

3. Créez et enregistrez les utilisateurs de tokens personnels pour chaque utilisateur final nécessitant un accès au Basic Tracker. Cette opération est effectuée par votre responsable de la sécurité dans l’application **Online Operations Manager (O2M)**.

   Les certificats existants peuvent être réutilisés, par exemple si les utilisateurs finaux utilisent déjà des certificats sur token personnel.

4. Attribuez les rôles **RBAC** du Tracker appropriés aux utilisateurs finaux concernés afin qu’ils puissent accéder au Basic Tracker.

   Comme à l’étape 3, l’attribution des rôles RBAC est également effectuée par votre responsable de la sécurité SwiftNet dans O2M.

   Selon leur rôle et leurs responsabilités, les certificats **SwiftNet PKI** utilisés par les utilisateurs finaux doivent être configurés avec les rôles RBAC appropriés associés au **DN**.

### Rôles RBAC

| Rôle | Description |
| --- | --- |
| **FullViewer** | Permet à un utilisateur final au sein d’une institution de voir toutes les transactions dans lesquelles son institution joue un rôle. |
| **Update** | Permet à un utilisateur final au sein d’une institution de mettre à jour les transactions de paiement dans lesquelles son institution joue un rôle. |
| **Admin** | Permet à un utilisateur final de gérer la configuration du Basic Tracker de son institution. Par exemple, l’utilisateur peut demander des notifications d’alerte au moyen du MT 199 ou du trck.003 depuis le Tracker. |
| **TMTransactionViewer** | Permet à un utilisateur final de consulter, via la fonctionnalité Rich Data Access de Case Management, les données enrichies qui ne peuvent pas être transmises depuis le dernier message pacs.008 enrichi échangé sur FINplus vers le MT 103 historique échangé sur FIN. Il permet également, via Transaction Copy, de consulter toutes les données disponibles pour une transaction donnée. |

**Remarque :** lorsqu’un utilisateur possède le rôle RBAC **Update**, il peut également consulter ces transactions dans l’interface graphique du Basic Tracker.

**Remarque :** le rôle **Admin** ne permet pas à l’utilisateur final de voir ou de consulter les transactions. Ce rôle est limité aux opérations de configuration.

**Remarque :** le rôle RBAC **TMTransactionViewer** doit toujours être utilisé en combinaison avec au moins un autre rôle RBAC, par exemple **FullViewer, TransactionViewer, TransactionUpdate** ou **Update**.

Les rôles du tableau précédent sont également étendus aux transactions et configurations **Swift Go** lorsque l’institution de l’utilisateur est abonnée et provisionnée pour le service Swift Go.

---

## Rôles supplémentaires pour les clients Case Management

Les clients Swift abonnés à **Case Management** bénéficient de privilèges supplémentaires et de rôles RBAC additionnels afin de permettre une séparation des privilèges et des responsabilités des utilisateurs.

Les privilèges des rôles RBAC précédents sont étendus aux clients Case Management, qui bénéficient également des rôles suivants :

| Rôle | Description |
| --- | --- |
| **FullViewer** | Permet à ses utilisateurs de consulter les opérations relatives aux transactions, c’est-à-dire les virements de crédit client, ainsi qu’aux investigations Stop and Recall qui concernent les BIC définis dans le périmètre du rôle RBAC FullViewer. |
| **TransactionViewer** | Permet à ses utilisateurs de consulter les opérations relatives aux transactions de virement de crédit client concernant les BIC définis dans le périmètre du rôle RBAC TransactionViewer. |
| **Update** | Permet à ses utilisateurs de consulter, mettre à jour, initier, traiter et approuver les opérations relatives aux transactions de virement de crédit client et aux investigations Stop and Recall concernant les BIC définis dans le périmètre du rôle RBAC Update. |
| **TransactionUpdate** | Permet à ses utilisateurs de consulter, mettre à jour et approuver les opérations relatives aux transactions de virement de crédit client concernant les BIC définis dans le périmètre du rôle RBAC TransactionUpdate. |
| **SensitiveData** | Permet à ses utilisateurs de consulter les opérations contenant des données sensibles, telles que le numéro de compte. |
| **Admin** | Permet à ses utilisateurs de consulter et de mettre à jour les opérations relatives aux paramètres concernant les BIC définis dans le périmètre du rôle RBAC Admin. |

Les rôles RBAC sont associés à un service.

Les noms de services pour l’interface graphique du Basic Tracker sont :

- **swift.tracker!p** pour le service Test and Training ;
- **swift.tracker** pour le service Live.

Par défaut, un seul BIC peut être défini dans le périmètre du rôle RBAC du **Distinguished Name (DN)** de l’utilisateur.

Si un DN utilisateur possède des privilèges sur plusieurs BIC non-GPI appartenant à la même hiérarchie, le DN doit remplir le formulaire électronique prévu à cet effet lorsqu’il utilise des certificats basés sur un token ou un HSM.

Une fois le formulaire soumis, le responsable de la sécurité peut déterminer dans **O2M** quels BIC non-GPI doivent être associés au périmètre des rôles RBAC accordés au DN utilisateur.

### Activation et configuration du token

1. Activez le token personnel via le **Swift Certificate Centre**.

2. Configurez le réseau pour **Swift Web Access**. Votre administrateur réseau doit effectuer les opérations suivantes :

   a. La configuration réseau doit être correctement établie afin que le navigateur installé sur le PC de chaque utilisateur puisse accéder au serveur Web du fournisseur de services Swift Web Access via **HTTPS**.

   b. Lors de l’utilisation de Swift Web Access dans **Alliance Web Platform Server-Embedded** avec **Alliance Gateway**, une configuration réseau supplémentaire est nécessaire.

   c. Acheminez le trafic HTTPS vers SwiftNet à l’aide de proxys HTTP, de dispositifs NAT ou d’une combinaison des deux.

   d. Si le proxy HTTP est installé sur un hôte différent de celui d’Alliance Gateway, l’hôte du proxy HTTP doit utiliser le **DNS SwiftNet** pour résoudre les noms d’hôtes des fournisseurs de services se terminant par `.swiftnet.sipn.swift.com`.

   e. Les pare-feu utilisés par le membre Swift Web Access doivent autoriser le trafic HTTPS des navigateurs vers les serveurs Web des fournisseurs de services.

3. Configurez les navigateurs des utilisateurs finaux :

   a. Configurez les paramètres de sécurité.  
   b. Ajoutez les sites de confiance.  
   c. Installez **SConnect**.

4. Accédez au Basic Tracker à l’aide des URL de déploiement suivantes :

| Application | URL de déploiement |
| --- | --- |
| Tracker (Test and Training) | `https://tracker-test.browse.swiftnet.sipn.swift.com/` |
| Tracker (Live) | `https://tracker.browse.swiftnet.sipn.swift.com/` |

---

# 2.3.2 Accès au Basic Tracker à l’aide d’une adresse e-mail / d’un mot de passe et de la vérification en deux étapes

<img width="654" height="340" alt="image" src="https://github.com/user-attachments/assets/1e5dd98f-38a5-4de3-83d6-affbf54f1093" />

Les utilisateurs disposant d’un compte **swift.com** peuvent accéder au Basic Tracker avec une adresse e-mail, un mot de passe et une vérification en deux étapes.

Ce mécanisme d’authentification repose sur les éléments suivants :

| Option d’authentification | Matériel | Réseau | Détails |
|---|---|---|---|
| Adresse e-mail / mot de passe et vérification en deux étapes | VPN | MV-SIPN | L’utilisateur final se connecte au service Swift Web Access uniquement avec une adresse e-mail, un mot de passe, la vérification en deux étapes et un navigateur disposant d’une connectivité vers Swift. |

**Remarque :** si votre institution utilise un fournisseur tiers pour se connecter à Swift, par exemple un **service bureau**, Swift recommande de contacter ce fournisseur afin de configurer l’accès au Basic Tracker.

## Configuration pour les utilisateurs de comptes swift.com utilisant MV-SIPN comme réseau

<img width="654" height="180" alt="image" src="https://github.com/user-attachments/assets/eb8bb588-addb-465c-b812-ecef58af5799" />

1. Créez un compte **swift.com**.

2. Confirmez votre compte swift.com via l’e-mail que vous recevez, associez votre compte à une institution et configurez la vérification en deux étapes.

   Pour finaliser la création de votre compte swift.com, votre administrateur swift.com doit l’approuver.

3. Connectez-vous à votre compte swift.com et, en fonction de votre rôle et de vos responsabilités, demandez un ou plusieurs rôles Basic Tracker swift.com dans la section **Manage your profile**.

| Rôle | Description |
| --- | --- |
| **Basic Tracker FullViewer (Live)** | Permet à un utilisateur final de consulter toutes les transactions dans lesquelles son institution joue un rôle dans l’environnement Live. |
| **Basic Tracker Update (Live)** | Permet à un utilisateur final de mettre à jour les transactions de paiement dans lesquelles son institution joue un rôle dans l’environnement Live. Lorsque l’utilisateur possède le rôle RBAC Update, il peut également consulter ces transactions dans la GUI Basic Tracker. |
| **Basic Tracker Admin (Live)** | Permet à un utilisateur final de gérer la configuration du Tracker de son institution dans l’environnement Live. Par exemple, il peut demander des notifications d’alerte au moyen du MT 199 ou du trck.003 depuis le Tracker. |
| **Basic Tracker FullViewer (Test and Training)** | Permet à un utilisateur final de consulter toutes les transactions dans lesquelles son institution joue un rôle dans l’environnement Test and Training. |
| **Basic Tracker Update (Test and Training)** | Permet à un utilisateur final de mettre à jour les transactions de paiement dans lesquelles son institution joue un rôle dans l’environnement Test and Training. |

**Remarque :** pour pouvoir effectuer des mises à jour via la GUI Basic Tracker dans l’environnement Test and Training, l’utilisateur doit disposer à la fois des rôles swift.com **Update** et **FullViewer** dans son profil swift.com.

### Basic Tracker Admin (Test and Training)

Ce rôle permet à un utilisateur final de gérer la configuration du Tracker de son institution dans l’environnement **Test and Training**.

Par exemple, l’utilisateur peut demander des notifications d’alerte au moyen du **MT 199** ou du **trck.003** depuis le Tracker.

**Remarque :** ce rôle ne permet pas à l’utilisateur final de voir ou de consulter les transactions. Il est limité aux opérations de configuration.

---

## Restrictions liées à Case Management

La création d’une demande **Stop and Recall** étant une opération faisant l’objet d’une **non-répudiation**, les utilisateurs doivent accéder à la GUI Swift GPI Tracker avec une méthode de connexion basée sur un certificat, soit un **token**, soit un **HSM**.

Par conséquent, l’authentification à la GUI Basic Tracker à l’aide d’une adresse e-mail, d’un mot de passe et de la vérification en deux étapes ne suffit pas pour bénéficier des fonctionnalités **Case Management**, y compris la fonctionnalité **Rich Data Access**.

Les rôles présentés précédemment sont également étendus aux transactions et configurations Swift Go lorsque l’institution de l’utilisateur est abonnée et provisionnée pour ce service.

Toute demande d’attribution d’un rôle Basic Tracker swift.com doit être approuvée par votre administrateur swift.com.

Swift recommande d’effectuer l’administration de swift.com, notamment la création de comptes et la gestion des mots de passe, depuis un poste de travail différent de celui utilisé pour se connecter au Basic Tracker.

L’administrateur swift.com doit s’assurer que les rôles appropriés sont attribués aux utilisateurs appropriés.

Ces utilisateurs peuvent accéder aux informations de l’institution dans le Basic Tracker et/ou les mettre à jour.

Plusieurs BIC peuvent être accessibles au moyen de la configuration swift.com.

### Case Management et SRP

Les clients **Case Management** ne peuvent pas gérer leurs demandes **SRP** dans le Basic Tracker lorsqu’ils sont connectés avec une adresse e-mail, un mot de passe et la vérification en deux étapes.

Ils doivent s’authentifier au moyen de **certificats SwiftNet PKI**, stockés sur un HSM ou sur un token Swift, afin de gérer leurs demandes SRP dans le Basic Tracker.

### Transaction Copy

Le Basic Tracker permet également aux utilisateurs d’interroger **Transaction Manager** afin de consulter les détails de **Transaction Copy**.

Cependant, les clients ne peuvent pas accéder aux fonctions Transaction Copy lorsqu’ils sont connectés avec une adresse e-mail, un mot de passe et la vérification en deux étapes.

Ils doivent s’authentifier avec des certificats **SwiftNet PKI**, stockés sur un HSM ou sur un token Swift, pour accéder à cette fonctionnalité.

---

# 2.4 Règles de visibilité dans le Basic Tracker

Les clients **Universal Confirmations** ont accès aux informations suivantes :

- le statut de la transaction ;
- le montant indiqué dans l’instruction ;
- la date et l’heure de la dernière mise à jour.

Les règles suivantes déterminent la visibilité des informations relatives aux agents dans le Basic Tracker.

### Si votre banque est non-GPI

Vous pouvez voir :

- la banque dont vous avez reçu le paiement ;
- la banque à laquelle vous avez envoyé le paiement ;
- l’agent du débiteur et/ou l’agent du créancier lorsque ces agents ont été identifiés par leur **BIC** dans les champs **Debtor Agent** et/ou **Creditor Agent** du message de paiement reçu et/ou envoyé par votre banque.

Tous les autres agents impliqués dans la transaction ne sont pas divulgués.

<img width="654" height="198" alt="image" src="https://github.com/user-attachments/assets/8163e6b7-b370-43cc-96e9-6daab2432c55" />

**Remarque :** les agents sont affichés aux clients non-GPI conformément à ces règles. Dans l’exemple du document, **Me** représente un client non-GPI.

Cet exemple suppose que l’agent du débiteur et l’agent du créancier sont présents dans le message reçu et/ou envoyé. Dans le cas contraire, ces agents ne sont eux aussi pas divulgués au client.

### Visibilité particulière pour les infrastructures de marché des paiements

Les clients **Payment Market Infrastructure (PMI)** participant au service **Network Interoperability** bénéficient d’une visibilité particulière dans le Basic Tracker.

Ils ont accès aux mises à jour de statut qu’ils ont fournies, y compris les branches générées en interne, ainsi qu’aux confirmations de crédit fournies **au nom de l’agent du créancier**.

---

# 3. Utiliser le Basic Tracker

## 3.1 Page d’accueil

La page d’accueil du Basic Tracker est composée de trois sections principales.

<img width="629" height="421" alt="image" src="https://github.com/user-attachments/assets/cac0e7fc-33ab-4d67-83fd-017450556e28" />

### Recherche

La fonction de recherche permet aux utilisateurs de rechercher et de suivre les transactions dans lesquelles leur banque a été ou est actuellement impliquée.

Les critères de recherche suivants peuvent être utilisés :

- **Tracking reference (UETR)** ;
- **Instruction Identification** (TRN du champ 20).

La fonction de recherche parcourt la base de données du Tracker afin de récupérer le résultat approprié parmi toutes les transactions générées au cours des **14 derniers jours calendaires**.

### Opérations en attente auprès de la banque de l’utilisateur

Cette section comptabilise tous les paiements qui ont atteint les BIC compris dans le périmètre de l’utilisateur au cours des deux dernières semaines et pour lesquels l’utilisateur doit fournir une confirmation dans le délai requis.

La section **Total operations pending** est divisée en deux sous-sections :

#### In progress

Il s’agit des paiements arrivés auprès de la ou des banques de l’utilisateur et pour lesquels aucune confirmation n’a encore été fournie.

Ces paiements en attente doivent être mis à jour, ou approuvés lorsque le paramètre d’approbation **4-eyes** est activé, dans les délais requis.

**Remarque :** dans le cas de branches de paiement de retour qui sont en cours auprès de la banque de l’utilisateur, aucune confirmation de l’utilisateur vers le Tracker n’est requise.

Toute confirmation fournie dans ce contexte est invalidée, y compris lorsqu’un agent du créancier recrédite le compte du client créancier.

#### On hold

Il s’agit des paiements arrivés auprès de la ou des banques de l’utilisateur et qui ont déjà été mis à jour par l’utilisateur avec le statut intermédiaire **On hold**.

Le nombre de **Total operations pending** correspond à l’agrégation des opérations en attente ayant les statuts **In progress** et **On hold**.

### Score Universal Confirmations

Le score **Universal Confirmations** et son code couleur affichés sur la page d’accueil du Basic Tracker permettent aux institutions financières d’identifier rapidement si elles respectent les règles métier définies dans le **Universal Confirmations Rulebook**.

Swift considère qu’une institution financière est conforme lorsque **80 % ou plus** de ses virements de crédit client entrants, c’est-à-dire les **MT 103 ou pacs.008**, ont été confirmés en moins de **deux jours ouvrés**.

Le score Universal Confirmations et le niveau de conformité des clients sont représentés par les couleurs suivantes :

- 🟢 **Vert** : l’institution financière respecte les règles métier Universal Confirmations.
- 🟠 **Orange** : l’institution financière ne respecte pas les règles métier Universal Confirmations et la période d’amélioration de **12 semaines** a commencé.
- 🔴 **Rouge** : l’institution financière ne respecte pas les règles métier Universal Confirmations depuis plus de **12 semaines consécutives avec trafic**.

Si plusieurs BIC non-GPI ont été associés au périmètre du **Distinguished Name (DN)** de l’utilisateur, le message neutre suivant apparaît :

> « You have multiple BICs in scope. See their respective scores in the dedicated screen. »

En français :

> **« Plusieurs BIC sont compris dans votre périmètre. Consultez leurs scores respectifs dans l’écran dédié. »**

Après avoir cliqué sur le score affiché sur la page d’accueil, une section dédiée au score Universal Confirmations de l’utilisateur apparaît.

### Swift Go

Dans le Basic Tracker, les utilisateurs abonnés à **Swift Go** peuvent consulter leur propre niveau de conformité ainsi que celui des autres clients Swift Go par rapport aux règles métier définies dans le **Swift Go Rulebook**.

Le document précise que cette fonctionnalité doit être disponible dans une version future.

Les administrateurs **GPI Observer Insights** de l’institution cliente peuvent également consulter directement les scores Swift Go de manière plus détaillée dans le portail **GPI Observer Insights**.

Pour plus d’informations sur le calcul des scores Swift Go, il faut se reporter à la section **Observer Insights** du **Swift Go Rulebook**.

### Case Management

Les utilisateurs abonnés à **Case Management** peuvent identifier, depuis la page d’accueil du Basic Tracker, les opérations **SRP** remontant jusqu’aux deux semaines précédentes.

**Remarque :** la section SRP apparaît uniquement sur la page d’accueil lorsqu’un client Case Management a reçu des opérations SRP en attente au cours des deux semaines précédentes.

<img width="629" height="354" alt="image" src="https://github.com/user-attachments/assets/8ea9777e-0492-4e7f-aa3b-ca217bc2a02d" />

## 3.2 Paiements en attente

Les paiements en attente devant être confirmés par l’utilisateur sont affichés dans un tableau de résultats.

<img width="629" height="342" alt="image" src="https://github.com/user-attachments/assets/22726187-4ec1-4f74-b569-0b1f10089ea7" />

Ce tableau est rapidement accessible depuis la page d’accueil en cliquant sur la section **Total operations pending**.

Le tableau comporte plusieurs fonctionnalités.

### Filtres

Des filtres de type **facette** sont disponibles en haut du tableau afin de permettre aux utilisateurs de parcourir et d’analyser facilement les résultats.

#### Tracking number

Ce filtre permet à l’utilisateur d’identifier, parmi toutes les opérations en attente, le paiement qui l’intéresse sur la base de son **UETR**.

Lorsqu’une recherche UETR est effectuée sur les opérations en attente, tous les autres filtres facette sont ignorés.

Plus précisément :

- **From-To** est défini sur **124 jours** ;
- le statut de transaction inclut tous les paiements **In progress** et **On hold** ;
- les actions en attente d’une approbation **4-eyes** sont également prises en compte.

**Remarque :** la recherche par UETR permet à tous les utilisateurs du Basic Tracker, y compris ceux ayant un statut de conformité **non conforme/rouge**, d’effectuer une recherche parmi les opérations en attente à partir de l’UETR du paiement.

En revanche, la recherche depuis la page d’accueil reste désactivée pour les utilisateurs Universal Confirmations non conformes/rouges.

#### From - To

La valeur par défaut de ce filtre est :

**From = aujourd’hui - 14 jours**  
**To = aujourd’hui**

Le tableau affiche donc initialement tous les paiements en attente ayant atteint la ou les banques de l’utilisateur au cours des deux dernières semaines.

Ce filtre peut être modifié afin d’afficher les paiements en attente sur la période souhaitée.

#### Status

Ce filtre présente les deux statuts possibles d’un paiement en attente auprès de la banque de l’utilisateur :

- **In progress**
- **On hold**

Si l’utilisateur clique depuis la page d’accueil sur **Total operations pending - In progress**, le filtre **In progress** est automatiquement sélectionné.

La même logique s’applique au statut **On hold**.

#### 4-eyes approval

Les utilisateurs peuvent activer le filtre **Pending my approval** afin de se concentrer uniquement sur les paiements nécessitant leur approbation selon le mécanisme **4-eyes**.

### Display only transactions without return legs

Ce critère permet d’exclure les transactions contenant des branches de retour.

Ces transactions possèdent le statut **In-Progress**, mais les utilisateurs ne peuvent pas mettre à jour les flux de retour dans l’interface graphique.

### Tableau de résultats

Le tableau répertorie les paiements en attente auprès de la ou des banques de l’utilisateur et qui doivent être mis à jour par celui-ci avec un statut final conformément au **Universal Confirmations Rulebook**.

Les résultats du tableau sont automatiquement adaptés aux valeurs sélectionnées dans les filtres facette.

La GUI affiche les **50 premiers résultats**.

Pour obtenir l’ensemble des résultats, l’utilisateur doit faire défiler la page jusqu’en bas.

Par défaut, tous les résultats de recherche utilisent l’heure locale de la transaction.

Les différents types de résultats disposent de présentations différentes :

- lorsqu’un utilisateur possède le rôle RBAC **Update** et peut agir sur les transactions en attente, un chevron bleu apparaît à la place du chevron classique gris ;
- lorsque l’utilisateur clique sur une ligne du tableau, il est dirigé vers la vue de transaction correspondante ;
- lorsqu’une approbation 4-eyes est en attente et que l’utilisateur possède le rôle RBAC lui permettant d’agir, une barre bleue et des bordures bleues apparaissent autour de la transaction concernée ;
- lorsqu’un utilisateur disposant du rôle RBAC Update initie une opération alors que le processus 4-eyes est activé, l’opération reste affichée comme étant en attente auprès de la banque ;
- l’initiateur ne pouvant pas effectuer l’approbation 4-eyes, un chevron classique indique qu’il ne peut pas agir sur cette opération ;
- si quelqu’un rejette une transaction pendant le processus 4-eyes, une barre rouge apparaît.

### Affichage dans l’heure locale

Par défaut, toutes les heures sont affichées selon l’heure locale de la transaction.

Les utilisateurs peuvent choisir d’afficher les transactions selon leur propre heure locale en activant l’option :

**Show in my local time**

Le choix de cette option est enregistré dans le **local storage** du navigateur.

Il reste conservé tant que l’utilisateur utilise le même poste/plateforme et ne supprime pas le cache du navigateur.

### Export

Les résultats du tableau peuvent être exportés à l’aide du bouton **Export**.

Le tableau affiché à l’écran est exporté au format **CSV**.

L’export ne contient pas la totalité des résultats de recherche si l’utilisateur n’a pas fait défiler la liste jusqu’à sa fin.

Les colonnes de l’export sont celles qui sont affichées à l’écran.

## 3.3 Paiements Swift Go en attente

Les clients **Swift Go** peuvent filtrer les transactions Swift Go en attente en cliquant sur **Swift Go Payment**.

Les résultats de recherche affichent toutes les transactions de paiement reçues comportant des événements incluant l’identifiant de type de service **009**.

Cette fonctionnalité est visible uniquement pour les clients Swift Go.

Elle peut être combinée avec les filtres de transactions de paiement existants décrits dans la section **Pending Payments**.

<img width="629" height="195" alt="image" src="https://github.com/user-attachments/assets/f0916e4e-6c96-4fac-9414-23d3f8a940d0" />

## 3.4 Stop and Recall en attente

Les demandes **Stop and Recall** en attente pour lesquelles les clients **Case Management** doivent fournir une réponse, conformément aux règles métier définies dans le **Stop and Recall for Case Management Rulebook**, sont affichées dans le tableau de résultats correspondant.

<img width="629" height="477" alt="image" src="https://github.com/user-attachments/assets/9dc2465c-2b04-4008-951c-6fad0ada1b36" />

## 3.5 Vue de la transaction

La **vue de la transaction** du Basic Tracker affiche les détails d’une transaction. Elle présente le **statut le plus récent** de la transaction.

<img width="629" height="373" alt="image" src="https://github.com/user-attachments/assets/7ffa64b6-5a37-49cc-a03b-b7a61bfdfaf3" />

### Transaction Copy

Les utilisateurs du Basic Tracker peuvent voir un nouveau bouton **Transaction Copy**.

Lorsque ce bouton est affiché, cela signifie que la transaction, identifiée par son **UETR**, existe dans **Transaction Manager**.

Pour plus d’informations, voir la section **Opérations manuelles dans la GUI - Vue Transaction Copy**.

---

## En-tête de la transaction

Les informations génériques suivantes concernant la transaction sont disponibles en haut de l’écran.

<img width="629" height="36" alt="image" src="https://github.com/user-attachments/assets/05a3207d-6a00-401d-bc19-71ab76a3c3d8" />

### Dernier statut

Quatre valeurs sont possibles :

#### Completed

Les paiements **Completed** sont ceux dont le statut de transaction est **ACCC**, c’est-à-dire lorsque le compte du bénéficiaire a été crédité.

Les paiements terminés sont affichés en **vert**.

#### In progress

Les paiements **In progress** sont ceux pour lesquels le dernier statut reçu est :

- **ACSP/G000**, lorsque le paiement est transféré à l’intérieur de **FIN ou SwiftNet** ;
- **ACSP/G001**, lorsque le paiement est transféré en dehors de **FIN ou SwiftNet**.

Les paiements en cours sont affichés en **gris**.

#### On hold

Les paiements **On hold** sont ceux pour lesquels le dernier statut reçu est :

- **ACSP/G002**, lorsque le paiement ne peut pas être confirmé dans un délai de deux jours ouvrés ;
- **ACSP/G003**, lorsque votre banque est en attente de réception de documents ;
- **ACSP/G004**, lorsque votre banque est en attente de réception des fonds.

Les paiements en attente sont affichés en **orange**.

#### Rejected

Les paiements **Rejected** sont ceux dont le statut de transaction est **RJCT**.

Les paiements rejetés sont affichés en **rouge**.

Des informations supplémentaires sont fournies concernant le statut, notamment la **date et l’heure de la dernière mise à jour de la transaction**.

### Montant indiqué dans l’instruction

Le montant indiqué dans l’instruction provient du champ **Instructed Amount and Currency** du message **pacs.008**, ou du **champ 33B** du message **MT 103**.

### Numéro de suivi

Le numéro de suivi correspond à l’**UETR** transporté dans les messages ou les appels API qui constituent la transaction.

### Ligne de métro

La **metro line** est la représentation graphique du cheminement du paiement dans la transaction.

Elle utilise plusieurs éléments graphiques principaux.

### Formes

- Clients débiteurs : Les clients débiteurs sont représentés par des **carrés**.

<img width="308" height="161" alt="image" src="https://github.com/user-attachments/assets/0424ade4-1199-4e55-8ca8-9a4e7e5f5ca3" />

- Clients créanciers: Les clients créanciers sont également représentés par des **carrés**.

<img width="303" height="167" alt="image" src="https://github.com/user-attachments/assets/6c57586a-f6e5-4945-a184-e16f9046db3f" />

- Participants à la transaction : Les participants à la transaction sont représentés par des **cercles**.

<img width="299" height="571" alt="image" src="https://github.com/user-attachments/assets/5fe9ec50-b026-44e3-b069-09a771d66ff6" />

Chaque cercle contient des informations détaillées sur la banque qu’il représente.

**Remarque :** la boîte bancaire correspondant à votre propre entité contient le logo **Me** et intègre des informations supplémentaires qui ne figurent pas dans les boîtes bancaires des contreparties.

Si l’agent du débiteur et/ou l’agent du créancier n’ont pas été identifiés par un **BIC** dans le virement de crédit client reçu ou envoyé, les informations contenues dans les boîtes bancaires ne sont pas divulguées.

<img width="260" height="413" alt="image" src="https://github.com/user-attachments/assets/28a96bb9-9b07-443e-91b3-b8e6aec90dd7" /> <br>

<img width="260" height="403" alt="image" src="https://github.com/user-attachments/assets/c470880e-db1d-476b-8d30-8a27b2892ddc" />

- Les cercles et les carrés sont reliés par des lignes afin d’indiquer le **flux de paiement** dans la transaction.

<img width="605" height="269" alt="image" src="https://github.com/user-attachments/assets/c9d22394-d3a3-41db-a061-fa5b7db37d32" />

### Couleurs de la ligne de métro

Les couleurs permettent de visualiser rapidement l’état du paiement.

- Gris : Le **gris** indique que la banque n’a pas encore reçu le paiement. Une confirmation de paiement est attendue dès que le paiement atteint la banque.

<img width="399" height="783" alt="image" src="https://github.com/user-attachments/assets/e95b8df3-d322-4e94-a736-088d60c8a49a" />

- Moitié verte / moitié grise : Une ligne de métro **moitié verte et moitié grise** indique que la banque a reçu le paiement et qu’elle doit le confirmer dans un délai de **deux jours ouvrés** afin de respecter le **Universal Confirmations Rulebook**.

<img width="386" height="726" alt="image" src="https://github.com/user-attachments/assets/295413ad-2602-44c4-b456-74a15628d630" />

- Vert : Le **vert** indique que la banque a reçu et confirmé le paiement. **Aucune action supplémentaire n’est requise.**

<img width="260" height="645" alt="image" src="https://github.com/user-attachments/assets/a570add7-da20-4698-a51f-819a3f30b87a" />

- Boîte du client bénéficiaire moitié verte / moitié grise : Une boîte du client bénéficiaire **moitié verte et moitié grise** indique que la banque du bénéficiaire a **partiellement crédité le client**. Le client n’a donc pas encore été crédité intégralement.

<img width="256" height="185" alt="image" src="https://github.com/user-attachments/assets/5a2d1fb4-b315-4c82-9f42-940780b6d9c3" />

- Vert avec une ligne rouge : Une ligne **verte avec une ligne rouge** indique que la banque a reçu le paiement et l’a **rejeté**.

<img width="264" height="281" alt="image" src="https://github.com/user-attachments/assets/91bbb5c1-ed4e-49e3-844c-fcc4ec7342f3" />

### Ligne pleine ou ligne en pointillés

- Une **ligne en pointillés** indique une incertitude concernant l’exécution du paiement.

<img width="605" height="178" alt="image" src="https://github.com/user-attachments/assets/e8adf12d-30e8-4750-bbf3-cf29a9ff45be" />

Une ligne verte en pointillés accompagnée de la mention : **undisclosed bank(s)** indique qu’il peut y avoir, ou non, une ou plusieurs banques impliquées dans la transaction à l’endroit où cette mention apparaît. Une ligne grise en pointillés indique que la chaîne de transaction n’est pas encore connue. Il peut donc y avoir, ou non, d’autres banques intermédiaires impliquées dans la transaction avant que le paiement n’atteigne la banque du bénéficiaire. 
Si le paiement est envoyé en dehors de **FIN**, la ligne en pointillés est accompagnée d’une **flèche en pointillés**.

<img width="605" height="113" alt="image" src="https://github.com/user-attachments/assets/0776a643-70e0-4fb5-b228-aca398dbf03c" />

- Une **ligne pleine** indique qu’il existe une certitude concernant la manière dont le paiement est exécuté.

<img width="605" height="84" alt="image" src="https://github.com/user-attachments/assets/aaa06a14-38fe-4582-8d1f-678ae3a1a93c" />

**Remarque :** Lorsqu’un utilisateur recherche une transaction dans laquelle sa banque n’est pas impliquée, aucune **metro line** n’est affichée. Seules des informations limitées sont affichées dans l’en-tête de la transaction :

- le dernier statut ;
- le numéro de suivi.

<img width="628" height="84" alt="image" src="https://github.com/user-attachments/assets/e74e3f91-cdd1-46ac-95ff-b49f43a8350b" />

# 3.6 Vue de la transaction avec flux de retour

Lorsqu’une transaction se trouve dans un **flux de retour**, la GUI du Basic Tracker affiche le virement de crédit client avec :

- le statut **In progress** ;
- l'indication **In return flow**.

Une **barre bleue** est affichée.

À gauche, elle indique :

> **A return has been initiated for the payment**

c’est-à-dire :

> **Un retour a été initié pour le paiement.**

À droite, un lien permet de sélectionner :

> **See the Return Flow**

pour afficher le flux de retour.

<img width="628" height="327" alt="image" src="https://github.com/user-attachments/assets/9d87cd4f-4cdb-4448-9d8d-c5c1b1f143b2" />

Si l’utilisateur possède dans son périmètre un **BIC participant au flux de retour**, la GUI du Basic Tracker présente le flux de retour complet à l’utilisateur.

Dans le cas contraire, l’utilisateur ne voit que la **vue publique du flux de retour**.

Cette vue publique affiche uniquement le statut :

**In progress**

pour l’UETR concerné.

---

## Présentation du flux de retour

Le flux de retour présente les agents de retour de gauche à droite :

**Return Originator → Return Creditor**

Une étiquette permet d’identifier les agents concernés.

Une barre bleue indique que l’utilisateur consulte actuellement le **Return Flow**.

À droite de cette barre, un lien permet de revenir à :

**See the Payment Flow**

c’est-à-dire la vue du flux de paiement initial.

---

## Ligne de métro du retour

La **metro line** du virement de crédit client retourné présente uniquement les **agents**.

Elle n’affiche pas de boîte pour :

- le client débiteur ;
- le client créancier.

Actuellement, le Basic Tracker ne prend pas en charge une confirmation **ACCC** pour l’agent du créancier du retour lorsqu’il recrédite le client final bénéficiaire du retour.

---

## Champs spécifiques au flux de retour

Les champs présents sur la ligne de métro du retour sont étiquetés afin d’indiquer clairement qu’ils correspondent au **flux de retour**.

Par exemple :

**Return Instructed amount**

correspond au **montant indiqué dans l’instruction de retour**.

Les mêmes règles de visibilité s’appliquent aux retours de virements de crédit client dans le flux aller. L’agent non-GPI a une visibilité sur le segment envoyé et sur celui reçu.

<img width="628" height="328" alt="image" src="https://github.com/user-attachments/assets/0099e61e-8b31-473e-a253-7e31d81ea435" />

## 3.7 Vue de la transaction avec un segment PMI

Pour les segments PMI sur Swift, le Tracker génère automatiquement des mises à jour de statut « En cours » (*In progress*) pour les PMI utilisant une topologie Y-Copy ou en V.

Le Tracker suit le trafic des PMI sur Swift, à condition que la PMI respecte les exigences minimales du Tracker.

Pour les PMI ISO utilisant une topologie Y-Copy, le Tracker génère automatiquement la mise à jour « En cours » à partir du message de paiement.

Lorsqu’une PMI Y-Copy ne parvient pas à traiter le paiement et renvoie un message d’interruption (*abort*) à l’expéditeur, soit un message MT 019 dans le cas de FIN, soit un message d’interruption xsys pour les PMI utilisant un service SwiftNet prenant en charge les messages ISO 20022, le Tracker enregistre ce message d’interruption comme une mise à jour de statut de rejet RJCT, avec le code de motif de rejet MS03.

Dans cette mise à jour, le BIC de la PMI est indiqué comme partie informatrice du Tracker (*Tracker Informing Party*), tandis que le BIC du Tracker est utilisé comme BIC de l’expéditeur et du destinataire du statut :

- TRCKCHZ0 dans l’environnement de Test et Formation ;
- TRCKCHZZ dans l’environnement de production (*Live*).

Pour les PMI sur Swift utilisant une topologie en V, lorsque la PMI respecte les exigences minimales de suivi, le Tracker suit les deux messages impliqués dans l’échange avec la PMI :

- du participant expéditeur vers la PMI ;
- de la PMI vers le participant destinataire.

Pour les PMI FIN utilisant une topologie en V, les BIC du participant expéditeur, de la PMI et du participant destinataire sont identifiés dans les en-têtes des messages Swift. Le Tracker peut ainsi utiliser ces informations d’en-tête pour identifier le premier segment, du participant expéditeur vers la PMI, ou le deuxième segment, de la PMI vers le participant destinataire.

Pour les PMI ISO utilisant une topologie en V, le Tracker génère automatiquement les mises à jour « En cours » à partir des messages de paiement envoyés sur Swift.

Les champs *Instructing Agent* et *Instructed Agent*, qui identifient respectivement les participants PMI expéditeur et destinataire, restent identiques dans le premier et/ou le deuxième segment.

Pour les PMI à topologie en V utilisant deux réseaux (*dual-network*), les participants peuvent échanger des messages avec la PMI en V via Swift ou via un autre réseau.

Des modifications ont été apportées au Tracker afin de permettre le suivi du segment PMI d’une PMI en V, même lorsque le Tracker n’est informé que d’un seul segment.

Dans le cas où un participant non-GPI envoie un segment PMI en V qui ne passe pas par Swift, il est recommandé à l’agent de fournir une mise à jour de statut « En cours » au Tracker pour ce segment.

La capture d’écran suivante présente un exemple de la manière dont les segments PMI sont affichés dans Basic Tracker.

<img width="628" height="272" alt="image" src="https://github.com/user-attachments/assets/518fa307-5434-418f-bc48-373cf233b9c6" />

Lorsqu’une PMI en V ne parvient pas à traiter le paiement et renvoie à l’expéditeur un message pacs.002 contenant un statut RJCT, le Tracker enregistre automatiquement cette mise à jour de statut de rejet.

## 3.8 Vue de la transaction avec un segment Network Interoperability

L’exemple suivant montre comment Basic Tracker présente une transaction comprenant une mise à jour de statut fournie par une infrastructure de marché de paiement (*Payment Market Infrastructure*, PMI) utilisant le service Network Interoperability.

<img width="628" height="340" alt="image" src="https://github.com/user-attachments/assets/7b7ecb40-e6f7-4991-8a59-926339a6f63d" />

Pour ces mises à jour effectuées au nom d’un autre établissement (*on-behalf-of updates*), une zone d’informations supplémentaire est affichée, comme indiqué dans la capture d’écran précédente. Elle précise l’établissement qui a fourni la mise à jour de statut.

L’exemple suivant montre comment une mise à jour effectuée au nom d’un autre établissement, fournie par un agent GPI utilisant le service Network Interoperability, est présentée à un client non-GPI dans Basic Tracker.

<img width="628" height="331" alt="image" src="https://github.com/user-attachments/assets/fac2b8ca-98e4-4375-a9c7-133ddeba60c7" />

## 3.9 Vue de la transaction avec des interruptions de messages

Swift a apporté une modification au Tracker afin de fournir des informations lorsqu’un message FIN ou FINplus suivi est interrompu par le service de messagerie.

Le Tracker prend déjà en charge la capture des événements de paiement liés aux messages interrompus par les infrastructures de marché de paiement (PMI), aussi bien pour FIN que pour les services SwiftNet Y-Copy. Il présente ces messages d’interruption sous forme de mises à jour de statut de rejet (RJCT) dans les transactions.

Lorsqu’un message de paiement FIN est interrompu, un message MT 019 est envoyé à l’expéditeur du message.

Lorsqu’un message de paiement FINplus est interrompu, un message système xsys.012 est envoyé à l’expéditeur du message.

Lorsque le Tracker est informé d’une interruption de message, il génère une mise à jour de statut RJCT. Cette mise à jour contient le code de motif de rejet MS03.

Dans l’interface graphique de Basic Tracker, la mise à jour de statut RJCT est affichée et la ligne de métro est représentée en gris à partir de l’expéditeur du message interrompu.

L’expéditeur d’un message interrompu peut :

- corriger et renvoyer le message ;
- réacheminer le message ;
- ou, lorsque cela est applicable, initier un retour de la transaction.

Le Tracker continue de suivre les messages ultérieurs liés à la transaction après le message interrompu, à condition que ces messages soient valides et contiennent le même UETR que celui de la transaction existante.

La capture d’écran suivante présente un exemple de la manière dont Basic Tracker affiche un message envoyé par l’agent du débiteur qui a été interrompu.

<img width="628" height="246" alt="image" src="https://github.com/user-attachments/assets/06fe46f4-8a64-4685-9098-9a19bf90b9bb" />

## 3.10 Vue de la transaction avec les opérations Stop and Recall

Les utilisateurs disposant de BIC Case Management définis dans le périmètre de leurs rôles RBAC FullViewer et/ou Update peuvent voir, dans la vue de la transaction, les demandes Stop and Recall (SRP) susceptibles d’avoir une incidence sur la transaction analysée.

Dans la vue de la transaction, les clients Case Management peuvent identifier :

- Si une demande SRP a été initiée pour la transaction.
- Les utilisateurs initiateur et destinataire de la demande SRP (*SRP initiator* et *SRP assignee*).
- Le dernier statut de la demande SRP.
- Le motif SRP indiqué par l’initiateur, ainsi que la réponse SRP, si le destinataire de la demande l’a déjà fournie.
- Si l’UETR de la transaction concernée par une demande SRP figure toujours dans la liste d’annulation du réseau (*network cancellation list*). Cette présence empêche la poursuite de la propagation de la transaction sur le réseau Swift jusqu’à ce qu’une réponse SRP définitive soit fournie par l’utilisateur destinataire de la demande.

La vue de la transaction Basic Tracker évolue pour refléter la progression de la demande SRP :

- Vue de la transaction Basic Tracker lorsqu’une demande SRP a été initiée.

<img width="605" height="381" alt="image" src="https://github.com/user-attachments/assets/cc03238a-9b82-4535-93c3-56236d57be51" />

- Vue de la transaction Basic Tracker lorsqu’une demande SRP a été attribuée et qu’une réponse est en attente.

<img width="605" height="382" alt="image" src="https://github.com/user-attachments/assets/0238326a-0111-4751-863b-4297c7d3bdb0" />

- Vue de la transaction Basic Tracker lorsqu’une demande SRP a été acceptée et que la transaction a été rejetée.

<img width="605" height="381" alt="image" src="https://github.com/user-attachments/assets/1054bfeb-9dc5-4153-8ba0-d8207b93c844" />

- Vue de la transaction Basic Tracker lorsqu’une demande SRP a été refusée et que la transaction a poursuivi sa propagation.

<img width="605" height="382" alt="image" src="https://github.com/user-attachments/assets/a40615c7-c672-4449-8e27-d34715fcea4b" />

## 3.11 Opérations manuelles dans l’interface graphique : mises à jour des paiements

Les utilisateurs doivent transmettre des confirmations au Tracker lorsque la réception d’un virement de crédit client (MT 103 ou pacs.008) entraîne le crédit du compte du bénéficiaire ou lorsqu’elle entraîne le rejet de l’instruction de paiement.

Une confirmation de crédit doit inclure :

- la date et l’heure auxquelles les fonds ont été crédités ;
- le montant et la devise crédités sur le compte du bénéficiaire ;
- l’initiateur du statut (*status originator*).

Une notification de rejet de paiement doit inclure la date et l’heure du rejet ainsi que le motif du rejet.

Lorsqu’un message de paiement est transmis à un autre établissement financier en dehors de Swift (FIN et/ou SwiftNet), au moyen d’un autre canal de paiement, Swift recommande à l’établissement financier ayant reçu le virement de crédit client (MT 103 ou pacs.008) de mettre à jour le Tracker avec les informations relatives à la transmission ultérieure du paiement.

La confirmation « En cours » (*In progress*) indique clairement qu’aucune autre mise à jour n’est attendue de la part de l’initiateur du statut. Elle fournit également davantage de détails sur le transfert, notamment le montant transféré.

Lorsqu’un paiement est en attente de traitement supplémentaire et qu’il n’est pas possible de le transférer ou de créditer le compte du bénéficiaire dans les deux jours suivant la date de valeur demandée dans l’instruction de paiement, Swift recommande d’envoyer une confirmation intermédiaire.

Lorsqu’une confirmation intermédiaire est envoyée, l’utilisateur reste tenu de fournir ultérieurement une confirmation définitive, dès que possible.

Des confirmations peuvent également être fournies, de manière facultative, pour les instructions de paiement reçues en dehors de Swift qui contiennent un identifiant unique de transaction de bout en bout (UETR), par exemple pour suivre les paiements acheminés via des infrastructures de marché compatibles GPI.

**Remarque :** aucune confirmation ne doit être envoyée au Tracker pour les segments de retour. Si de telles confirmations sont fournies, elles sont invalidées.

### Mettre à jour un paiement

Chaque fois qu’un paiement atteint la banque de l’utilisateur, le cercle situé au-dessus des informations de sa banque apparaît à moitié vert et à moitié gris.

Cela indique que l’utilisateur doit confirmer le paiement conformément aux règles du *Universal Confirmations Rulebook*.

<img width="263" height="491" alt="image" src="https://github.com/user-attachments/assets/32448f6c-71be-4ed3-b422-a1991a14239f" />

Un paiement peut être mis à jour avec quatre statuts différents.

### J’ai crédité le paiement (*I credited the payment*)

Lorsque le client bénéficiaire a été crédité après réception d’un virement de crédit client (MT 103 sur FIN ou pacs.008 sur SwiftNet), les utilisateurs doivent mettre à jour le statut du paiement en sélectionnant « J’ai crédité le paiement ».

Le code de statut ISO 20022 ACCC (*Accepted Settlement Completed*) indique que le règlement sur le compte du client bénéficiaire a été effectué.

<img width="628" height="149" alt="image" src="https://github.com/user-attachments/assets/51a5fb1e-2921-4c36-9dba-7be74d4a0ab2" />

- L’utilisateur ne peut pas modifier le champ *Received amount* (montant reçu).
- Le champ *My deducts* (mes déductions) est défini à zéro par défaut. Le champ *Credited amount* (montant crédité) reprend par défaut le montant reçu.
- Si l’utilisateur modifie le montant des déductions, le montant crédité est automatiquement mis à jour.
- Si l’utilisateur modifie le montant crédité sans modifier les déductions, un message d’avertissement s’affiche et il ne peut pas cliquer sur « Confirm status update » (Confirmer la mise à jour du statut).
- Si l’utilisateur modifie la devise du montant crédité, ce montant est ramené à zéro et le champ du taux de change devient facultatif.
- Si le montant crédité est supérieur au montant reçu, un message d’erreur s’affiche et l’utilisateur ne peut pas cliquer sur « Confirm status update ».
- Si le code devise des déductions ou du montant est incorrect, un message d’erreur s’affiche et l’utilisateur ne peut pas cliquer sur « Confirm status update ».
- La valeur par défaut du champ *Funds available on* (Date de disponibilité des fonds) correspond à la date et à l’heure locales auxquelles l’utilisateur a cliqué sur « Update payment status » (Mettre à jour le statut du paiement). L’utilisateur peut modifier cette date et cette heure.

### J’ai transféré le paiement (*I transferred the payment*)

Lorsque le destinataire du virement de crédit client est un intermédiaire et qu’il ne transmet pas le paiement au participant suivant via Swift (MT 103 sur FIN ou pacs.008 sur SwiftNet), Swift recommande aux utilisateurs de mettre à jour le statut du paiement en sélectionnant « J’ai transféré le paiement ».

<img width="628" height="188" alt="image" src="https://github.com/user-attachments/assets/088656f2-d37e-4bbc-91bb-dca6ff450808" />

Le code de statut ISO 20022 ACSP (*Settlement in Progress*) indique que la transaction nécessite encore un traitement supplémentaire avant de pouvoir être considérée comme terminée.

Pour un paiement transféré en dehors de FIN, cela signifie que l’initiateur du statut n’a plus d’obligations de mise à jour.

Règles de saisie :

- Les champs relatifs à *My deducts* et *Transferred amount* (montant transféré) fonctionnent de la même manière que dans l’option précédente, sauf lorsque l’utilisateur modifie la devise du montant transféré.
- Le champ *Deducts code* (code des déductions) permet à l’utilisateur de sélectionner l’une des valeurs suivantes :
  - BEN/CRED ;
  - OUR/DEBT ;
  - SHA/SHAR.
- Pour permettre le suivi des segments non-FIN d’une transaction, l’utilisateur peut indiquer le BIC de l’agent destinataire du transfert dans le champ *Transferred to* (Transféré à).
- Le champ *Settlement method* (méthode de règlement) permet de sélectionner la méthode de règlement. Si CLRG est sélectionné, le champ *Clearing system* (système de compensation) apparaît.

**Remarque :** lorsque le destinataire du virement de crédit client agit comme intermédiaire et que le paiement est transmis à l’étape suivante en dehors de Swift, c’est-à-dire sans utiliser FIN ou SwiftNet, il n’est pas nécessaire de générer une mise à jour de statut Tracker si une banque ultérieure dans la chaîne l’a déjà fait dans un délai de deux jours ouvrables.

Dans le contexte de Swift Go, le client peut sélectionner l’identifiant de type de service 009 pour fournir une mise à jour de statut Swift Go, ou ne sélectionner aucun identifiant de type de service si le transfert du paiement n’est pas éligible à Swift Go.

Par exemple, l’agent destinataire du transfert n’est pas un client Swift Go.

Cette option est activée et visible uniquement lorsque les conditions suivantes sont réunies :

- Le client est abonné à Swift Go et dispose du provisionnement nécessaire.
- Le paiement reçu respecte les règles Swift Go. Par exemple, le montant reçu est inférieur au seuil maximal autorisé pour la devise concernée. Pour plus d’informations, consulter le *Swift Go Rulebook*.

Ce filtrage préalable des paiements a été mis en place pour aider le client à effectuer des paiements selon le principe du traitement direct (*Straight-Through Processing*, STP).

Si l’utilisateur sélectionne l’identifiant de type de service 009 :

- Le code des déductions (*Deducts code*) est verrouillé sur SHA/SHAR.
- Le champ *My deducts* est verrouillé à 0,00.
- Le champ *Clearing system* devient obligatoire.
- Le champ *Transferred to* devient obligatoire.

### J’ai mis le paiement en attente (*I put the payment on hold*)

Lorsque le destinataire du virement de crédit client (MT 103 ou pacs.008) ne peut pas envoyer de confirmation définitive dans le délai requis, Swift recommande de fournir dès que possible une confirmation intermédiaire en sélectionnant le statut « J’ai mis le paiement en attente ».

Une confirmation définitive est ensuite attendue de la part des utilisateurs dès que possible.

Cette confirmation intermédiaire peut également être utilisée lorsque l’établissement intermédiaire qui reçoit le virement de crédit client ne peut pas envoyer un message de paiement vers l’établissement suivant dans le délai requis.

Le code de statut ISO 20022 ACSP (*Settlement in Progress*) doit être utilisé pour indiquer que la transaction est toujours en attente.

<img width="628" height="139" alt="image" src="https://github.com/user-attachments/assets/3fe01b7f-fcc8-4d69-8552-9de963aa99d6" />

L’utilisateur peut sélectionner l’une des trois valeurs proposées dans le panneau de mise à jour.

### J’ai rejeté le paiement (*I rejected the payment*)

Lorsque le destinataire du virement de crédit client (MT 103 ou pacs.008) ne peut pas traiter le paiement et rejette donc l’instruction, les utilisateurs doivent mettre à jour le statut du paiement en sélectionnant « J’ai rejeté le paiement ».

Le code de statut ISO 20022 RJCT (*Rejected*) indique que la transaction a été rejetée.

Cette confirmation doit toujours être fournie lorsqu’un virement de crédit client est rejeté, quel que soit le rôle de l’initiateur du rejet dans la transaction.

<img width="628" height="139" alt="image" src="https://github.com/user-attachments/assets/8211e95c-bdee-4c4c-9d47-5d5e025aaca7" />

L’utilisateur peut sélectionner l’une des valeurs proposées dans la liste déroulante du panneau de mise à jour.

Lorsque l’utilisateur clique sur « Confirm status update » (Confirmer la mise à jour du statut), le panneau se ferme et une notification de confirmation s’affiche.

### Approuver ou rejeter une opération

Le panneau d’approbation présente tous les détails qui ont été renseignés dans le panneau de mise à jour du paiement.

<img width="628" height="110" alt="image" src="https://github.com/user-attachments/assets/bf726d81-67cc-4462-becd-995052ce367e" />

Pour approuver ou rejeter une opération selon le principe du contrôle à quatre yeux (*4-eyes approval*), un utilisateur doit initier l’action et un autre utilisateur doit l’approuver.

Si l’approbation ou le rejet selon le principe du contrôle à quatre yeux est désactivé, toutes les opérations en attente d’approbation ou de rejet avant la désactivation de cette fonctionnalité restent soumises à cette exigence de double validation.

## 3.12 Opérations manuelles dans l’interface graphique : demandes Stop and Recall

Les utilisateurs disposant de BIC Case Management définis dans le périmètre de leur rôle RBAC Update doivent respecter les règles métier Stop and Recall (SRP) définies dans le *Stop and Recall for Case Management Rulebook*.

Les agents destinataires d’une demande SRP (*SRP assignee agents*) doivent fournir une réponse au plus tard à la fin du jour ouvrable suivant.

Cette réponse doit, au minimum, être une réponse indiquant que la demande est en attente (*pending*).

Si la première réponse à la demande SRP est définie comme étant en attente, l’agent destinataire de la demande doit fournir une deuxième réponse dans un délai maximal de 10 jours calendaires à compter de la réception de la demande SRP.

Cette deuxième réponse peut être :

- une réponse définitive, indiquant que la demande SRP a été acceptée ou refusée par l’agent destinataire ;
- ou une nouvelle réponse indiquant que la demande est toujours en attente, si les 10 jours calendaires n’ont pas été suffisants pour permettre à l’agent destinataire de clôturer la demande.

### Initier une demande Stop and Recall

Lorsqu’un paiement a été initié ou relayé par erreur, avec des informations incorrectes ou de manière frauduleuse, un client Case Management disposant du rôle RBAC Update peut voir apparaître le bouton « Initiate Stop and Recall » (Initier une demande Stop and Recall).

<img width="628" height="395" alt="image" src="https://github.com/user-attachments/assets/a232c2f4-6ffd-4fc2-a668-14e7be6a7b2d" />

La sélection d’un motif Stop and Recall est obligatoire avant de cliquer sur « Initiate Stop and Recall ».

L’accord d’indemnisation (*Indemnity agreement*, INDM) est défini sur « No » (Non) par défaut.

La fenêtre d’initiation d’une demande Stop and Recall apparaît uniquement si le Tracker peut identifier d’autres agents de transaction, GPI ou non-GPI, actifs sur le service SRP.

Plus précisément, si la vérification préalable de l’utilisateur destinataire de la demande SRP (*SRP assignee user pre-check*) est négative, c’est-à-dire si le Tracker ne peut identifier aucun participant à la transaction actif sur SRP après l’initiateur de la demande SRP, un avertissement FRNA est affiché.

### Répondre à une demande Stop and Recall

Les clients Case Management disposant du rôle RBAC Update et identifiés par le Tracker comme agents destinataires d’une demande SRP (*SRP assignee agents*) doivent répondre à cette demande dans le délai défini dans le *Stop and Recall for Case Management Rulebook*.

<img width="628" height="430" alt="image" src="https://github.com/user-attachments/assets/8b0eee79-cb47-4ba0-84a7-b89e81171a45" />

## 3.13 Opérations manuelles dans l’interface graphique : fonctionnalité Rich Data Access

Cette fonctionnalité vise à proposer une alternative cohérente et plus efficace au processus bilatéral de demande d’informations (*Request for Information*, RFI), décrit dans le document *CBPR+ Data Integrity Market Practice Guidance*.

Elle permet de supprimer la dépendance vis-à-vis de l’intermédiaire précédent et, par conséquent, d’accélérer le traitement des investigations.

### Initier une demande Rich Data Access

Les utilisateurs Swift SUPE ou PSPA disposant du rôle RBAC Update, qui ont reçu ou envoyé un virement de crédit client historique au format MT dans le cadre d’une transaction initialement initiée sous forme de paiement pacs.008 échangé sur FINplus, peuvent voir le bouton « Initiate rich data case » (Initier un dossier de données enrichies) sur l’écran des détails de la transaction dans l’interface Basic Tracker.

<img width="628" height="379" alt="image" src="https://github.com/user-attachments/assets/fc4d67f6-1f41-4471-9dd7-21c7be2a010f" />

Après avoir cliqué sur « Initiate rich data case », le panneau d’initiation du dossier s’ouvre.

<img width="605" height="416" alt="image" src="https://github.com/user-attachments/assets/b1092d86-57f6-4468-9b23-66da01a0e801" />

- Si le BIC inclus dans le périmètre du rôle RBAC Update de l’utilisateur est abonné à Case Management, l’utilisateur doit sélectionner le code motif de dossier RICH dans la liste déroulante.
- Dans le cas contraire, le Tracker préremplit tous les champs avec les valeurs par défaut appropriées.

**Remarque :** le processus d’approbation à quatre yeux (*4-eyes approval*) ne s’applique pas à la création d’un dossier RICH.

Plus précisément, si le BIC inclus dans le périmètre du rôle RBAC Update est configuré avec un dispositif de validation à quatre yeux, l’initiation d’un dossier RICH ne déclenche pas ce processus d’approbation. Le dossier RICH est créé directement.

Dès que le dossier RICH est initié, Basic Tracker le clôture automatiquement et fournit, en réponse, un lien vers les éléments de données enrichies.

<img width="628" height="432" alt="image" src="https://github.com/user-attachments/assets/0f58ffd0-4397-4847-a71e-aad79db70de0" />

### Consulter les éléments de données enrichies

Le dossier apparaît alors dans l’écran « Cases in transaction » (Dossiers de la transaction) de l’interface Tracker.

Les utilisateurs disposant du rôle RBAC TMTransactionViewer, associé au rôle RBAC FullViewer et/ou Update, peuvent cliquer sur le lien des données enrichies pour consulter ces éléments.

L’écran propose également une option permettant de copier et d’exporter les données, par exemple pour alimenter une application locale de filtrage (*screening application*).

<img width="628" height="354" alt="image" src="https://github.com/user-attachments/assets/e3575e4e-74ac-4193-ac7b-4d950f5e1a09" />

## 3.14 Opérations manuelles dans l’interface graphique : vue Transaction Copy

L’interface graphique Basic Tracker fournit aux clients non-GPI appartenant à la catégorie d’utilisateurs SUPE de nouvelles fonctionnalités destinées à faciliter l’adoption du traitement des paiements par Transaction Manager.

Transaction Manager stocke et conserve une copie de chaque transaction (*Transaction Copy*), identifiée par son UETR, aussi bien pour les virements de crédit client que pour les transferts entre institutions financières.

La Transaction Copy contient les données disponibles pour une transaction donnée, notamment son statut tout au long de son cycle de vie.

Pour plus d’informations sur la Transaction Copy, consulter le document *Transaction Manager Service Description*.

L’interface Basic Tracker offre deux possibilités pour consulter la Transaction Copy associée à un UETR :

1. Une action accessible depuis la vue d’une transaction dans l’interface Basic Tracker.
2. Une fonction de recherche dédiée à la Transaction Copy.

Lorsqu’un utilisateur consulte la ligne de métro d’une transaction de paiement dans Basic Tracker, si cette transaction existe également dans Transaction Manager, une nouvelle option « Transaction Copy » apparaît.

Si l’utilisateur dispose d’un BIC dans son périmètre autorisé qui peut consulter cette Transaction Copy, en fonction du rôle de ce BIC participant à la transaction, soit en tant que détenteur actuel du paiement, soit en tant qu’agent précédent, l’option « Transaction Copy » apparaît en bleu et peut être sélectionnée.

Si la transaction existe dans Transaction Manager, mais qu’aucun des BIC du périmètre de l’utilisateur n’est autorisé à la consulter, l’option « Transaction Copy » apparaît en gris et ne peut pas être sélectionnée.

<img width="628" height="335" alt="image" src="https://github.com/user-attachments/assets/deb779a2-7294-40ad-b045-5364457c844c" />

Lorsque l’utilisateur clique sur « Transaction Copy », Basic Tracker vérifie d’abord si l’utilisateur dispose de plusieurs BIC dans le périmètre de son rôle RBAC TMTransactionViewer et si un ou plusieurs de ces BIC figurent également dans la transaction Basic Tracker.

---

Les BIC inclus dans le périmètre de TMTransactionViewer correspondent à ceux des rôles RBAC suivants :

- FullViewer ;
- TransactionViewer ;
- Update ;
- TransactionUpdate.

Le rôle TMTransactionViewer ne possède pas son propre périmètre de BIC.

---

Si l’utilisateur est autorisé pour plusieurs BIC dans son périmètre, mais qu’un seul de ces BIC figure également dans la transaction Basic Tracker, Basic Tracker demande les détails de la Transaction Copy à Transaction Manager en utilisant :

- l’UETR de la transaction ;
- le BIC concerné ;
- le type de transaction correspondant à la transaction Basic Tracker, à savoir un virement de crédit client.

Si l’utilisateur est autorisé pour plusieurs BIC dans son périmètre et que plusieurs de ces BIC figurent également dans la transaction Basic Tracker, l’interface lui demande de sélectionner le BIC qu’il souhaite utiliser pour interroger Transaction Manager au sujet de la Transaction Copy.

<img width="329" height="158" alt="image" src="https://github.com/user-attachments/assets/a9d29c53-cc4b-4e36-9f3b-2b506cf83fc0" />

Une fois le BIC sélectionné, Basic Tracker demande les détails de la Transaction Copy selon le processus décrit précédemment.

L’interface Basic Tracker affiche les données de la transaction dans une section récapitulative contenant :

- l’UETR ;
- l’état de la transaction ;
- la date et l’heure de création ;
- la date et l’heure de la dernière mise à jour.

La section *Payment Initiation* de la Transaction Copy et les flux de la transaction sont affichés dans des onglets distincts.

- **Détails de l’initiation du paiement (*Payment Initiation*) :** informations relatives aux parties, notamment *Ultimate Debtor*, *Debtor*, *Ultimate Creditor*, *Creditor Party Details* et *Instructed Details* (montant et taux de change).
- **Flux principal (*Principal Flow*) :** état du flux et participant actuel, suivis des informations relatives à l’initiation de la compensation (*Clearing Initiation*), aux segments de règlement (*Settlement Legs*), aux confirmations de crédit (*Credit Confirmation*) et à la liste des participants du flux principal.
- **Flux de couverture (*Cover Flow*), lorsqu’il est applicable :** état du flux et participant actuel, suivis de l’agent initiateur (*Initiating Agent*), des segments de règlement, des confirmations de crédit et de la liste des participants du flux de couverture.

**Remarque :** lors de la consultation de la Transaction Copy, les BIC affichés sont toujours des BIC de production (*Live BICs*).

En revanche, lorsque le paiement est consulté dans Basic Tracker en environnement Test et Formation, les BIC correspondant aux mêmes parties sur la ligne de métro du Tracker sont représentés par des BIC de test (BIC0).

L’utilisateur peut naviguer dans les détails de la Transaction Copy en développant ou en réduisant les différentes sections. Il peut également revenir à la vue de la ligne de métro de Basic Tracker.

### Transaction Copy : onglet Payment Initiation

**Remarque :** l’exemple de Transaction Copy présenté dans le guide concerne un virement de crédit client qui ne fait pas partie d’une transaction contenant un flux de couverture. Par conséquent, l’onglet relatif au flux de couverture n’est pas affiché.

<img width="628" height="352" alt="image" src="https://github.com/user-attachments/assets/791b7f96-3f4c-4651-b4ee-384ade14e589" />

### Transaction Copy : flux principal (Principal Flow)

<img width="628" height="352" alt="image" src="https://github.com/user-attachments/assets/353b5c79-ee58-48a2-8eaa-2c7a5f67fa23" />

### Option d’exportation PDF

L’interface Basic Tracker propose une option « Export PDF » permettant à l’utilisateur d’exporter les détails de la Transaction Copy au format PDF.

<img width="628" height="644" alt="image" src="https://github.com/user-attachments/assets/5edb34d4-e616-4556-a626-f31ed7967617" />

## 3.15 Opérations manuelles dans l’interface graphique : recherche Transaction Copy

Afin de permettre aux utilisateurs de Basic Tracker d’interroger la Transaction Copy lorsqu’ils ne peuvent pas consulter la ligne de métro de la transaction Tracker correspondante, Basic Tracker leur propose une autre méthode d’accès à la Transaction Copy.

Cette fonctionnalité permet aux utilisateurs d’interroger la Transaction Copy pour les transferts entre institutions financières, même si les utilisateurs de Basic Tracker n’ont pas accès aux transactions du service Swift GPI Financial Institution Transfer Tracker.

Sur la page d’accueil de Basic Tracker, un nouveau lien est affiché pour permettre à l’utilisateur d’accéder à l’écran de recherche Transaction Copy (**Transaction Copy search**).

<img width="628" height="296" alt="image" src="https://github.com/user-attachments/assets/f43e3bf6-b1b2-4bf0-b9fe-15d442e0d60f" />

Ce lien redirige l’utilisateur vers l’écran de recherche Transaction Copy (**Transaction Copy search**).

<img width="628" height="206" alt="image" src="https://github.com/user-attachments/assets/d6df08dd-39ba-42af-b7d7-a1e9261c8d82" />

L’utilisateur doit :

- fournir l’UETR de la transaction ;
- sélectionner dans la liste déroulante le BIC de son périmètre qui participe à la transaction ;
- sélectionner le type de transaction dans la liste déroulante : *Financial Institution Transfer* (transfert entre institutions financières) ou *Customer Credit Transfer* (virement de crédit client).

Lorsque l’utilisateur clique sur « Search » (Rechercher), la requête est directement transmise à Transaction Manager avec les informations fournies.

Si aucune transaction ne peut être trouvée à partir des informations fournies, ou si elle ne peut pas être affichée parce que le BIC indiqué ne dispose d’aucun droit de visibilité sur cette transaction, l’interface Basic Tracker informe l’utilisateur par le message suivant :

« Transaction does not exist or cannot be displayed for this UETR. »

Traduction : « La transaction n’existe pas ou ne peut pas être affichée pour cet UETR. »

Si la transaction est trouvée, la Transaction Copy est affichée selon le fonctionnement décrit dans la section « Opérations manuelles dans l’interface graphique : vue Transaction Copy », à la page 55.

Toutefois, dans ce cas, l’option « Back » (Retour) redirige l’utilisateur vers l’écran de recherche Transaction Copy.

## 3.16 Score Universal Confirmations

### Calcul du score Universal Confirmations

Le score Universal Confirmations est calculé selon les règles suivantes :

- Les transactions individuelles (messages MT 103 et/ou pacs.008) sont évaluées et agrégées chaque semaine au niveau du BIC à 8 caractères. Cela signifie que les flux non-FIN (MT 199 ou appels API) sont exclus des mesures du score Universal Confirmations.
- Tous les destinataires de virements de crédit client (messages MT 103 et/ou pacs.008) sont évalués pour leurs rôles d’intermédiaire et de bénéficiaire.
- Tout statut envoyé dans un délai de deux jours ouvrables donne lieu à un résultat positif pour le score Universal Confirmations. Les statuts concernés sont : ACCC, ACSP/G000, ACSP/G001, ACSP/G002, ACSP/G003, ACSP/G004 ou RJCT.

Les flux suivants sont exclus du calcul du score Universal Confirmations :

- Les virements de crédit client (messages MT 103 ou pacs.008) invalidés par le Tracker, par exemple lorsqu’un intermédiaire met à jour le montant instruit (*Instructed Amount*, champ 33B).
- Lorsque le destinataire du virement de crédit client agit en tant qu’intermédiaire et que le paiement est transmis à l’étape suivante en dehors de Swift, sans utiliser FIN ou SwiftNet, aucune mise à jour de statut Tracker n’est exigée du destinataire initial si une banque ultérieure dans la chaîne a déjà mis à jour le statut du paiement dans un délai de deux jours ouvrables.
- Les infrastructures de marché utilisant une topologie en V.
- Les flux de retour.

Le score Universal Confirmations calcule le rapport entre :

- le nombre de virements de crédit client (messages MT 103 ou pacs.008) confirmés dans un délai de deux jours ouvrables ;
- et le nombre de virements de crédit client (messages MT 103 ou pacs.008) reçus au cours d’une période de 10 jours observés.

La mesure du respect du seuil défini par le *Universal Confirmations Rulebook* repose sur les mises à jour Tracker effectuées dans un délai de deux jours ouvrables, à compter de la date de valeur, pour tous les virements de crédit client reçus (messages MT 103 ou pacs.008).

Cette règle s’applique également au cas où le destinataire transfère le paiement en dehors de Swift, c’est-à-dire sans utiliser FIN ou SwiftNet.

Le score Universal Confirmations est calculé et actualisé chaque semaine.

### Définition de la conformité au score Universal Confirmations

Swift considère que les institutions financières respectent le *Universal Confirmations Rulebook* lorsqu’elles ont confirmé au moins 80 % de leurs virements de crédit client entrants (messages MT 103 ou pacs.008) en moins de deux jours ouvrables.

Plus précisément :

- Si une institution financière met à jour plus de 80 % de ses virements de crédit client en attente (messages MT 103 ou pacs.008), contenus dans les transactions initiées au cours de la semaine évaluée, en moins de deux jours ouvrables, elle dépasse le seuil requis. Elle est alors considérée comme conforme aux règles métier Universal Confirmations et son score apparaît en vert.

- Si une institution financière ne met pas à jour au moins 80 % de ses virements de crédit client en attente (messages MT 103 ou pacs.008), contenus dans les transactions initiées au cours de la semaine évaluée, en moins de deux jours ouvrables, elle se situe sous le seuil requis. Elle est alors considérée comme non conforme aux règles métier Universal Confirmations.

Dès qu’une institution financière passe sous le seuil, elle entre dans une période d’amélioration de 12 semaines.

Pendant cette période d’amélioration, le score de l’établissement apparaît en orange.

Si une institution financière ne met pas à jour au moins 80 % de ses virements de crédit client en attente (messages MT 103 ou pacs.008), contenus dans les transactions initiées au cours de la semaine évaluée, en moins de deux jours ouvrables, et ce pendant plus de 12 semaines consécutives comportant du trafic de virements de crédit client, elle se situe sous le seuil requis et sa période d’amélioration est terminée.

Elle est alors considérée comme non conforme aux règles métier Universal Confirmations et son score apparaît en rouge.

La fonctionnalité de score Universal Confirmations met également en évidence le nombre de semaines consécutives pendant lesquelles une institution financière a conservé un statut donné :

- Conforme : vert.
- Non conforme pendant la période d’amélioration : orange.
- Non conforme après la période d’amélioration : rouge.

La mesure est calculée chaque semaine pour les messages contenus dans les transactions initiées au cours d’une semaine donnée. Elle est ensuite affichée dans Basic Tracker après un délai de 10 jours.

Les institutions financières dont le score reste orange (non conforme) pendant 12 semaines consécutives passent au rouge dans Basic Tracker Observer et perdent l’accès aux fonctionnalités de suivi, par exemple la recherche du statut des paiements sortants.

**Remarque :** toute semaine durant laquelle aucun virement de crédit client (message MT 103 ou pacs.008) n’a été reçu est ignorée dans le calcul du score Universal Confirmations de cette semaine. L’institution financière conserve alors le score précédemment calculé.

Enfin, le statut de conformité Universal Confirmations (conforme, en vert, ou non conforme après la période d’amélioration, en rouge), ainsi que le nombre de semaines pendant lesquelles une banque a été conforme (vert) ou non conforme (rouge), sont visibles par le reste de la communauté.

### Calendrier du score Universal Confirmations

- **À partir du 1er juin 2021 :** le statut de conformité Universal Confirmations des institutions financières devient visible par l’ensemble de la communauté. Le nombre de semaines de conformité ou de non-conformité est également visible par la communauté.

**Remarque :** le score orange est uniquement visible dans la vue des performances propres à l’établissement (*own performance*). Lorsqu’il est disponible, le reste de la communauté continue de voir ce score en vert.

### Exemples du score Universal Confirmations

Le score Universal Confirmations est affiché à deux endroits dans Basic Tracker :

- Sur la page d’accueil, afin de permettre aux institutions financières de vérifier rapidement si elles respectent les règles métier définies dans le *Universal Confirmations Rulebook*.
- Sur un écran dédié, qui fournit des informations supplémentaires sur le niveau de respect ou de non-respect du programme Universal Confirmations par l’institution financière.

Les cinq cas d’utilisation suivants illustrent le fonctionnement de cette fonctionnalité dans Basic Tracker.

**Exemple 1 : l’institution financière respecte les règles métier Universal Confirmations.**

Les informations sont présentées :

- sur la page d’accueil ;

<img width="581" height="389" alt="image" src="https://github.com/user-attachments/assets/b60fb610-e8c4-4f83-9c48-dc18c1d6e5ee" />

- sur l’écran Universal Confirmations.

<img width="581" height="389" alt="image" src="https://github.com/user-attachments/assets/80c1430d-7ea8-4fc4-bf4e-1f94d0e6841d" />

**Exemple 2 : l’institution financière ne respecte pas les règles métier Universal Confirmations et entre dans sa période d’amélioration de 12 semaines, avec du trafic de virements de crédit client.**

Les informations sont présentées :

- sur la page d’accueil ;

<img width="581" height="389" alt="image" src="https://github.com/user-attachments/assets/a4322d06-d0ea-445d-9f42-2cb1a1182bf9" />

- sur l’écran Universal Confirmations.

<img width="581" height="389" alt="image" src="https://github.com/user-attachments/assets/f3e6248f-85b3-42d1-b49a-800161db3dbc" />

**Exemple 3 : l’institution financière ne respecte pas les règles métier Universal Confirmations pendant plus de 12 semaines consécutives comportant du trafic de virements de crédit client et a perdu l’accès à ses fonctionnalités de suivi.**

Les informations sont présentées :

- sur la page d’accueil ;

<img width="581" height="390" alt="image" src="https://github.com/user-attachments/assets/b4cb3a7b-4b77-410f-8346-a8aa2d16b428" />

- sur l’écran Universal Confirmations.

<img width="581" height="389" alt="image" src="https://github.com/user-attachments/assets/b303c605-e5b8-410f-90fd-d98a90fd5a9d" />

**Exemple 4 : l’utilisateur possède plusieurs BIC non-GPI dans son périmètre. Certains BIC sont conformes, tandis que d’autres ne le sont pas.**

Lorsque l’utilisateur dispose de plusieurs BIC non-GPI dans son périmètre, l’écran Universal Confirmations affiche une liste déroulante.

Le score Universal Confirmations affiché dans l’indicateur circulaire est automatiquement actualisé en fonction du BIC sélectionné dans cette liste.

**Remarque :** un utilisateur est considéré comme non conforme et perd par conséquent l’accès aux fonctionnalités de recherche dès qu’un seul des BIC non-GPI associés à son périmètre passe au rouge.

- sur la page d’accueil ;

<img width="581" height="148" alt="image" src="https://github.com/user-attachments/assets/15b42203-18f9-483e-91a4-0b95965a9d3b" />

- sur l’écran Universal Confirmations avec multiple BICs dans le périmtre :

<img width="581" height="208" alt="image" src="https://github.com/user-attachments/assets/f79c5053-c483-4e2d-912c-e6d034b884e7" /> <br>

<img width="581" height="255" alt="image" src="https://github.com/user-attachments/assets/a48ba27a-7db3-4389-8c84-1e103f6e7097" /> <br>

<img width="581" height="256" alt="image" src="https://github.com/user-attachments/assets/a8f9d110-7b0f-4a91-95a8-3cc71bf00a9b" />

**Exemple 5 : aucun score n’est disponible pour l’institution financière.**

Ce cas peut se présenter lorsque l’institution financière a uniquement envoyé des virements de crédit client, sans en avoir reçu, et/ou lorsqu’elle est une infrastructure de marché de paiement utilisant une topologie en V.

Les informations correspondantes sont présentées :

- sur la page d’accueil ;

<img width="581" height="390" alt="image" src="https://github.com/user-attachments/assets/482c5f1c-10b0-4656-a05a-d903763e9631" />

- sur l’écran Universal Confirmations.

<img width="581" height="390" alt="image" src="https://github.com/user-attachments/assets/350d493d-4305-4f7c-9132-25075005e5db" />

## 3.17 Statut de conformité Universal Confirmations des autres banques

Un nouvel onglet a été introduit afin de permettre aux utilisateurs respectant les règles métier Universal Confirmations de rechercher et d’analyser le statut de conformité d’autres entités, GPI ou non-GPI. Cet onglet permet de consulter le statut de conformité des autres établissements, qui peut être vert ou rouge.

**Remarque :** l’onglet de conformité des autres banques (*Other bank's compliance*) est uniquement accessible aux utilisateurs qui respectent les règles métier Universal Confirmations. Dès qu’un BIC du périmètre de l’utilisateur passe au rouge, cet onglet est désactivé.

<img width="628" height="305" alt="image" src="https://github.com/user-attachments/assets/e201e755-f512-4dbb-9b0b-a878a605c1cc" /> <br>

<img width="628" height="341" alt="image" src="https://github.com/user-attachments/assets/cbc79e2e-b0a6-480e-aba0-62fa9e961fae" />

Le nouvel onglet permet aux utilisateurs de rechercher une autre banque à partir de l’un des critères suivants : son BIC, son nom, son pays, sa ville.

<img width="628" height="333" alt="image" src="https://github.com/user-attachments/assets/4c5fd9d2-2410-4687-8d74-9671610160f8" />

Les résultats de la recherche apparaissent dans un tableau.

Ce tableau contient toutes les informations permettant d’identifier les banques recherchées :

- BIC de la banque ;
- nom ;
- ville ;
- pays ;
- statut de conformité aux règles métier Universal Confirmations : conforme ou non conforme.

Le nombre de semaines pendant lesquelles les banques ont conservé un statut donné est également affiché.

Les résultats de recherche peuvent être exportés dans un fichier Excel à tout moment.

<img width="628" height="332" alt="image" src="https://github.com/user-attachments/assets/d7f23a86-49ae-4732-bc33-c659c5d2cbc3" />

En fonction des critères de recherche utilisés, plusieurs résultats peuvent apparaître dans le tableau.

<img width="628" height="342" alt="image" src="https://github.com/user-attachments/assets/1a3a271e-ae57-4ba7-a437-7d5a3a1dcac1" />

## 3.18 Score Case Management

### Indice de qualité Case Management

L’indice de qualité Case Management (*Case Management quality index*) a été défini pour évaluer les performances de vos propres entités ou de vos contreparties en matière de traitement des demandes d’investigation.

Plus précisément, cet indice permet de voir rapidement si les entités appartenant à votre propre groupe bancaire ou si vos contreparties commerciales parviennent à traiter les demandes Stop and Recall (SRP) conformément aux règles métier définies dans le *Stop and Recall for Case Management Rulebook*.

### Disponibilité de l’indice de qualité Case Management

L’indice est disponible :

- dans l’interface graphique Basic Tracker pour les entités Case Management non-GPI ;
- dans Observer Insights et Observer Analytics pour les institutions GPI.

L’interface graphique Basic Tracker est composée de deux sections :

1. **My case management score (vue personnelle)** : cette section présente votre propre indice de qualité Case Management pour le BIC sélectionné dans la liste déroulante.
2. **Other bank’s case management compliance (vue communautaire)** : cette section présente le statut de conformité Case Management des autres banques.

<img width="628" height="144" alt="image" src="https://github.com/user-attachments/assets/fce6980e-609f-4aca-b07e-58bca1ef567f" />

### Calcul de l’indice de qualité Case Management

L’indice de qualité Case Management calcule le score moyen pondéré du service SRP.

Le score du service SRP repose sur les deux indicateurs suivants :

**Indicateur 1 : réponse le jour même (*Same day response*)**

Nombre de demandes SRP pour lesquelles l’agent destinataire (*SRP assignee*) a fourni une première réponse (CNCL/RJCR/PDCR) le jour même ou le jour ouvrable suivant, lorsque la demande SRP a été reçue après l’heure limite de traitement (*cut-off time*), rapporté au nombre total de demandes SRP reçues par cet agent au cours du mois évalué.

**Indicateur 2 : réponse définitive dans les délais (*Timely final response*)**

Nombre de demandes SRP pour lesquelles l’agent destinataire a fourni :

- une réponse SRP définitive (CNCL/RJCR) ;
- ou une autre réponse indiquant que la demande est en attente (PDCR),

dans un délai de 10 jours calendaires à compter de l’initiation de la demande SRP, rapporté au nombre total de demandes SRP reçues par cet agent au cours du mois évalué.

**Exemple :**

<img width="628" height="251" alt="image" src="https://github.com/user-attachments/assets/cf4ffd52-89b9-402e-934e-47c987e2e733" />

### Mois évalué, période d’observation et mois de publication / actualisation

L’indice de qualité Case Management est calculé chaque mois pour toutes les réponses SRP relatives aux demandes SRP reçues au cours d’un mois donné.

<img width="628" height="560" alt="image" src="https://github.com/user-attachments/assets/505f066f-911e-4da4-b567-994b36d1cc91" />

### Période de calibration Case Management

Étant donné que l’indice de qualité Case Management est une nouvelle fonctionnalité, une période de calibration de six mois est définie afin d’ajuster ou de corriger toute anomalie éventuelle dans les mesures.

Pendant cette période de calibration, l’indice et les scores SRP dédiés sont accessibles uniquement à votre banque (la vue publique n’est pas proposée).

<img width="628" height="499" alt="image" src="https://github.com/user-attachments/assets/66293508-a1a8-4e41-9295-89077e79af7b" />

Votre indice de qualité de gestion des dossiers (*Case Management*) apparaît toujours en vert, même s’il est inférieur au seuil de conformité de 90 %.

### Seuils de conformité de la gestion des dossiers (Case Management)

Les scores de gestion des dossiers affichés dans votre propre vue utilisent le code couleur suivant :

- **Vert**

<img width="605" height="478" alt="image" src="https://github.com/user-attachments/assets/ed809235-eb1f-4ab3-8284-25c1fa574e9e" />

La couleur verte indique que l’indice de qualité de gestion des dossiers de l’entité est égal ou supérieur à 90 %. Cela signifie que l’entité respecte les règles métier de gestion des dossiers définies dans le *Stop and Recall for Case Management Rulebook*.

La couleur verte est visible aussi bien dans votre propre vue que dans la vue publique, après la période de calibration.

- **Orange**

<img width="605" height="481" alt="image" src="https://github.com/user-attachments/assets/02f539d5-58df-4d17-b255-9fc763f376a2" />

La couleur orange indique que l’indice de qualité de gestion des dossiers de l’entité est inférieur à 90 %. Cela signifie que l’entité ne respecte pas les règles métier de gestion des dossiers, mais qu’elle se trouve encore dans sa période d’amélioration, fixée à 6 mois.

La période d’amélioration de 6 mois est réinitialisée dès que le BIC a été conforme pendant un mois.

Une entité ayant un statut orange est uniquement affichée dans sa vue privée. Pendant cette période, son statut dans la vue publique reste vert.

- **Rouge**

<img width="605" height="480" alt="image" src="https://github.com/user-attachments/assets/4b1e08f4-d000-4cc6-9331-2b41d95116c8" />

La couleur rouge indique que l’institution financière n’a pas respecté les règles métier de gestion des dossiers pendant 6 mois consécutifs et que sa période d’amélioration est terminée.

Ce score rouge est visible dans la vue personnelle et dans la vue publique.

**Remarque :** Si aucun trafic pertinent n’est reçu au cours du mois faisant l’objet du rapport, l’indice de qualité et le statut de gestion des dossiers du mois précédent sont reportés sur le mois en cours.

### Conformité des autres banques en matière de gestion des dossiers (vue publique)

À la fin de la période de calibration, les utilisateurs de Case Management peuvent accéder à la vue publique afin d’analyser le statut de conformité des autres contreparties utilisant Case Management.

Ils peuvent également consulter le nombre de mois pendant lesquels chaque contrepartie a été conforme ou non aux règles métier.

<img width="628" height="483" alt="image" src="https://github.com/user-attachments/assets/e1e97635-55d5-40fb-aa1f-fe3c46e4295e" />

## 3.19 Score Swift Go

### Indice de qualité Swift Go

L’indice de qualité Swift Go est défini pour évaluer les performances de vos propres entités ou de vos contreparties dans le traitement des paiements Swift Go, conformément au *Swift Go Rulebook*.

### Indice de qualité Swift Go et calculs

La conformité des clients Swift Go aux règles métier est mesurée au moyen d’un indice de qualité.

Cet indice est calculé mensuellement pour chaque BIC Live de 8 caractères enregistré sur le service Swift Go.

Les indicateurs Swift Go sont répartis en deux catégories : **Critiques** et **Autres**.

Pour plus d’informations sur les indicateurs et les règles appliquées, consultez la section Observer Insights du *Swift Go Rulebook*.

Les indicateurs critiques (*Critical metrics*) sont les suivants :

- Montants non modifiés (*Unaltered amounts*) ;
- Routage conforme au Swift Go Rulebook (*Swift Go Rulebook routing*) ;
- Identifiant du type de service non modifié (*Unaltered service type identifier*).

Ils contribuent au calcul de l’indice de qualité du Swift Go Rulebook avec une pondération de **80 %**.

Les autres indicateurs (*Other metrics*) sont les suivants :

- Montant interbancaire dans les limites autorisées (*Interbank amount within limit*) ;
- Porteur des frais (*Charge bearer*) ;
- Rapidité (*Speed*) ;
- Traçabilité (*Traceability*) ;
- Informations de remise non modifiées (*Unaltered remittance*).

Ils représentent une pondération de **20 %**.

Chaque indicateur Swift Go est agrégé dans sa catégorie respective (Critique ou Autre), sur la base de la moyenne pondérée des indicateurs par rôle.

La pondération dépend de la proportion du volume de paiements traités pour chaque rôle par le BIC de 8 caractères considéré. Les BIC de 11 caractères provenant du répertoire GPI sont regroupés au niveau du BIC de 8 caractères.

Pour plus d’informations sur le calcul arithmétique de l’indice de qualité, consultez la section Swift Go du *Observer Insights for Swift GPI User Guide*.

### Disponibilité de l’indice de qualité Swift Go

L’indice est disponible :

- Dans l’interface graphique Basic Tracker pour les clients Swift Go qui ne sont pas clients GPI ;
- Dans Observer Insights / Observer Analytics pour les clients GPI.

L’interface graphique Basic Tracker comporte deux sections :

- **My Swift Go score** : affiche votre propre indice de qualité Swift Go pour le BIC sélectionné dans la liste déroulante.
- **Other banks' Swift Go compliance** : affiche le statut de conformité Swift Go des autres clients Swift Go disposant du statut Live.

<img width="628" height="177" alt="image" src="https://github.com/user-attachments/assets/5d7435a1-cd5b-42e1-ba57-8d31c512be34" />

### Période de calibration et seuils Swift Go

L’indice de qualité Swift Go permet de déterminer le statut de conformité de chaque BIC Live de 8 caractères.

En cas de non-conformité, c’est-à-dire lorsque l’indice de qualité est inférieur à 90 %, les clients Swift Go disposent de trois mois pour améliorer leur score.

Si, à l’issue de cette période de trois mois, l’indice de qualité reste inférieur à 90 %, leur statut public sur la page communautaire d’Observer Insights et dans le score *Other banks' Swift Go compliance* de l’interface Basic Tracker apparaît comme non conforme (code couleur rouge).

- **Vert**

<img width="605" height="240" alt="image" src="https://github.com/user-attachments/assets/b716e965-864e-4429-9b27-6dff6ff2db06" />

Le statut vert indique que l’indice de qualité Swift Go du client est égal ou supérieur à 90 %. Cela signifie que le client respecte les règles métier Swift Go définies dans le *Swift Go Rulebook*.

- **Orange**

<img width="605" height="271" alt="image" src="https://github.com/user-attachments/assets/2797993f-88ad-42bf-b86b-98ea73c5e4e5" />

Le statut orange indique que l’indice de qualité Swift Go du client est inférieur à 90 %. Cela signifie que le client ne respecte pas les règles métier Swift Go, mais qu’il se trouve encore dans sa période d’amélioration, fixée à trois mois.

La période d’amélioration de trois mois est réinitialisée dès que le client a respecté les règles métier Swift Go pendant un mois.

**Remarque :** Le statut orange est uniquement affiché dans la vue du client. Pendant cette période, le statut dans la vue publique reste vert.

- **Rouge**

<img width="605" height="276" alt="image" src="https://github.com/user-attachments/assets/1c4f9218-c981-4df0-bda7-0b763d78c59a" />

Le statut rouge indique que le client n’a pas respecté les règles métier Swift Go pendant trois mois consécutifs et que sa période d’amélioration est terminée.

Le statut rouge est visible dans la vue du client ainsi que dans la vue publique.

**Remarque :** Si aucun trafic pertinent n’est reçu au cours du mois faisant l’objet du rapport, l’indice de qualité et le statut Swift Go du mois précédent sont reportés sur le mois en cours.

### Conformité Swift Go des autres banques (vue publique)

À la fin de la période de calibration, les clients Swift Go peuvent accéder à la vue publique pour analyser le statut de conformité des autres clients Swift Go et connaître le nombre de mois pendant lesquels chaque contrepartie a respecté ou non les règles métier Swift Go.

## 3.20 Administrer les paramètres

### Journaux d’audit (Audit logs)

Les journaux d’audit permettent aux utilisateurs de Basic Tracker de disposer de fonctionnalités d’audit afin de suivre les modifications apportées aux paramètres, notamment l’activation ou la désactivation d’une alerte de paiement ou des paramètres d’approbation à quatre yeux (*4-eyes approval*).

Plus précisément, la fonctionnalité de journal d’audit permet à chaque utilisateur de Basic Tracker d’identifier :

- Les administrateurs ayant effectué les modifications ;
- Le type de modification apportée aux paramètres ;
- La date et l’heure auxquelles ces modifications ont été effectuées.

Les journaux sont disponibles dans les paramètres de l’interface graphique Basic Tracker et peuvent être consultés par tous les utilisateurs, quel que soit leur rôle.

Les journaux restent disponibles dans Basic Tracker pendant **124 jours** et peuvent être exportés dans un fichier Excel à tout moment, selon les besoins.

### Notifications d’alerte (Alert notifications)

Certains paiements ou messages de confirmation peuvent être identifiés comme invalides par Tracker. Cela se produit essentiellement lorsqu’ils ne correspondent pas au reste de la transaction de paiement globale telle qu’elle est enregistrée dans Tracker.

Ces messages sont alors signalés comme invalides dans la base de données de Tracker.

Les utilisateurs ayant envoyé ces paiements invalides ou ces confirmations de paiement peuvent demander à être informés en activant le mécanisme d’alerte depuis l’écran d’administration de Basic Tracker.

Une fois cette fonctionnalité activée, Tracker génère des notifications d’alerte sous la forme de messages MT 199 (mode push).

Différents cas d’utilisation peuvent être distingués. Ils sont présentés dans les sous-sections suivantes.

<img width="628" height="446" alt="image" src="https://github.com/user-attachments/assets/ac674fef-1f9d-47c8-afed-2aa74e7756ba" />

### Alertes liées aux messages de paiement MT 103 invalides

La banque B envoie un message de paiement de transfert de crédit client invalide, au format MT 103 ou pacs.008 (1), et a configuré Basic Tracker pour générer des messages d’alerte ISO MX trck.003.

<img width="654" height="378" alt="image" src="https://github.com/user-attachments/assets/f3d69f62-ef84-4318-9c8e-186f10de292d" />

### Alertes liées aux messages de confirmation invalides

La banque B envoie un message de confirmation invalide, au format MT 199 ou ISO FINplus trck.001 (2), et a configuré Basic Tracker pour générer des alertes FIN MT 199.

<img width="654" height="378" alt="image" src="https://github.com/user-attachments/assets/fb19d45e-6d64-4ab7-ab29-12f9d0df4002" />

### Paramètres des alertes

Basic Tracker dispose d’un écran d’administration dédié qui permet d’activer et de gérer les notifications d’alerte.

<img width="628" height="533" alt="image" src="https://github.com/user-attachments/assets/e1d03c5e-2627-4077-8d54-aaa028ad4f0d" /> <br>

<img width="628" height="111" alt="image" src="https://github.com/user-attachments/assets/47fb1e55-f987-4569-a03b-9ed9ed5a9323" />

**Remarque :** Vous devez disposer du rôle RBAC **Admin** pour accéder aux paramètres des notifications d’alerte et les modifier.

Les clients dont les BIC sont provisionnés sur Swift Go peuvent activer ou désactiver toutes les alertes liées à Swift Go en bas de l’onglet **Payment alert**.

<img width="628" height="179" alt="image" src="https://github.com/user-attachments/assets/04672f0f-4065-4385-bfef-58e7b72f824f" />

Les utilisateurs peuvent configurer Basic Tracker pour envoyer des notifications d’alerte de type **INVALID** (invalide) ou **WARNING** (avertissement).

Les messages d’alerte MT 199 sont envoyés par :

- **TRCKCHZZVAL** en environnement Live ;
- **TRCKCHZ0VAL** en environnement de test.

<img width="628" height="207" alt="image" src="https://github.com/user-attachments/assets/e7be2482-70c3-4f8d-9171-20d473034f24" />

Pour plus d’informations sur le format des notifications d’alerte, ainsi que sur les codes de statut et les codes de motif, consultez le *Universal Confirmations Rulebook*.

**Remarque :** Pour activer ces flux de messagerie avec Tracker, les utilisateurs doivent échanger une autorisation RMA avec le BIC de Tracker.

Une seule autorisation RMA couvre les deux flux, puisqu’elle est établie au niveau :

- De TRCKCHZZ (BIC Tracker Live) ;
- Ou de TRCKCHZ0 (BIC Tracker de test).

Pour plus d’informations sur RMA, consultez la documentation *Relationship Management Application in RMA Service - Service Description*.

### Notifications Stop and Recall (SRP)

Les clients non-GPI ayant souscrit à Case Management peuvent bénéficier des notifications SRP.

Pour le SRP, les utilisateurs peuvent demander à Basic Tracker de recevoir :

**Une demande SRP (SRP Request) :**

- Au format MT 192 (par défaut) ;
- Au format camt.056.

**Une réponse SRP (SRP Response) :**

- Au format MT 196 ;
- Au format MT 199 ;
- Au format camt.029 ;
- Aucune réponse (par défaut).

Les paramètres précédents déterminent si Basic Tracker effectue une traduction :

- De MT 192 vers camt.056, ou de camt.056 vers MT 192 ;
- De MT 196 / MT 199 vers camt.029, ou de camt.029 vers MT 196 / MT 199.

Les utilisateurs peuvent également déterminer s’ils souhaitent recevoir une notification de changement de statut d’une demande SRP au moyen d’un message MT 199.

<img width="628" height="194" alt="image" src="https://github.com/user-attachments/assets/e06a741e-a8c0-4dbf-98ab-d17969353b4b" /> <br>

<img width="628" height="135" alt="image" src="https://github.com/user-attachments/assets/c15e9aea-8fe3-44f3-b5ed-c25408aa5edb" />

### Approbation à quatre yeux (4-eyes approval)

Basic Tracker prend en charge la fonctionnalité d’approbation à quatre yeux.

Lorsqu’elle est activée, un utilisateur peut lancer le processus de confirmation d’un paiement, mais un autre utilisateur doit obligatoirement autoriser et approuver ce processus de confirmation.

Si le paramètre d’approbation à quatre yeux est activé, au moins deux utilisateurs doivent ensuite être définis.

### Paramètres de l’approbation à quatre yeux

En plus de la configuration des paramètres des notifications d’alerte, les utilisateurs disposant du rôle Administrateur peuvent également activer ou désactiver le processus d’approbation à quatre yeux.

Si ce paramètre est activé, au moins deux utilisateurs doivent ensuite être définis.

**Remarque :** Par défaut, le paramètre d’approbation à quatre yeux est activé.

<img width="628" height="147" alt="image" src="https://github.com/user-attachments/assets/989085d0-af01-4be6-bf4f-fe2fa11053a1" />

**Remarque :** Vous devez disposer du rôle RBAC **Admin** pour accéder aux paramètres d’approbation à quatre yeux et les modifier.

<img width="537" height="177" alt="image" src="https://github.com/user-attachments/assets/19827429-d524-4104-a6e6-59c113d3150f" />

---

# 4. Utilisation des API Tracker

Les clients peuvent mettre à jour les transactions en fournissant des mises à jour de statut au moyen des services API de mise à jour du statut des paiements, en version **v5 ou v6**.

La spécification est disponible sur le Developer Portal.

Les clients non-GPI qui souhaitent fournir des mises à jour par API doivent souscrire au service API pour leurs BIC en remplissant le formulaire de commande électronique (*e-order form*).

Les clients qui souscrivent à la mise à jour de Tracker via API se voient attribuer le rôle RBAC **Update** pour :

- Le service API pilote : `swift.apitracker!p` ;
- Le service API Live : `swift.apitracker`.

Les clients Payment Market Infrastructure (PMI) ayant souscrit au service Network Interoperability se voient attribuer un rôle RBAC supplémentaire, **NIPMIupdate**, pour le service API.

Ce rôle RBAC NIPMIupdate permet à ces clients de mettre à jour Tracker au nom de leurs participants.

Il leur permet notamment de confirmer que l’agent du créancier (*Creditor Agent*) a crédité le créancier (*Creditor*), lorsque la PMI dispose de cette information.

---

# 5. Qualité des données de Tracker

Basic Tracker est conçu pour mettre à jour et afficher le statut des transactions sur la base des messages conformes aux règles métier et aux spécifications techniques décrites dans le *Universal Confirmations Rulebook*.

## Devise et montant ordonnés (champ 33B du MT 103)

La devise et le montant ordonnés doivent rester inchangés tout au long de la chaîne de traitement de la transaction.

Le contenu de ce champ est utilisé pour vérifier que l’UETR est unique pour une transaction.

Si un même UETR est utilisé alors que le montant ou la devise ordonnés sont différents, cela est considéré comme une réutilisation d’un UETR existant et l’événement de paiement est invalidé.

## Agent du débiteur et agent du créancier (champs 52A et 57A du MT 103)

Basic Tracker affiche les informations relatives à l’agent du débiteur ou à l’agent du créancier uniquement lorsque ces agents sont présents dans les messages de transfert de crédit client (MT 103 ou pacs.008) reçus et/ou envoyés.

Tracker identifie ces parties au moyen de leurs BIC respectifs et affiche le nom de l’établissement tel qu’il est publié dans BIC Plus.

## Messages en double (Duplicate messages)

Tracker effectue automatiquement une vérification des doublons en comparant le contenu des mises à jour de statut des transferts de crédit client avec les mises à jour de statut précédemment reçues portant le même UETR.

Tracker traite les doublons comme des messages valides et les associe à la transaction.

## Collision d’UETR (UETR collision)

Un UETR ne peut servir à identifier qu’une seule transaction.

Tracker utilise l’agent du débiteur (*Debtor Agent*) et le montant ordonné (*Instructed Amount*) pour vérifier que l’UETR n’a pas déjà été utilisé pour identifier une autre transaction.

Lorsque cette vérification échoue, le message est signalé comme invalide et n’est pas ajouté à la transaction déjà identifiée par cet UETR.

Lorsqu’une transaction comporte deux messages de transfert de crédit client consécutifs, c’est-à-dire lorsque l’expéditeur du deuxième message est le destinataire du premier, Tracker vérifie la deuxième mise à jour du statut du paiement comme suit :

**Devise et montant ordonnés (Instructed Currency and Amount)**

- Si la devise et le montant ordonnés sont présents dans les deux messages, leurs contenus doivent être identiques.
- Si la devise et le montant ordonnés sont présents dans le deuxième message, mais absents du premier, la devise et le montant ordonnés du deuxième message doivent être identiques à la devise et au montant du règlement interbancaire (*Interbank Settlement Currency and Amount*) du premier message.
- Si la devise et le montant ordonnés ne sont pas présents dans le deuxième message, la validation est considérée comme réussie.

**Agent du débiteur (Debtor Agent)**

- Si l’agent du débiteur est présent dans les deux messages, le BIC de 8 caractères doit être identique dans les deux messages.
- Si l’agent du débiteur n’est présent dans aucun des deux messages, la validation est considérée comme réussie.
- L’agent du débiteur n’est pas soumis à validation dans les messages de test et de formation (*Test and Training*).

Lorsqu’une transaction comporte deux messages non consécutifs, c’est-à-dire lorsque l’expéditeur du deuxième message n’est pas le destinataire du premier, Tracker vérifie le deuxième message comme suit :

- Si la devise et le montant ordonnés sont présents dans les deux messages, ils doivent être identiques.
- Si la devise et le montant ordonnés sont présents dans le deuxième message, mais absents du premier, la validation est considérée comme réussie. Dans ce scénario, une comparaison avec le montant du règlement interbancaire n’est pas possible, car des déductions peuvent avoir été effectuées entre les deux messages.
- Si le montant du règlement interbancaire (*Interbank Settlement Amount*) n’est pas présent dans le deuxième message, la validation est considérée comme réussie.
- Aucune validation de l’agent du débiteur (*Debtor Agent*) n’est effectuée.

**Remarque :** L’expéditeur initial peut établir, dans sa propre application, une corrélation entre les différentes mises à jour reçues de chaque intermédiaire.

Si le statut affiché dans Basic Tracker ne correspond pas au statut réel dans l’application de paiement de l’expéditeur, contactez immédiatement le support Swift.

---

# 6. Passage à Swift GPI

L’avenir des paiements transfrontaliers prend déjà forme avec Swift GPI, qui offre une approche complète pour accompagner l’évolution du paysage des paiements internationaux.

Depuis janvier 2017, Swift GPI s’attaque, sur les plans tactique et stratégique, aux principaux points de friction des paiements transfrontaliers.

Il garantit que le processus des paiements internationaux répond aux exigences de l’ensemble du secteur en matière de rapidité, de transparence et d’amélioration de l’expérience utilisateur finale.

Il fournit ainsi aux clients des banques des informations fluides, cohérentes et en temps réel sur le statut et la localisation de leurs paiements.

Swift GPI constitue l’une des évolutions les plus ambitieuses et les plus importantes du secteur de la banque correspondante depuis plusieurs décennies.

Il réinvente les activités de paiements transfrontaliers en introduisant une infrastructure pérenne, résiliente et sécurisée, continuellement enrichie par des améliorations et des services supplémentaires destinés à tous les utilisateurs de la chaîne de paiement.

Il offre à toutes les institutions financières la possibilité :

- D’augmenter le traitement automatisé de bout en bout (*Straight-Through Processing*) de leurs opérations ;
- De réduire les coûts et les risques ;
- D’améliorer la gestion de la liquidité ;
- De suivre numériquement leurs propres paiements ainsi que ceux de leurs clients.

Pour tirer pleinement parti de la révolution Swift GPI, bénéficier d’un suivi complet de bout en bout avec des informations détaillées sur les montants, les déductions, le routage par les intermédiaires et les opérations de change (FX), ainsi que pour accéder à de nombreuses fonctionnalités supplémentaires puissantes, les utilisateurs de Basic Tracker peuvent facilement passer à Swift GPI.

La suite de produits Swift GPI comprend trois composants :

**1. Swift GPI Tracker**

Plateforme de suivi des paiements de bout en bout utilisée pour surveiller l’évolution d’une transaction GPI.

L’interface graphique Tracker (GUI) permet aux clients GPI de suivre le parcours d’une transaction presque en temps réel, d’obtenir une visibilité sur les déductions et la rapidité du traitement, ainsi que de consulter le statut final de la transaction.

**2. Observer Insights**

Tableau de bord de Business Intelligence présentant la conformité des clients GPI aux règles du *Swift GPI Rulebook for Mandatory Services*, notamment :

- GPI Customer Credit Transfer ;
- GPI Cover Payments.

Observer Insights offre une visibilité sur le respect de certaines règles métier sélectionnées dans le *Swift GPI Rulebook for Mandatory Services* pour les transferts de crédit client GPI et les paiements de couverture GPI.

**3. Directory**

Le répertoire fournit des informations opérationnelles sur les clients Swift GPI, notamment :

- Les BIC applicables ;
- Les devises ;
- Les heures limites de traitement (*cut-off times*).

Le répertoire est utilisé par Tracker et Observer pour déterminer si le destinataire d’un transfert de crédit client Swift GPI (*gCCT*) est censé traiter le paiement conformément aux règles GPI.

Pour les flux non-FIN ou non-SwiftNet, les banques doivent utiliser le répertoire afin d’informer Tracker si la banque suivante dans la transaction de paiement traite le paiement conformément aux règles GPI.

Le tableau suivant met en évidence les principales différences entre Basic Tracker et Swift GPI.

**Ensemble de fonctionnalités | Basic Tracker**

**Recherche (Search)**

- Recherche par UETR et identification de l’instruction : OUI (1).
- Recherche détaillée et options d’exportation des résultats.

**Données (Data)**

- Statut du paiement et heure de la dernière mise à jour, UETR, identification de l’instruction, identification de l’agent du débiteur et de l’agent du créancier, devise et montant ordonnés : OUI (1).
- Montant et devise crédités.
- Localisation du paiement dans la ligne de métro, coordonnées bancaires et identification de l’instruction des intermédiaires.
- Référence de l’expéditeur, déductions, opérations de change (FX) et date de valeur.

**Ensemble de fonctionnalités | Basic Tracker**

**Mise à jour et consommation des données (Update and consume)**

- Mise à jour manuelle via l’interface graphique (GUI) : OUI.
- Mise à jour via API, FIN ou FINplus trck.001 : OUI.
- Consultation des informations via l’interface graphique (GUI) : OUI (1).
- Consultation des mises à jour de statut via API ou FIN.

**Mesure (Measure)**

- Respect des règles Universal Confirmations par sa propre entité : OUI.
- Respect des règles Universal Confirmations par les contreparties : OUI (1).
- SLA GPI (propre entité et contreparties).

**Valeur ajoutée (Value Add)**

- Initiation SRP, g4C (Pay and Trace, Inbound Tracking) et futurs services à valeur ajoutée.
- Services d’intégration (*Onboarding services*).

**(1)** Les fonctionnalités sont bloquées lorsque les banques ne respectent pas les règles métier Universal Confirmations.

---

# 7. Support

## Assistance aux clients Swift

Par défaut, Swift Support constitue le point de contact unique pour signaler tous les problèmes et soumettre toutes les questions relatives aux services et produits Swift.

Le service d’assistance est accessible à tous les clients Swift.

Les personnes appartenant à une organisation cliente doivent s’inscrire sur swift.com pour pouvoir utiliser le service Support.

Pour plus d’informations sur les différents services proposés par Swift dans le cadre de ses offres d’assistance, ainsi que sur la procédure de commande de ces services, consultez la rubrique *Support and Care Services* sur swift.com.

Swift fournit une assistance uniquement pour ses propres services et produits.

Par exemple, Swift ne fournit pas d’assistance pour les systèmes matériels et logiciels sous-jacents utilisés avec ses produits, tels que :

- Les systèmes d’exploitation ;
- Les logiciels de messagerie intermédiaires de fournisseurs tiers (*third-party messaging middleware*).

En cas de problème ou de question concernant ces systèmes matériels ou logiciels tiers, les clients doivent contacter le fournisseur responsable (*Vendor*).

## Informations complémentaires

Pour plus d’informations sur les services d’assistance, consultez la documentation descriptive correspondant au forfait d’assistance applicable : *Support documentation*.

---

# Annexe A : Alertes Tracker

## A.1 Alertes Tracker basées sur les messages FIN MT

En complément de la validation réseau et/ou de la validation du schéma, Tracker applique des contrôles supplémentaires.

Ces contrôles portent également sur :

- La qualité des mises à jour de statut des paiements par transfert de crédit client ;
- La transmission correcte des informations du transfert de crédit client reçu vers le message de paiement suivant.

Lorsque cette fonctionnalité est configurée, Tracker génère des messages d’alerte (MT 199 ou trck.003) à partir de Tracker (TRCKCHZZVAL) à destination de l’émetteur du statut (*status originator*).

La notification d’alerte n’est pas envoyée aux autres banques (GPI) participant à la transaction.

Les utilisateurs FIN ne peuvent prendre connaissance des messages d’alerte MT 199 que s’ils choisissent de les recevoir dans Basic Tracker et que les autorisations RMA ont été échangées avec le BIC de Tracker.

## Format de la notification d’alerte MT 199

- **Le MT 199 « alert »** contient le même UETR (champ 121) que la confirmation reçue de l’émetteur du statut.
- **Le champ 20** contient une référence générée par Tracker pour ce nouveau MT 199.
- **Le champ 21** contient la valeur du champ 20 du message de confirmation MT 199 reçu (ou l’InstructionIdentification de la requête API).
- **Le champ 79** contient :
  - `//(Date)(Time)(Sign)(Offset)` : la date et l’heure de génération de l’alerte, avec indication du décalage par rapport à UTC (temps universel coordonné, norme ISO 8601).
  - `//(status code)/(reason code)` : pour plus d’informations, consultez la section *Tracker Errors*, page 91.
  - `//BIC` : le BIC de l’émetteur du statut figurant dans le message de confirmation à l’origine de l’alerte.

Il est possible qu’un transfert de crédit client reçu ne nécessite aucune confirmation et ne soit donc pas affiché dans la liste des paiements en attente de confirmation de Basic Tracker.

Cela peut notamment se produire lorsque le montant ordonné dans le paiement a été modifié par rapport au montant ordonné reçu.

Conformément à la documentation des normes, le montant ordonné doit être transmis sans modification tout au long de la transaction.

Le contenu de ce champ est utilisé pour vérifier que l’UETR est unique pour une transaction.

Si le même UETR est utilisé alors qu’une étape du paiement (*payment leg*) contient un montant ou une devise ordonnés différents, cela est considéré comme une réutilisation d’un UETR existant.

Le message est alors invalidé et n’est pas associé à la transaction d’origine.

Par conséquent, dans ce cas, Tracker n’utilise pas le transfert de crédit client suivant pour mettre à jour le statut de la transaction.

Les messages MT 103 invalidés par Tracker sont exclus des mesures du score Universal Confirmations.

## A.2 Alertes Tracker basées sur les messages ISO trck

En complément de la validation des messages sur le réseau SwiftNet, Tracker applique des contrôles supplémentaires afin de garantir la validité des mises à jour de statut.

Ces contrôles portent également sur :

- La qualité des messages suivis ;
- La transmission correcte des informations du message entrant vers le message sortant sur Swift.

**Remarque :** Les utilisateurs Swift ne peuvent prendre connaissance de ces messages d’alerte que s’ils activent leur réception dans Basic Tracker et échangent une autorisation RMA avec le BIC de Tracker.

Pour plus d’informations, consultez le *Basic Tracker Operations Guide*.

Lorsque cette fonctionnalité est activée dans le menu d’administration de Basic Tracker et que le format de message XML ISO (MX) est sélectionné, des alertes au format **trck.003.001.02** peuvent être envoyées par Tracker (TRCKCHZZVAL, TRCKCHZ0VAL en environnement de test) à la partie informée par Tracker (*Tracker informing party*).

La notification d’alerte n’est pas envoyée aux autres banques (GPI) participant à la transaction.

**Important :** Swift recommande fortement de configurer et de surveiller ces alertes provenant de Tracker. Dans le cas contraire, le client ne sera pas informé lorsqu’une confirmation est rejetée par Tracker.

Pour plus d’informations sur la structure du statut des alertes, consultez les directives d’utilisation de trck.003 sur MyStandards.

## Notifications d’alerte Tracker

| Élément XML | Description |
| --- | --- |
| `<GrpHdr><MsgId>` | Référence unique du message générée par Tracker. |
| `<TrckrStsAndTx><AlrtSts><AlrtSts><Cd>` | Code de statut de l’alerte Tracker : **INVA** pour Invalide, **WARN** pour Avertissement, **RJCR** pour Demande d’annulation rejetée, **RJIN** pour Investigation rejetée. |
| `<TrckrStsAndTx><AlrtSts><StsRsn><Prtry>` | Code de motif du statut de l’alerte Tracker, tel qu’indiqué dans la section *Tracker Errors*, page 91. |
| `<TrckrStsAndTx><AlrtSts><AddtlInf>` | Description du motif du statut de l’alerte Tracker. |
| `<TrckrStsAndTx><Tx><TrckdMsgId><MsgNmId>` | Fait référence au type de requête du message invalide. |
| `<TrckrStsAndTx><Tx><TrckdMsgId><CreDtTm>` | Date et heure de création du message ayant déclenché l’alerte. |
| `<TrckrStsAndTx><Tx><TrckrInfrmgPty><Id><FinInstnId><BICFI>` | Expéditeur du message invalidé ou faisant l’objet d’un avertissement. Si le statut de l’alerte est INVA et que le motif est X001, le BIC TrackerInformingParty est TRCKCHZZ. |
| `<TrckrStsAndTx><Tx><PmtId><InstrId>` | Identification de l’instruction ou champ 20 du paiement FIN. |
| `<TrckrStsAndTx><Tx><PmtId><UETR>` | UETR du message associé. |

## A.2.1 Exemple

Alerte Tracker envoyée après la détection d’une incohérence dans l’UETR du message trck.001.001.03 (le message ne peut pas être associé au paiement pour lequel la confirmation est fournie).

Exemple de message XML fourni dans le document source :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Document xmlns="urn:swift:xsd:trck.003.001.02"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <TrckrAlrtNtfctn>
    <GrpHdr>
      <MsgId>ALERTWXYZ9876</MsgId>
    </GrpHdr>
    <TrckrStsAndTx>
      <AlrtSts>
        <AlrtSts>
          <Cd>INVA</Cd>
        </AlrtSts>
        <StsRsn>
          <Prtry>X004</Prtry>
        </StsRsn>
      </AlrtSts>
      <Tx>
        <TrckdMsgId>
          <MsgNmId>trck.001.001.03</MsgNmId>
          <CreDtTm>2020-12-14T06:10:31Z</CreDtTm>
        </TrckdMsgId>
        <TrckrInfrmgPty>
          <Id>
<FinInstnId>
  <BICFI>WXYZUS33</BICFI>
</FinInstnId>
</Id>
</TrckrInfrmgPty>
<PmtId>
  <InstrId>ABCD12345WXYZ</InstrId>
  <UETR>f2bfc320-4001-47c7-b0e0-7904861042a4</UETR>
</PmtId>
</Tx>
</TrckrStsAndTx>
</TrckrAlrtNtfctn>
</Document>
```

## A.3 Erreurs Tracker

Les tableaux de cette section répertorient les différents codes de statut et codes de motif susceptibles d’être utilisés dans les notifications d’alerte de Basic Tracker.

### Messages d’erreur relatifs aux paiements et aux confirmations de statut

| Statut | Code | Description | Associé à |
| --- | --- | --- | --- |
| INVA | X001 | Erreur de syntaxe | Message de confirmation |
| INVA | X002 | L’émetteur du statut n’est pas autorisé à mettre à jour le statut de ce paiement (envoi éventuellement dans le désordre). | Message de confirmation |
| WARN | X003 | La transaction est déjà dans son état final. Aucune action supplémentaire n’est nécessaire. | MT 103 ou pacs.008. Message de confirmation. Aucune notification d’alerte n’est envoyée par Tracker. |
| INVA | X004 | Identifiant de transaction inconnu. La mise à jour du statut a éventuellement été envoyée dans le désordre. | Message de confirmation |
| WARN | X005 | Le montant ordonné du message de paiement ne correspond pas aux messages de paiement précédemment envoyés pour le même identifiant de transaction. | MT 103 ou pacs.008 |
| INVA | X007 | Un message de paiement suivi invalide la mise à jour du statut. | MT 103 ou pacs.008 |
| INVA | X008 | Cette institution n’est pas censée fournir cette mise à jour de statut (envoi éventuellement dans le désordre). | Message de confirmation |
| WARN | X009 | L’agent du débiteur ne correspond pas à celui indiqué dans les messages de paiement précédemment envoyés pour le même identifiant de transaction. | MT 103 ou pacs.008 |
| INVA | X011 | Mise à jour du statut non autorisée. | Message de confirmation |
| INVA | X012 | Les déductions ne correspondent pas. | Message de confirmation gCCT |
| WARN | X018 | L’UETR a déjà été utilisé dans le service GPI. | MT 103 ou pacs.008. Message de confirmation (INVA). |
| INVA | X021 | La valeur du champ SettlementMethod n’est pas autorisée. | Message de confirmation |
| INVA | X021 | La valeur du champ ClearingSystem n’est pas autorisée. | Message de confirmation |
| INVA | X021 | Seule une confirmation de statut ACCC est autorisée. | Message de confirmation |

### Suite des messages d’erreur relatifs aux paiements et aux confirmations de statut

| Statut | Code | Description | Associé à |
| --- | --- | --- | --- |
| INVA | X021 | La valeur du champ Reject Reason Code n’est pas autorisée. | Message de confirmation |
| INVA | X026 | La partie informée par Tracker et l’agent ordonné d’une confirmation de statut Swift Go doivent être des banques participant au service Swift Go. | Confirmation Swift Go |
| WARN | X040 | Les étapes envoyées par l’agent du créancier avec la méthode de règlement INGA ne sont pas suivies. | pacs.008. Message de confirmation (INVA). Aucune notification d’alerte n’est envoyée par Tracker. |
| WARN | X041 | Une incohérence de montant a été détectée. | MT 103 ou pacs.008. Confirmation de statut ACSP/G000, ACSP/G001 ou ACCC. Aucune invalidation. |
| WARN | X041 | Il s’agit d’une deuxième conversion de change (FX) effectuée par un agent intermédiaire dans la même transaction gCCT. | MT 103 ou pacs.008. Aucune invalidation. |
| INVA | X042 | Les confirmations de statut ou les messages de rejet ne sont pas pris en charge pour une transaction appartenant à un flux de retour. | Confirmation pacs.002 ou MT 103 REJT |
| WARN | X044 | Les messages pacs.008 ne sont pas suivis dans une transaction appartenant à un flux de retour. | pacs.008 |
| WARN | I001 | Le montant transféré dépasse le seuil autorisé pour la devise, conformément au Swift Go Rulebook. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I002 | Le code de frais n’est pas valide pour une transaction Swift Go. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I003 | Les frais à la charge de l’expéditeur ne sont pas autorisés pour une transaction Swift Go. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I004 | Le montant du règlement interbancaire d’une transaction Swift Go doit correspondre à celui de l’étape précédente. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I005 | La devise n’est pas prise en charge par le destinataire du message Swift Go. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I006 | Le bénéficiaire n’est pas un client Swift Go. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |
| WARN | I008 | La confirmation d’un crédit partiel n’est pas prise en charge pour Swift Go. | Étape de transaction activée pour Swift Go, avec identifiant de type de service 009 / niveau de service G009 |

### Messages d’erreur SRP

| Statut | Code | Description | Associé à |
| --- | --- | --- | --- |
| RJCR | FRNA | La demande doit être transmise à l’agent suivant. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API). Consulter le Stop and Recall Rulebook pour connaître la syntaxe spécifique utilisée pour RJCR/FRNA. |
| RJCR | X015 | La transaction gCCT est dans un état rejeté. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | Un processus SRP est déjà en cours pour cette transaction gCCT. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |

### Suite des messages d’erreur SRP

| Statut | Code | Description | Associé à |
| --- | --- | --- | --- |
| RJCR | X015 | Ce BIC n’est pas autorisé à initier le SRP, car il ne fait pas partie de la transaction gCCT. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | L’identifiant du type de service de cette demande doit être 002. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | Aucune transaction gCCT n’a été identifiée pour cet UETR. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | La référence de transaction de la transaction gCCT sous-jacente ne correspond pas à la demande SRP. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | Le mot-code est manquant ou invalide. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X015 | Seul le code INDM est autorisé comme texte supplémentaire après le code du motif d’annulation. | Message d’initiation Stop and Recall (MT 192, MT 199, CancelTransaction - API) |
| RJCR | X016 | L’identifiant du type de service de cette demande doit être 002. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |
| RJCR | X016 | La référence de transaction de la demande d’annulation sous-jacente ne correspond pas à la réponse SRP. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |
| RJCR | X016 | Combinaison manquante ou invalide du mot-code avec le code de motif conditionnel. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |
| RJCR | X016 | Le statut n’est pas autorisé, car aucun processus SRP n’est en cours. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |
| RJCR | X016 | Ce BIC n’est pas autorisé à répondre à la demande SRP. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |
| RJCR | X016 | L’agent destinataire du transfert (*forwarded agent*) doit être vide. | Message de réponse Stop and Recall (MT 196, MT 199, TransactionCancellationStatus - API) |

# Annexe B : Traitement de Tracker dans l’environnement de test

Grâce à l’interopérabilité prise en charge par Tracker pendant la période de coexistence liée à la migration vers ISO 20022, les différentes étapes d’une transaction de paiement peuvent être constituées d’un mélange de messages FIN MT et de messages ISO 20022.

De même, les mises à jour du statut des paiements envoyées à Tracker peuvent être fournies au moyen :

- De messages FIN MT ;
- De messages ISO 20022 ;
- D’API ;
- De l’interface graphique (GUI).

Cela reste possible indépendamment du ou des formats utilisés pour les messages de paiement.

Il est ainsi possible de mettre à jour Tracker concernant un paiement FIN (MT 103) au moyen d’un message de mise à jour de statut ISO 20022 trck.001.

Inversement, il est possible de mettre à jour Tracker concernant un paiement ISO 20022 pacs.008 au moyen d’un message FIN MT 199, d’une API ou de l’interface graphique Tracker.

Bien que cette interopérabilité fonctionne de manière transparente dans l’environnement Live, une particularité doit être prise en compte dans l’environnement de test concernant l’utilisation des BIC de test (BIC dont le huitième caractère est zéro, par exemple SENDBEB0).

- Les messages FIN envoyés dans l’environnement de test (*Test and Training*) doivent obligatoirement utiliser des BIC de test (BIC0) pour l’expéditeur et le destinataire (blocs 1 et 2). Toutefois, le corps du message peut contenir des BIC Live ou des BIC de test pour identifier les agents.
- Les messages de paiement ISO 20022 envoyés dans l’environnement de test doivent contenir des BIC Live dans les champs expéditeur/destinataire (DN du demandeur et du répondant dans l’en-tête technique). Toutefois, la charge utile (*payload*) peut contenir des BIC Live ou des BIC de test.
- Les requêtes API v5/v6 peuvent contenir des BIC Live ou des BIC de test.
- Les mises à jour effectuées dans la GUI peuvent contenir des BIC Live ou des BIC de test, mais uniquement pour l’agent destinataire du transfert (*forwarded-to agent*).

Afin d’offrir aux utilisateurs la flexibilité nécessaire pour combiner différents formats de canaux dans l’environnement de test et de prendre en charge les cas où des BIC Live et des BIC de test sont utilisés simultanément, Tracker convertit les BIC Live présents dans la charge utile des messages en leurs BIC de test correspondants pour le traitement des mises à jour de statut des paiements.

Cette conversion est effectuée quel que soit le canal par lequel la mise à jour est reçue par Tracker.

Tracker utilise une table de correspondance interne pour effectuer ces conversions de BIC.

**Remarque :** Les BIC Live sont convertis en BIC de test de 8 caractères aussi bien lorsqu’il s’agit d’un BIC Live de 11 caractères que d’un BIC Live de 8 caractères.

**Remarque :** Dans le cas peu probable où, pour des raisons techniques, certains BIC Live d’agents (émetteur du statut / agent donneur d’instruction ou agent destinataire du transfert / agent instruit) ne pourraient pas être convertis en leurs équivalents de test, Tracker ne serait pas en mesure de traiter ces événements de mise à jour de statut de paiement. Ceux-ci seraient alors invalidés silencieusement.

Les autres agents identifiés dans un message de paiement au moyen de BIC Live ne disposant pas de BIC de test sont enregistrés tels quels. Ils ne sont pas identifiés comme agents GPI et ne reçoivent aucune notification Tracker.

Pour les paiements ISO 20022 ou les mises à jour de statut trck.001, les BIC Live présents dans l’en-tête du message et dans la charge utile sont convertis en BIC de test (BIC0) avant le traitement par Tracker.

L’expéditeur et le destinataire d’un message pacs.008 dans l’environnement pilote (environnement de test) sont identifiés par des BIC Live dans l’en-tête technique. Toutefois, la charge utile du message peut contenir des BIC Live ou des BIC de test.

Tracker convertit les BIC Live en BIC de test et les enregistre dans les informations de transaction Tracker.

Si le destinataire d’un message FIN MT 103 (qui doit être identifié par un BIC de test dans l’environnement Test and Training) envoie une mise à jour à Tracker au moyen d’un message ISO 20022 trck.001, Tracker accepte cette mise à jour, que l’émetteur du statut ou l’agent destinataire du transfert soit identifié par un BIC de test (BIC0) ou par son BIC Live équivalent. Dans ce dernier cas, ces BIC sont convertis en BIC de test lors de leur traitement par Tracker.

## Conversion des BIC Live en BIC de test pour le traitement par Tracker

Il est possible que plusieurs BIC de test soient définis pour un même BIC Live.

Par conséquent, lorsque Tracker convertit des BIC Live en leurs BIC de test équivalents (BIC0), il sélectionne le BIC de test de la manière suivante :

- Si un seul BIC de test est configuré pour le BIC Live, l’utilisateur doit utiliser ce BIC.
- Si plusieurs BIC de test sont configurés, Tracker sélectionne le premier BIC de test trouvé lors d’une recherche par ordre alphabétique.

Pour plus d’informations sur la configuration des BIC de test, consultez le *FIN Operations Guide*.

Lorsqu’un utilisateur consulte des transactions de test dans l’interface graphique Basic Tracker, les agents apparaissent dans la ligne de métro avec leurs BIC de test.

Pour faciliter les tests dans l’environnement de test, Swift recommande aux clients de s’assurer que leurs BIC de test sont correctement configurés.

Pour tester les messages ISO 20022, Swift recommande d’utiliser des BIC Live dans la charge utile des messages. Ceux-ci peuvent également être utilisés, de manière facultative, dans la charge utile des messages FIN liés à la même transaction, afin de simplifier les opérations.

Pour les messages traités par Transaction Manager, lorsque une ou plusieurs étapes de la transaction utilisent des BIC de test dans la charge utile, tandis que d’autres étapes utilisent des BIC Live, le traitement résultant par Transaction Manager peut produire des résultats inattendus.

Cela s’explique par le fait que l’application correcte des règles de validation métier et des règles d’intégrité des données repose sur une correspondance exacte et individuelle des BIC.

Par conséquent, Swift recommande vivement d’utiliser des BIC Live dans la charge utile des messages à des fins de test.

À la fin de la période de migration ISO 20022 pour les paiements (2025), les BIC de test ne sont plus autorisés dans la charge utile des messages sur les services FINplus Test.

Pour plus d’informations, consultez la documentation *FINplus Service Description*.

## Exemple

Le paiement comporte trois étapes. Chaque étape est traitée comme un transfert de crédit client Swift GPI. Toutes les banques de la chaîne sont des banques GPI :

- Banque A → ISO pacs.008 → Banque B
- Banque B → FIN MT 103 → Banque C
- Banque C → trck.001 → Tracker (ou MT 199 en alternative)

La banque A utilise des BIC Live dans l’en-tête et dans le corps du message pacs.008, conformément à la recommandation.

La banque B utilise des BIC Live dans le corps du message MT 103, mais doit utiliser des BIC de test dans l’en-tête. Les BIC de test sont également autorisés dans le corps du message.

La banque C utilise des BIC Live dans l’en-tête et dans le corps du message trck.001. Les BIC de test sont également autorisés dans le corps du message.

**Étape 1 : pacs.008 de la banque A (ABDCDEFX) vers la banque B (ABCDGB2L)**

Exemple de message XML :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AppHdr xmlns="urn:iso:std:iso:20022:tech:xsd:head.001.001.02"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Fr>
    <FIId>
      <FinInstnId>
        <BICFI>ABDCDEFXXXX</BICFI>
      </FinInstnId>
    </FIId>
  </Fr>
  <To>
    <FIId>
      <FinInstnId>
        <BICFI>ABCDGB2LXXX</BICFI>
      </FinInstnId>
    </FIId>
  </To>
  <BizMsgIdr>MSG200206/111185</BizMsgIdr>
  <MsgDefIdr>pacs.008.001.08</MsgDefIdr>
  <BizSvc>swift.cbprplus.02</BizSvc>
  <CreDt>2022-08-22T11:10:31-05:00</CreDt>
</AppHdr>
<Document xmlns:pacs="urn:iso:std:iso:20022:tech:xsd:pacs.008.001.08">
  <FIToFICstmrCdtTrf>
    <GrpHdr>
      <MsgId>MSG200206/111185</MsgId>
      <CreDtTm>2022-08-22T00:00:00+00:00</CreDtTm>
      <NbOfTxs>1</NbOfTxs>
      <SttlmInf>
        <SttlmMtd>INDA</SttlmMtd>
      </SttlmInf>
    </GrpHdr>
    <CdtTrfTxInf>
      <PmtId>
        <InstrId>MSG200206/111185</InstrId>
        <EndToEndId>MSG000001/000008</EndToEndId>
        <UETR>21b671f2-c0c8-4d78-8f98-981fbcb85248</UETR>
      </PmtId>
      <IntrBkSttlmAmt Ccy="USD">500</IntrBkSttlmAmt>
      <IntrBkSttlmDt>2022-08-22</IntrBkSttlmDt>
      <InstdAmt Ccy="USD">500</InstdAmt>
      <ChrgBr>SHAR</ChrgBr>
      <InstgAgt>
        <FinInstnId>
          <BICFI>ABDCDEFXXXX</BICFI>
        </FinInstnId>
      </InstgAgt>
      <InstdAgt>
        <FinInstnId>
          <BICFI>ABCDGB2LXXX</BICFI>
        </FinInstnId>
      </InstdAgt>
      <Dbtr>
        <Nm>BEST AMERICAN COOKIES</Nm>
        <PstlAdr>
          <AdrLine>27 Sea Drive</AdrLine>
          <AdrLine>CA 92101 San Diego</AdrLine>
          <AdrLine>United States</AdrLine>
        </PstlAdr>
      </Dbtr>
      <DbtrAcct>
        <Id>
          <Othr>
            <Id>451822890</Id>
          </Othr>
        </Id>
      </DbtrAcct>
      <DbtrAgt>
        <FinInstnId>
          <BICFI>ABDCDEFXXXX</BICFI>
        </FinInstnId>
      </DbtrAgt>
      <CdtrAgt>
        <FinInstnId>
          <BICFI>WXYZUS33XXX</BICFI>
        </FinInstnId>
      </CdtrAgt>
      <Cdtr>
        <Nm>CHOCOBEL</Nm>
        <PstlAdr>
          <AdrLine>Rue Royale 21</AdrLine>
          <AdrLine>1000 Brussels</AdrLine>
          <AdrLine>Belgium</AdrLine>
        </PstlAdr>
      </Cdtr>
      <CdtrAcct>
        <Id>
          <Othr>
            <Id>171864959</Id>
          </Othr>
        </Id>
      </CdtrAcct>
    </CdtTrfTxInf>
  </FIToFICstmrCdtTrf>
</Document>
```

## Étape 2 : MT 103 de la banque B (ABCDGB2L) vers la banque C (WXYZUS33), avec des BIC de test dans l’en-tête

**Expéditeur :** ABCDGB20XXX (BIC réservé à l’environnement Test and Training).

**Destinataire :** WXYZUS30XXX (BIC réservé à l’environnement Test and Training).

```text
{121:21b671f2-c0c8-4d78-8f98-981fbcb85248}

:20:ABCD1234WXYZ

:23B:CRED

:32A:220822USD470,

:33B:USD500,

:50K:/451822890

BEST AMERICAN COOKIES

27 Sea Drive

CA 92101 San Diego

United States

:52A:ABDCDEFXXXX

:59:/171864959

CHOCOBEL

Rue Royale 21

1000 Brussels

Belgium

:70:/RFB/MSG000001/000008

:71A:SHA

:71F:USD30,
```

## Étape 3 : trck.001 de la banque C (WXYZUS33) vers le BIC Live de Tracker (TRCKCHZZ)

Exemple de message XML :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AppHdr xmlns="urn:iso:std:iso:20022:tech:xsd:head.001.001.02"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Fr>
    <FIId>
      <FinInstnId>
        <BICFI>WXYZUS33XXX</BICFI>
      </FinInstnId>
    </FIId>
  </Fr>
  <To>
    <FIId>
      <FinInstnId>
        <BICFI>TRCKCHZZXXX</BICFI>
      </FinInstnId>
    </FIId>
  </To>
  <BizMsgIdr>WXYZ9876TRCK</BizMsgIdr>
  <MsgDefIdr>trck.001.001.03</MsgDefIdr>
  <BizSvc>swift.uc.01</BizSvc>
  <CreDt>2022-08-22T11:10:31-05:00</CreDt>
</AppHdr>
<Document xmlns="urn:swift:xsd:trck.001.001.03"
          xmlns:si="http://www.w3.org/2001/XMLSchema-instance">
  <PmtStsTrckrUpd>
    <GrpHdr>
      <MsgId>WXYZ9876TRCK</MsgId>
    </GrpHdr>
    <TrckrStsAndTx>
      <TxSts>
        <Sts>ACCC</Sts>
      </TxSts>
      <Tx>
        <TrckrInfrmgPty>
          <Id>
            <FinInstnId>
              <BICFI>WXYZUS33XXX</BICFI>
            </FinInstnId>
          </Id>
        </TrckrInfrmgPty>
        <PmtId>
          <InstrId>ABCD12345WXYZ</InstrId>
          <UETR>21b671f2-c0c8-4d78-8f98-981fbcb85248</UETR>
        </PmtId>
        <PmtScnro>CCTR</PmtScnro>
        <ChrgsInf>
          <Amt Ccy="USD">20</Amt>
          <Agt>
            <FinInstnId>
              <BICFI>WXYZUS33XXX</BICFI>
            </FinInstnId>
          </Agt>
        </ChrgsInf>
        <TrckrData>
          <ConfdDt>
            <DtTm>2022-08-22T11:10:00-05:00</DtTm>
          </ConfdDt>
          <ConfdAmt Ccy="USD">450</ConfdAmt>
        </TrckrData>
      </Tx>
    </TrckrStsAndTx>
  </PmtStsTrckrUpd>
</Document>
```

## Étape 3 : alternative avec un MT 199 de la banque C (WXYZUS33) vers Tracker (TRCKCHZZ), en utilisant des BIC de test

Si la banque C utilise un MT 199 comme format de confirmation de crédit au lieu de trck.001, les BIC présents dans l’en-tête du message doivent être des BIC de test.

En revanche, le ou les BIC présents dans le corps du MT 199 peuvent être des BIC de test ou des BIC Live.

Dans cet exemple, le BIC de test est utilisé.

**Expéditeur :** WXYZUS30XXX (BIC réservé à l’environnement Test and Training).

**Destinataire :** TRCKCHZ0XXX (BIC réservé à l’environnement Test and Training).

```text
{121:21b671f2-c0c8-4d78-8f98-981fbcb85248}

:20:INSTRUCT123

:21:ABCD12345WXYZ

:79://202208221110-0500

//ACCC

//WXYZUS30

//USD450,

//:71F:USD20,
```

Si la banque C souhaite utiliser l’API de mise à jour du statut des paiements Universal Confirmations pour confirmer le crédit, au lieu d’utiliser ISO trck.001 ou MT 199, elle peut utiliser des BIC Live ou des BIC de test pour les agents dans la requête API.

Dans l’interface graphique Basic Tracker, lorsqu’un utilisateur de l’une des banques de la chaîne consulte la transaction, il peut voir les agents dans la ligne de métro Basic Tracker identifiés par leurs BIC de test (BIC de 8 caractères se terminant par 0), à condition qu’il dispose d’une visibilité sur les étapes concernées.

# Mentions légales

## Droits d’auteur

Swift © 2026. Tous droits réservés.

## Distribution restreinte

Ne distribuez pas cette publication en dehors de votre organisation, sauf si votre abonnement ou votre commande vous accorde expressément ce droit. Dans ce cas, veillez à respecter toutes les autres conditions applicables.

## Avertissement

Les informations contenues dans cette publication peuvent être modifiées périodiquement.

Vous devez toujours vous référer à la version la plus récente disponible.

## Traductions

La version anglaise de la documentation Swift est la seule version officielle et juridiquement contraignante.

## Marques commerciales

Swift est le nom commercial de S.W.I.F.T. SC.

Les marques suivantes sont des marques déposées de Swift :

- 3SKey ;
- Innotribe ;
- MyStandards ;
- Sibos ;
- Swift ;
- SwiftNet ;
- Le logo Standards Forum ;
- Le logo Swift ;
- Swift GPI avec son logo ;
- Le logo Swift GPI ;
- UETR.

Les autres noms de produits, de services ou de sociétés figurant dans cette publication sont des noms commerciaux, des marques ou des marques déposées appartenant à leurs propriétaires respectifs.

---
