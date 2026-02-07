# Application de Suivi de Présence des Employés 

##  Description

Cette application permet le suivi de présence des employés avec un système d'authentification sécurisé. Elle offre une interface web unifiée pour gérer les employés, importer des données de badges depuis des fichiers Excel, et générer des rapports de présence mensuels et journaliers.


##  Technologies Utilisées

- **Backend** : Java 17, Spring Boot 3.2, Spring Security, Spring Data JPA
- **Base de données** : MySQL 8.0
- **Frontend** : HTML5, CSS3, JavaScript ES6, Bootstrap 5
- **Build** : Maven 3.x
- **Import** : Apache POI pour les fichiers Excel

##  Prérequis

- Java 17 ou supérieur
- Maven 3.6 ou supérieur
- MySQL 8.0 ou supérieur
- Navigateur web moderne

##  Installation et Démarrage

### 1. Configuration de la Base de Données

```sql
-- Créer la base de données
CREATE DATABASE attendance_db;

-- Créer l'utilisateur
CREATE USER 'attendance_user'@'localhost' IDENTIFIED BY 'attendance_password';

-- Accorder les privilèges
GRANT ALL PRIVILEGES ON attendance_db.* TO 'attendance_user'@'localhost';
FLUSH PRIVILEGES;
```

### 2. Démarrage de l'Application

```bash
# Cloner ou extraire le projet
cd employee-attendance-v2

# Compiler et démarrer l'application
mvn spring-boot:run
```

L'application sera accessible sur : **http://localhost:8081**

### 3. Connexion

- **URL** : http://localhost:8081
- **Utilisateur** : `admin`
- **Mot de passe** : `admin123`

##  Guide d'Utilisation

###  Connexion

1. Accédez à http://localhost:8081
2. Vous serez automatiquement redirigé vers la page de connexion
3. Saisissez les identifiants : `admin` / `admin123`
4. Cliquez sur "Se connecter"

###  Gestion des Employés

#### Ajouter un Employé
1. Cliquez sur l'onglet "Employés"
2. Cliquez sur "Ajouter Employé"
3. Remplissez le formulaire :
   - **ID Employé** : Identifiant unique (ex: 010)
   - **Nom** : Nom de famille
   - **Prénom** : Prénom
   - **Département** : Service (ex: IT, RH, Finance)
   - **Poste** : Fonction (ex: Développeur, Manager)
   - **Étage** : Numéro d'étage (ex: 2)
4. Cliquez sur "Enregistrer"

#### Modifier un Employé
1. Dans la liste des employés, cliquez sur "Modifier"
2. Modifiez les informations souhaitées
3. Cliquez sur "Enregistrer"

#### Supprimer un Employé
1. Dans la liste des employés, cliquez sur "Supprimer"
2. Confirmez la suppression

### Import des Badges

#### Format du Fichier Excel
Le fichier Excel doit contenir les colonnes suivantes :
- **Colonne A** : ID employé
- **Colonne B** : Nom
- **Colonne C** : Prénom
- **Colonne D** : Date (format DD/MM/YYYY)
- **Colonne E** : Première heure d'entrée (format HH:MM:SS)
- **Colonne F** : Dernière heure de sortie (format HH:MM:SS)
- **Colonne G** : Nombre d'entrées

#### Exemple de Données
```
010 | Mdh | Wassim | 07/07/2025 | 9:49:40 | 18:04:47 | 2
010 | Mdh | Wassim | 08/07/2025 | 9:54:37 | 18:04:47 | 3
010 | Mdh | Wassim | 09/07/2025 | 9:39:27 | 18:04:47 | 6
```

#### Procédure d'Import
1. Cliquez sur l'onglet "Import Badges"
2. Cliquez sur "Choisir un fichier" et sélectionnez votre fichier Excel
3. Cliquez sur "Importer"
4. Un message de confirmation indiquera le nombre de badges importés

###  Génération de Rapports

#### Rapport Mensuel
1. Cliquez sur l'onglet "Rapports"
2. Dans la section "Vue Mensuelle" :
   - Sélectionnez un employé
   - Choisissez l'année et le mois
   - Cliquez sur "Générer Rapport"

**Interprétation** :
- **Vert** : Journée avec 6 heures ou plus de travail
- **Rouge** : Journée avec moins de 6 heures de travail
- **Gris** : Pas de données pour cette journée

#### Rapport Journalier
1. Dans la section "Vue Journalière" :
   - Sélectionnez un employé
   - Choisissez les dates de début et fin
   - Cliquez sur "Générer Rapport"

**Statuts** :
- **Absent** : 0 entrée
- **Présent** : 1 entrée
- **Normal** : 2-3 entrées
- **Fréquent** : Plus de 3 entrées

###  Déconnexion

Cliquez sur "Déconnexion" dans la barre de navigation pour vous déconnecter de l'application.

## 🔧 Configuration Avancée

### Modification du Port
Pour changer le port d'écoute, modifiez le fichier `src/main/resources/application.properties` :
```properties
server.port=8082
```

### Configuration de la Base de Données
Modifiez les paramètres de connexion dans `application.properties` :
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/votre_db
spring.datasource.username=votre_utilisateur
spring.datasource.password=votre_mot_de_passe
```

### Modification des Identifiants de Connexion
Pour changer les identifiants de connexion, modifiez la classe `SecurityConfig.java` :
```java
UserDetails admin = User.builder()
    .username("nouveau_nom")
    .password(passwordEncoder().encode("nouveau_mot_de_passe"))
    .roles("ADMIN")
    .build();
```

##  Dépannage

### L'application ne démarre pas
- Vérifiez que Java 17 est installé : `java -version`
- Vérifiez que Maven est installé : `mvn -version`
- Vérifiez que MySQL est démarré : `sudo systemctl status mysql`

### Erreur de connexion à la base de données
- Vérifiez que la base de données `attendance_db` existe
- Vérifiez les identifiants de connexion dans `application.properties`
- Testez la connexion : `mysql -u attendance_user -p attendance_db`

### Page de connexion inaccessible
- Vérifiez que l'application écoute sur le bon port
- Testez avec curl : `curl -I http://localhost:8081`
- Vérifiez les logs de l'application pour les erreurs

##  Support

Pour toute question ou problème :
1. Consultez les logs de l'application
2. Vérifiez la configuration de la base de données
3. Assurez-vous que tous les prérequis sont installés



