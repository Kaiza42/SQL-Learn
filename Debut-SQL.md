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

Une table sans aucune obligation.
```sql
create table Users (
  id int primary key,
  prenom varchar(50) not null,
  nom varchar(50)not null,
  age int not null,
  naissance date null,
  email varchar(50) not null, 
  test numeric null
);
```
Une table avec des obligations exemple not Null et null <br>
``not null`` => ne peut pas etre vide <br>
``null`` => peut etre vide 
```sql
create table Users (
  id int primary key,
  prenom varchar(50) not null,
  nom varchar(50)not null,
  age int not null,
  naissance date null,
  email varchar(50) not null 
);
```