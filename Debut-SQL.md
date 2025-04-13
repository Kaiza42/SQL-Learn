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

```SQL
CREATE TABLE Flight(
   flight_id UUID PRIMARY KEY,
   flight_departuretime TIMESTAMPTZ NOT NULL,
   flight_arrivaltime TIMESTAMPTZ NOT NULL,
   arrival_airport_id UUID NOT NULL,
   departure_airport_id UUID NOT NULL,
   plane_id UUID NOT NULL,
   check (departure_airport_id <> arrival_airport_id)
   FOREIGN KEY (departure_airport_id) REFERENCES Airport(airport_id),
   FOREIGN KEY (arrival_airport_id) REFERENCES Airport(airport_id),
   FOREIGN KEY (plane_id) REFERENCES Plane(plane_id)
);
```

