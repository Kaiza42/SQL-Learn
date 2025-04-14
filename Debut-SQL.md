# les debut

## les type
| Type SQL         | Description                                      | Exemple de valeur             |
|------------------|-------------------------------------------------|------------------------------|
| `INT`            | Entier (nombre sans virgule)                    | 42                            |
| `INTEGER`        | Synonyme de INT                                 | 100                           |
| `REAL`           | Nombre à virgule flottante                      | 3.14                          |
| `FLOAT`          | Autre nom pour REAL                             | 2.718                         |
| `NUMERIC`        | Nombre avec précision décimale                  | 123.45                        |
| `VARCHAR(n)`     | Texte (chaîne de caractères, max `n` caractères)| 'Alice'                       |
| `CHAR(n)`        | Texte fixe de `n` caractères                    | 'ABCD'                        |
| `TEXT`           | Texte de longueur illimitée                     | 'Un long paragraphe...'       |
| `DATE`           | Date (AAAA-MM-JJ)                               | '2025-04-12'                  |
| `DATETIME`       | Date + heure                                    | '2025-04-12 14:30:00'         |
| `BOOLEAN`        | Vrai ou faux (1 ou 0 dans SQLite)               | 1 (true), 0 (false)           |
| `BLOB`           | Données binaires (images, fichiers, etc.)       | (image stockée en base)       |


## Table

### les contrainte fans une création de table
|  Contrainte     | Description                                                | Exemple SQL                                          |
|-------------------------|------------------------------------------------------------|------------------------------------------------------|
| `PRIMARY KEY`           | Identifiant unique de la table                             | `id INT PRIMARY KEY`                                 |
| `FOREIGN KEY`           | Lie une colonne à une autre table                          | `FOREIGN KEY (film_id) REFERENCES films(id)`         |
| `NOT NULL`              | Oblige à mettre une valeur                                 | `nom VARCHAR(50) NOT NULL`                           |
| `NULL`                  | Autorise les valeurs manquantes                            | `bio TEXT NULL`                                      |
| `UNIQUE`                | Interdit les doublons                                      | `email VARCHAR(100) UNIQUE`                          |
| `DEFAULT`               | Donne une valeur par défaut                                | `note INT DEFAULT 0`                                 |
| `CHECK`                 | Impose une condition sur les valeurs                       | `CHECK (note >= 0 AND note <= 10)`                   |
| `AUTO INCREMENT`        | Valeur qui s'incrémente automatiquement (SQLite/MySQL)     | `id INTEGER PRIMARY KEY AUTOINCREMENT`               |
| `ON DELETE CASCADE`     | Supprime aussi les lignes liées en cas de suppression      | `FOREIGN KEY (...) REFERENCES ... ON DELETE CASCADE` |
| `ON DELETE SET NULL`    | Remplace par NULL si la ligne liée est supprimée           | `FOREIGN KEY (...) REFERENCES ... ON DELETE SET NULL`|
| `ON UPDATE CASCADE`     | Met à jour automatiquement si la valeur liée change        | `FOREIGN KEY (...) REFERENCES ... ON UPDATE CASCADE` |
| `COLLATE`               | Règle la sensibilité à la casse des comparaisons texte     | `nom TEXT COLLATE NOCASE`                            |

Une table sans aucune contrainte.
```sql
create table Users (
  id int primary key,
  prenom varchar(50) not null,
  nom varchar(50)not null,
  age int not null,
  naissance date null
);
```
Une table avec des contraite exemple not Null et null <br>
``not null`` => ne peut pas etre vide <br>
``null`` => peut etre vide 

```sql
create table Users (
  id int primary key ,
  prenom varchar(50) not null,
  nom varchar(50)not null,
  age int not null,
  naissance date null
);
```
J'ai oublier ``test`` dans l'entité ``Users``

```sql
alter table Users 
add column test varchar(50) not null;
```
Non c'etait pas ``test`` mais ``email``

```sql
alter table Users
rename column test to email;
```
je ne veut plus appeler ma table ``Users`` mais ``membre``

```sql
alter table Users
rename to Membre;
```

si je voudrais suprimer une colonne dans ma table

```sql 
alter table Users 
drop column email;
```

et si je souhaite suprimer une table entière 

```sql 
drop table Users;
```

```sql
CREATE TABLE Flight(
   flight_id UUID PRIMARY KEY,
   flight_departuretime TIMESTAMPTZ NOT NULL,
   flight_arrivaltime TIMESTAMPTZ NOT NULL,
   plane_id UUID NOT NULL,
   check (departure_airport_id <> arrival_airport_id)
   departure_airport_id UUID NOT NULL REFERENCES Airport(airport_id),
   arrival_airport_id UUID NOT NULL REFERENCES Airport(airport_id),
   FOREIGN KEY (plane_id) REFERENCES Plane(plane_id)
);
```

Table Client
CREATE TABLE Customer(
   customer_id UUID PRIMARY KEY,
   customer_lastname VARCHAR(50) NOT NULL,
   customer_firstname VARCHAR(50) NOT NULL,
   customer_mail VARCHAR(64) NOT NULL UNIQUE,
   customer_birth DATE NOT NULL,
   customer_phone VARCHAR(10) NULL UNIQUE,
   customer_password VARCHAR(128) NOT NULL
);
Table Passager
CREATE TABLE Passenger(
   passenger_id UUID PRIMARY KEY,
   passenger_lastname VARCHAR(50) NOT NULL,
   passenger_firstname VARCHAR(50) NOT NULL,
   passenger_mail VARCHAR(64) UNIQUE NULL,
   passenger_passport VARCHAR(9) NOT NULL,
   passenger_gender CHECK(passenger_gender IN ('Male', 'Female', 'Other')) NULL,
   passenger_phone VARCHAR(10) NULL,
   passenger_type CHECK(passenger_type IN ('Adult', 'Kid', 'Baby')) NOT NULL
);
Table Compagnie
CREATE TABLE Airline(
   airline_id UUID PRIMARY KEY,
   airline_name VARCHAR(50) NOT NULL UNIQUE
);
Table pays
CREATE TABLE Country(
   country_id UUID PRIMARY KEY,
   country_name VARCHAR(50) NOT NULL UNIQUE
);
Table Réservation
CREATE TABLE Booking(
   booking_id UUID PRIMARY KEY,
   booking_class VARCHAR(10) CHECK(booking_class IN ('Economy','Business', 'First')) NOT NULL,
   booking_date TIMESTAMP NOT NULL,
   booking_seatnumber VARCHAR(4) NOT NULL UNIQUE,
   passenger_id UUID NOT NULL UNIQUE,
   customer_id UUID NOT NULL UNIQUE,
   FOREIGN KEY (passenger_id) REFERENCES Passenger(passenger_id),
   FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
);
Table Avion
CREATE TABLE Plane(
   plane_id UUID PRIMARY KEY,
   plane_capacity INT NOT NULL,
   plane_model VARCHAR(50) NOT NULL,
   airline_id UUID NOT NULL,
   FOREIGN KEY (airline_id) REFERENCES Airline(airline_id)

);
Table Ville
CREATE TABLE City(
   city_id UUID PRIMARY KEY,
   city_name VARCHAR(50) NOT NULL,
   city_zipcode VARCHAR(10) NOT NULL UNIQUE,
   country_id UUID NOT NULL,
   FOREIGN KEY (country_id) REFERENCES Country(country_id)
);
Table Aéroport
CREATE TABLE Airport(
   airport_id UUID PRIMARY KEY,
   airport_name VARCHAR(80) NOT NULL,
   airport_address VARCHAR(250) NOT NULL UNIQUE,
   airport_gate VARCHAR(5) NOT NULL,
   airport_terminal VARCHAR(5) NOT NULL,
   city_id UUID NOT NULL,
   FOREIGN KEY (city_id) REFERENCES City(city_id)
);
Table Vol
CREATE TABLE Flight(
   flight_id UUID PRIMARY KEY,
   flight_departuretime TIMESTAMPTZ NOT NULL,
   flight_arrivaltime TIMESTAMPTZ NOT NULL,
   arrival_airport_id UUID NOT NULL,
   departure_airport_id UUID NOT NULL,
   plane_id UUID NOT NULL,
   check (departure_airport_id <> arrival_airport_id),
   FOREIGN KEY (departure_airport_id) REFERENCES Airport(airport_id),
   FOREIGN KEY (arrival_airport_id) REFERENCES Airport(airport_id),
   FOREIGN KEY (plane_id) REFERENCES Plane(plane_id)
);
Table historique des réservations et vols
CREATE TABLE Logs(
   flight_id UUID NOT NULL,
   booking_id UUID NOT NULL,
   PRIMARY KEY (flight_id, booking_id),
   FOREIGN KEY (flight_id) REFERENCES Flight(flight_id),
   FOREIGN KEY (booking_id) REFERENCES Booking(booking_id)
);

