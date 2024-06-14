# Projet ACM

## Instructions pour exécuter le projet

1. Clonez les dépôts Git :
   ```sh
   git clone https://github.com/AgriConnectMiage/AgriConnectMiage.git
   cd AgriConnectMiage
   git clone https://github.com/AgriConnectMiage/measurement-service.git
   git clone https://github.com/AgriConnectMiage/watering-service.git
   git clone https://github.com/AgriConnectMiage/api-gateway.git
   git clone https://github.com/AgriConnectMiage/device-monitoring-service.git
   git clone https://github.com/AgriConnectMiage/management-service.git
   git clone https://github.com/AgriConnectMiage/authentication-service.git
   git clone https://github.com/AgriConnectMiage/stats-service.git
   git clone https://github.com/AgriConnectMiage/config-server.git
   git clone https://github.com/AgriConnectMiage/discovery.git
   ```

2. Construisez les images Docker en exécutant la commande suivante :
   ```sh
   docker compose build
   ```

3. Lancez les conteneurs en arrière-plan en exécutant la commande suivante :
   ```sh
   docker compose up -d
   ```

## Documentation des requêtes API

### Actuator API

#### Get All Actuators
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/actuators`
- **Description**: Récupère tous les actionneurs.

#### Get Actuator By ID
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/actuators/:id`
- **Description**: Récupère un actionneur par son ID.
- **Variables**:
  - `id`: UUID de l'actionneur.

#### Get Actuators By Farmer
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/actuators/farmer/:farmerId`
- **Description**: Récupère les actionneurs par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

#### Create Actuator
- **Méthode**: POST
- **URL**: `http://localhost/api/management/actuators?farmerId=:farmerId`
- **Description**: Crée un nouvel actionneur.
- **Header**:
  - `Content-Type: application/json`
- **Query Params**:
  - `farmerId`: UUID du fermier.

#### Delete Actuator
- **Méthode**: DELETE
- **URL**: `http://localhost/api/management/actuators/:id`
- **Description**: Supprime un actionneur par son ID.
- **Variables**:
  - `id`: UUID de l'actionneur.

#### Assign Actuator To Field
- **Méthode**: POST
- **URL**: `http://localhost/api/management/actuators/:id/assign?fieldId=:fieldId`
- **Description**: Assigne un actionneur à un champ.
- **Variables**:
  - `id`: UUID de l'actionneur.
- **Query Params**:
  - `fieldId`: UUID du champ.

#### Unassign Actuator From Field
- **Méthode**: POST
- **URL**: `http://localhost/api/management/actuators/:id/unassign`
- **Description**: Désassigne un actionneur d'un champ.
- **Variables**:
  - `id`: UUID de l'actionneur.

#### Change Actuator State
- **Méthode**: POST
- **URL**: `http://localhost/api/management/actuators/:id/state?state=:state`
- **Description**: Change l'état d'un actionneur.
- **Variables**:
  - `id`: UUID de l'actionneur.
- **Query Params**:
  - `state`: Nouvel état (e.g., `ON`, `OFF`).

#### Find Actuator By Field
- **Méthode**: GET
- **URL**: `http://localhost/api/management/actuators/field/:fieldId`
- **Description**: Trouve des actionneurs par ID de champ.
- **Variables**:
  - `fieldId`: UUID du champ.

### Authentication API

#### Authenticate
- **Méthode**: POST
- **URL**: `http://localhost/api/authentication/auth`
- **Description**: Authentifie un utilisateur.
- **Header**:
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "email": "johndoe@gmail.com",
    "password": "password"
  }
  ```

### Farmer API

#### Get All Farmers
- **Méthode**: GET
- **URL**: `http://localhost/api/management/farmers`
- **Description**: Récupère tous les fermiers.

#### Get Farmer by ID
- **Méthode**: GET
- **URL**: `http://localhost/api/management/farmers/:id`
- **Description**: Récupère un fermier par son ID.
- **Variables**:
  - `id`: UUID du fermier.

#### Get Farmer by Email
- **Méthode**: GET
- **URL**: `http://localhost/api/management/farmers/email?email=:email`
- **Description**: Récupère un fermier par son email.
- **Query Params**:
  - `email`: Adresse email du fermier.

#### Create Farmer
- **Méthode**: POST
- **URL**: `http://localhost/api/management/farmers`
- **Description**: Crée un nouveau fermier.
- **Header**:
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "password": "password123",
    "fieldSize": 3
  }
  ```

#### Update Farmer Password
- **Méthode**: PUT
- **URL**: `http://localhost/api/management/farmers/:id/password?password=:new_password`
- **Description**: Met à jour le mot de passe d'un fermier.
- **Variables**:
  - `id`: UUID du fermier.
- **Query Params**:
  - `password`: Nouveau mot de passe.

#### Delete Farmer by ID
- **Méthode**: DELETE
- **URL**: `http://localhost/api/management/farmers/:id`
- **Description**: Supprime un fermier par son ID.
- **Variables**:
  - `id`: UUID du fermier.

### Field API

#### Get Fields By Farmer
- **Méthode**: GET
- **URL**: `http://localhost/api/management/fields/farmer/:farmerId`
- **Description**: Récupère les champs par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

### Sensor API

#### Get Sensor By ID
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/sensors/:id`
- **Description**: Récupère un capteur par son ID.
- **Variables**:
  - `id`: UUID du capteur.

#### Get Sensors
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/sensors`
- **Description**: Récupère tous les capteurs.

#### Get Sensors By Farmer
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/sensors/farmer/:farmerId`
- **Description**: Récupère les capteurs par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

#### Create Sensor
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors?farmerId=:farmerId`
- **Description**: Crée un nouveau capteur.
- **Header**:
  - `Content-Type: application/json`
- **Query Params**:
  - `farmerId`: UUID du fermier.

#### Delete Sensor
- **Méthode**: DELETE
- **URL**: `http://localhost/api/management/sensors/:id`
- **Description**: Supprime un capteur par son ID.
- **Variables**:
  - `id`: UUID du capteur.

#### Unassign Sensor From Field
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors/:id/unassign`
- **Description**: Désassigne un capteur d'un champ.
- **Variables**:
  - `id`: UUID du capteur.

#### Change Sensor State
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors/:id/state?state=:state`
- **Description**: Change l'état d'un capteur.
- **Variables**:
  - `id`: UUID du capteur.
- **Query Params**:
  -

 `state`: Nouvel état (e.g., `ON`, `OFF`).

#### Change Sensor Interval
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors/:id/interval?interval=:interval`
- **Description**: Change l'intervalle de mesure d'un capteur.
- **Variables**:
  - `id`: UUID du capteur.
- **Query Params**:
  - `interval`: Nouvel intervalle.

#### Update Sensor Measures
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors/:id/measure?temperature=:temperature&humidity=:humidity`
- **Description**: Met à jour les mesures d'un capteur.
- **Variables**:
  - `id`: UUID du capteur.
- **Query Params**:
  - `temperature`: Nouvelle température.
  - `humidity`: Nouvelle humidité.

#### Assign Sensor To Field
- **Méthode**: POST
- **URL**: `http://localhost/api/management/sensors/:id/assign?fieldId=:fieldId`
- **Description**: Assigne un capteur à un champ.
- **Variables**:
  - `id`: UUID du capteur.
- **Query Params**:
  - `fieldId`: UUID du champ.

### Stats API

#### Get All Stats
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements`
- **Description**: Récupère toutes les statistiques de mesures.

#### Get Temperatures and Humidity stats
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements/humidity-temperature`
- **Description**: Récupère les statistiques de température et d'humidité.

#### Get Waterings stats
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements/watering`
- **Description**: Récupère les statistiques d'arrosage.

#### Get stats By Farmer ID
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements/farmer/:farmerId`
- **Description**: Récupère les statistiques par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

#### Get humidity and temperature stats By Farmer ID
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements/farmer/:farmerId/humidity-temperature`
- **Description**: Récupère les statistiques de température et d'humidité par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

#### Get watering stats by farmer
- **Méthode**: GET
- **URL**: `http://localhost/api/stats/measurements/farmer/:farmerId/watering`
- **Description**: Récupère les statistiques d'arrosage par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

### WateringLog API

#### Find All Watering Logs
- **Méthode**: GET
- **URL**: `http://localhost/api/watering/watering-logs`
- **Description**: Récupère tous les journaux d'arrosage.

#### Find Watering Logs By Farmer ID
- **Méthode**: GET
- **URL**: `http://localhost/api/watering/watering-logs/farmer/:farmerId`
- **Description**: Récupère les journaux d'arrosage par ID de fermier.
- **Variables**:
  - `farmerId`: UUID du fermier.

### WateringScheduler API

#### Find Watering Scheduler By Actuator
- **Méthode**: GET
- **URL**: `http://localhost/api/device-monitoring/actuators/:actuatorId/watering-scheduler`
- **Description**: Récupère le programme d'arrosage par ID de l'actionneur.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.

#### Add Manual Watering Scheduler
- **Méthode**: POST
- **URL**: `http://localhost/api/watering/actuators/:actuatorId/watering-scheduler?duration=:duration`
- **Description**: Ajoute un programme d'arrosage manuel.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.
- **Query Params**:
  - `duration`: Durée d'arrosage.

#### Add Intelligent Watering Scheduler
- **Méthode**: POST
- **URL**: `http://localhost/api/watering/actuators/:actuatorId/watering-scheduler/intelligent?duration=:duration&threshold=:threshold`
- **Description**: Ajoute un programme d'arrosage intelligent.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.
- **Query Params**:
  - `duration`: Durée d'arrosage.
  - `threshold`: Seuil d'humidité.

#### Cancel Watering Scheduler
- **Méthode**: POST
- **URL**: `http://localhost/api/watering/actuators/:actuatorId/watering-scheduler/:schedulerId/cancel`
- **Description**: Annule un programme d'arrosage.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.
  - `schedulerId`: UUID du programme d'arrosage.

#### Get Watering Scheduler
- **Méthode**: GET
- **URL**: `http://localhost/api/watering/actuators/:actuatorId/watering-scheduler/:schedulerId`
- **Description**: Récupère un programme d'arrosage par ID de l'actionneur et du programme.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.
  - `schedulerId`: UUID du programme d'arrosage.

#### Trigger Intelligent Watering
- **Méthode**: POST
- **URL**: `http://localhost/api/watering/actuators/:actuatorId/watering-scheduler/:schedulerId/intelligent-watering`
- **Description**: Déclenche un arrosage intelligent.
- **Variables**:
  - `actuatorId`: UUID de l'actionneur.
  - `schedulerId`: UUID du programme d'arrosage.

```

Assurez-vous de remplacer `UUID` par les valeurs appropriées lorsque vous utilisez ces API.
