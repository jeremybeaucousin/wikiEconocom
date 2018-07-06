<!-- TITLE: Environnements -->
<!-- SUBTITLE: A quick summary of Environnements -->

# Schémas
## Interactions avec les autres applications
![croisic_interactions_avec_les_autres_applications.png](/uploads/1b806b6544ba52af54b846ad00ece40e/croisic_interactions_avec_les_autres_applications.png.png)

## Interactions avec les bases  de données
![interactions_avec_les_bases_de_données](/uploads/047a3eca111c939c852c9cbe5303084e/interactions_avec_les_bases_de_données.png)

## Interaction avec les modules de l'application
![interaction_avec_les_modules_de_l_application](/uploads/fc12be3e39ab7c492afb82f5bd4effe6/interaction_avec_les_modules_de_l_application.png)
 
## Découpage de l'application
![Découpage_de_l_application](/uploads/39af010aeb7d50a9522909ad000d85ea/Découpage_de_l_application.png)

# Échanges
##  Format des échanges :
Les échanges d’information entre CROISIC et les autres applications sont effectués directement en base de données (Interface ETL : Extract Transform Load) ou via des transferts de fichiers (.csv, .ini, etc.). Les informations provenant de la base de données sont fournis par l’intermédiaire de vues accessibles avec le compte utilisé par CROISIC.
2.4.1.	HOEDIC
Hiérarchie des Objets Et Définition des Inventaires Commun. Inventaire du réseau, de la sécurité et des services. Référentiel des liaisons et des matériels pour la DISIT. Ce référentiel gère l’intégrité des données sur le réseau. SAT est une base de données regroupant un ensemble de référentiel de la DISIT.

**Interface ETL**
* **V_CRO_HOE_REF_SITE** : liste des sites;
* **V_CRO_HOE_ENT_TEMP** : liste des entités temporaire ;
* **V_CRO_HOE_ABO_LAN** : liste des LAN : 
	* En création, modification, à conserver
	* Ayant un produit détaillé fonctionnel ou technique de renseigné
	* Des interventions en P10, P11
	* De l’intervention ayant la date de réalisation la plus récente si le LAN concerne plusieurs interventions
* V_CRO_HOE_ABO_SNOW: liste des abonnés : 
	* Des interventions en P8, P9
	* Des interventions ayant eu une génération ini à destination d’OC2E
 
**Transferts de Fichier**
* **croisic_hoedic_abonnelan_previ.csv** : Liste des abonnes LAN de la base de données du planning de CROISIC;
* **croisic_hoedic_abonnegab_previ.csv** : Liste des abonnes GAB de la base de données du planning de CROISIC;
* **croisic_hoedic_equipement_previ.csv** : Liste des équipements de la base de données du planning de CROISIC;
* **croisic_hoedic_liaison_previ.csv** : Liste des liaisons de la base de données du planning de CROISIC ;
* **croisic_hoedic_entite_temporaire.csv** : Liste des entités de la base de données du planning de CROISIC ;
* **croisic_hoedic_site.csv** : Liste des sites de la base de données du planning de CROISIC ;

### AXITEL
Base des références techniques et commerciales des liaisons Télécoms. L’application CROISIC envoie à SPOT les informations nécessaires à une commande de liaisons. Cette application remplace les outils de commande DFI-AT et permet de commander les liaisons chez les opérateurs concernés.
**Transferts de Fichier**
* **axitel_croisic_commande_ yyyymmddHHmmssSSS.csv** : Contient les retours d’informations sur les commandes ou résiliation de liaisons;
* **croisic_axitel_commande_ yyyymmddHHmmssSSS.csv** : Contient les commandes ou résiliation de liaisons demandées par l’utilisateur;
* **croisic_axitel_entite_temporaire_ yyyymmddHHmmssSSS.csv** : Contient les entités en cours de régularisation de leur code régate ;

### OC2E
Outil de configuration des équipements ECRIN. L’application CROISIC envoie à OC2E des fichiers qui permettent à cette application de configurer les équipements.
**Transferts de Fichier**
* **<nom_normalisé_equipement>.ini** : Contient les informations sur l’équipement concerné nécessaires à sa configuration pour OC2E.
**Web service**
* **getEcho** : Méthode de test pour savoir si le service web fonctionne bien ;
* **validerRealisation** : Service permettant de valider (ou non) un déploiement.
* **retourRadio** : Service permettant de valider (ou non) la configuration du DHCP ;
* **retourConfigurationCw** : Service permettant de valider (ou non) la configuration d'une borne dans les contrôleurs.
* **retourFingerprint** : Service permettant de valider (ou non) l'activation/désactivation du fingerprint d'une borne.
* **retourDhcp** : Service permettant de valider (ou non) la configuration d'un SR de collecte dans le DHCP.
* **retourConfigurationAuto** : Service pour le retour OC2E pour la configuration automatique d'un équipement.
* **ext_PostIni.php** : Envoi de fichiers INI.
* **ext_GenConfMini.php** : Génération de configurations routeurs minimales ;
* **ext_PlanifOperationAuto.php** : Demande de réalisation d’une opération automatique ;
* **ext_AffLogsOperationAuto.php** : Affichage des logs d’une opération automatique

### TAHITI
Application responsable de collecter des statistiques.
**Transferts de Fichier**
* **CROISIC_TAHITI*.*** : Données statistiques.

### IPAM
Base de gestion des sous-réseaux pour le déploiement de nouveaux équipements. L’application CROISIC demande à l’IPAM un sous-réseau disponible pour la mise en place d’un nouvel équipement et la réservation de ce sous-réseau, ainsi que la libération d’un sous-réseau lors de la suppression d’un équipement. La communication entre l’IPAM et CROISIC se fait par l’intermédiaire de plusieurs web services l’IPAM.
**Web service**
* **laposte_get_ip_not_used_php** : Ce web service permet de demander à l’IPAM un sous-réseau non utilisé ;
* **laposte_control_format_php** : Ce web service permet de valider une adresse de sous-réseau (selon les règles d’adressage de la DISIT) et de connaître son état (libre ou non). Il n’est pas utilisé par CROISIC à ce jour.
* **laposte_delete_flag_php** : Ce web service permet d’informer l’IPAM de la libération d’un sous-réseau.
* **laposte_get_loopback_not_used_php** : Ce web service permet de demander à l’IPAM un sous-réseau loopback libre et le sous-réseau interco libre associé.
* **laposte_get_vr_not_used_php** : Ce web service permet de demander à l’IPAM un sous-réseau loopback VR libre et le sous-réseau interco VR libre associé.
* **laposte_reserve_ip_php** : Ce web service permet de demander à l’IPAM la réservation d’un sous-réseau.

### OUESSANT
Application responsable de la gestion et de la centralisation des Login/Password des équipements du réseau, des connections et des acteurs. L’application CROISIC interagit avec OUESSANT par l’intermédiaire d’un web service OUESSANT.
L’application CROISIC envoie au web service de l’application OUESSANT le Login/Password de l’utilisateur qui tente de s’identifier. Si l’authentification est positive, CROISIC reçoit en retour des informations sur l’utilisateur sous forme de flux XML. Celles-ci permettent d’identifier le rôle applicatif de l’utilisateur dans CROISIC.


# Documents de références
[CROISIC_DAT_Dossier_Architecture_Technique_9.1.docx](/uploads/a3529e272b59d7cd067413f3a44d34b6/CROISIC_DAT_Dossier_Architecture_Technique_9.1.docx)