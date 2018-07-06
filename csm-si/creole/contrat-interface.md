<!-- TITLE: Contrat d'interface -->
<!-- SUBTITLE: A quick summary of Creole -->

# Guide d'utilisation des routes

## Intoduction

---

Dans le cadre de la refonte de l'API Rest CreoleV2, deux types de routes ont été définis :

* [Les routes spécifiques](##-Routes-specifiques), utilisé pour la réalisation de certaines actions plus élaboré ou comme tampon (evite le nom des tables directement renseigné dans l'URL)
* [Les routes passe-plat](##-Routes-passe-plat), liens direct avec la base de donnée disposants des methodes GET, PUT, POST, DELETE

---

## Routes specifiques

---

### Envoi une liste de partenaire dans la table management subscription via un POST

|||
|:----:|:----:|
|/manage_subscription| `POST`|

```json
    [{
        "id":null,
        "address_ip": "999.999.999.999/17",
        "comment": "-",
        "date_archive": null,
        "date_create": "2017-02-16T11:14:00",
        "eh_id": 2,
        "en_production": "OUI",
        "libelle": "Unknown",
        "metier_id": "OK",
        "nat_ip": "85.85.85.85/17",
        "number_abonment": 9013,
        "type": "GBE2",
        "user_archive": null,
        "user_create": 61
    },{...}]
```

---

### Met à jour une liste de partenaire dans la table management subscription via un PUT

|||
|:----:|:----:|
|/manage_subscription/<int:sub_id> | `PUT`|

```json
    [{
        "id":2140,
        "address_ip": "999.999.999.999/17",
        "comment": "-",
        "date_archive": null,
        "date_create": "2017-02-16T11:14:00",
        "eh_id": 2,
        "en_production": "OUI",
        "libelle": "Unknown",
        "metier_id": "OK",
        "nat_ip": "85.85.85.85/17",
        "number_abonment": 9013,
        "type": "GBE2",
        "user_archive": null,
        "user_create": 61
    },{...}]
```

---

### Gere les actions necessaires à l'identification du fichier de configuration en production

|||
|:----:|:----:|
|/host_managment_file/<int:file_id> | `PUT`|

```json
    [{
        "file_id":2140,
        "file_generation_storage_name":"20161024_093106_CentralPolicy-PASIV2-ref-test.txt"
    }]
```

---

### Envoi une liste d'utilisateurs dans la table users via un POST

|||
|:----:|:----:|
|/manage_users | `POST`|

```json
    [{
        "id":null,
        "IDRH":"gbe",
        "email": "facile@creole.api",
        "name":"test",
        "username":"gbe",
        "roles": "ROLE_BDD,ROLE_AUTRE",
        "password": "pwd",
        "last_connection_time": "0001-01-01T00:00:00",
        "salt": "fs3ov0rjvdkcc0k4008w40s0g8asck8",
        "time_created": 15448986,
        "isEnabled": true,
        "confirmationToken": "",
        "timePasswordResetRequested": 1566895,
        "disabledDate": "0001-01-01T00:00:00"
    },{...}]
```

---

### Envoi une liste de flux dans la table rule_configuration_data via un POST

|||
|:----:|:----:|
|/manage_flux_data_conf | `POST`|

```json
    [{
        "id":null,
        "date_create": "2016-11-09T16:12:35",
        "date_delete": null,
        "destination": "test.gbe.list669",
        "direction": 1,
        "eh_id": 3,
        "management_subscription_id": 1481,
        "partenaire_record": null,
        "port": 787,
        "protocole": 1,
        "record": 1481,
        "source": "10.241.16.0/27",
        "type": 2,
        "user_create": 4,
        "user_delete": null
    },{...}]
```

---

### Effectue la demande de generation de fichier et la validation de la conservation de celui-ci

|||
|:----:|:----:|
|/generate_configuration_file/<int:file_id>-<int:eh_id> | `POST - PUT`|

```json
    [{
        "file_id":7,
        "eh_id":18,
        "save_file":true,
        "new_file_name":"20161024_093106_CentralPolicy-PASIV2-ref-test.txt"
    }]
```

---

## Routes passe-plat

|Table |Routes|Methodes|
| ---- | ---- | ---- |
|**file**|/api1/file | `GET - POST`|
|**file**|/api1/file/<int:uid>| `PUT - DELETE`|
|**rule_configuration_data**|/api1/rule_configuration_data | `GET - POST`|
|**rule_configuration_data**|/api1/rule_configuration_data/<int:uid> | `PUT - DELETE`|
|**management_subscription**|/api1/management_subscription | `GET - POST`|
|**management_subscription**|/api1/management_subscription/<int:uid> | `PUT - DELETE`|
|**metier**|/api1/metier | `GET - POST`|
|**metier**|/api1/metier/<int:uid> | `PUT - DELETE`|
|**users**|/api1/users | `GET - POST`|
|**users**|/api1/users/<int:uid> | `PUT - DELETE`|
|**domain**|/api1/domain | `GET - POST`|
|**domain**|/api1/domain/<int:uid> | `PUT - DELETE`|
|**rule_condition**|/api1/rule_condition | `GET - POST`|
|**rule_condition**|/api1/rule_condition/<int:uid> | `PUT / DELETE`|
|**rule_subnet**|/api1/rule_subnet | `GET - POST`|
|**rule_subnet**|/api1/rule_subnet/<int:uid> | `PUT - DELETE`|
|**rule_type_category**|/api1/rule_type_category | `GET - POST`|
|**rule_type_category**|/api1/rule_type_category/<int:uid> | `PUT - DELETE`|
|**rule_protocole**|/api1/rule_protocole | `GET - POST`|
|**rule_protocole**|/api1/rule_protocole/<int:uid> | `PUT - DELETE`|
|**file_generation**|/api1/file_generation | `GET - POST`|
|**file_generation**|/api1/file_generation/<int:uid> | `PUT - DELETE`|
|**file_production_versionning**|/api1/file_production_versionning | `GET - POST`|
|**file_production_versionning**|/api1/file_production_versionning/<int:uid> | `PUT - DELETE`|