# PSQL 

## commande de conexion PSQL 

| Commande / Option                                  | Description                                                                 |
|----------------------------------------------------|-----------------------------------------------------------------------------|
| `psql`                                             | Lance l’interface PSQL avec l’utilisateur courant                          |
| `psql -U utilisateur`                              | Connexion à PostgreSQL avec un utilisateur spécifique                      |
| `psql -d nom_base`                                 | Se connecter directement à une base de données                             |
| `psql -h hôte -p port -U utilisateur -d base`      | Connexion complète (avec host, port, user, db)                             |
| `psql -W`                                          | Demande le mot de passe manuellement                                       |
| `\c nom_base utilisateur`                          | Changer de base de données (et/ou utilisateur) en session                  |
| `\conninfo`                                        | Affiche les infos de connexion actuelles                                   |
| `psql "postgresql://user:pass@host:port/db"`       | Connexion via URI (très pratique pour les scripts)                         |
| `PGPASSWORD=motdepasse psql -U user -d db`         | Connexion en ligne de commande avec mdp temporaire                         |
| `psql --help`                                      | Liste toutes les options de connexion                                      |

| Commande / Action                                  | Description                                                                 |
|----------------------------------------------------|-----------------------------------------------------------------------------|
| `sudo -i -u postgres`                              | Se connecter à l’utilisateur système `postgres`                            |
| `psql` (dans postgres)                             | Lancer le shell PSQL en tant que superutilisateur                          |
| `psql -U postgres`                                 | Se connecter directement à PostgreSQL en tant que superuser                |
| `CREATE USER nom WITH PASSWORD 'mdp';`             | Créer un utilisateur avec mot de passe                                     |
| `CREATE ROLE nom;`                                 | Créer un rôle vide (pas de login par défaut)                               |
| `ALTER ROLE nom WITH LOGIN PASSWORD 'mdp';`        | Donner le droit de connexion à un rôle                                     |
| `GRANT ALL PRIVILEGES ON DATABASE db TO user;`     | Donner tous les droits sur une base à un utilisateur                       |
| `\du`                                              | Lister les rôles/utilisateurs                                               |
| `DROP USER nom;`                                   | Supprimer un utilisateur                                                   |
| `ALTER USER nom WITH SUPERUSER;`                   | Donner les droits superuser à un utilisateur                               |
| `\password nom_utilisateur`                        | Changer le mot de passe d’un utilisateur                                   |



## les commande PSQL

| Commande                          | Description                                                                 |
|-----------------------------------|-----------------------------------------------------------------------------|
| `\l` ou `\list`                   | Liste toutes les bases de données                                           |
| `\c nom_de_la_base`               | Se connecter à une base de données                                          |
| `\dt`                             | Liste toutes les tables de la base de données courante                      |
| `\d`                              | Liste toutes les relation entre table                                       |
| `\d nom_table`                    | Affiche les détails d'une table (colonnes, types, clés, etc.)               |
| `\du`                             | Liste les rôles (utilisateurs)                                              |
| `\q`                              | Quitter PSQL                                                                |
| `\?`                              | Affiche l’aide des commandes internes de PSQL                               |
| `\conninfo`                       | Affiche les infos de connexion à la base actuelle                           |
| `CREATE DATABASE nom_base;`       | Crée une nouvelle base de données                                           |
| `DROP DATABASE nom_base;`         | Supprime une base de données                                                |
| `CREATE TABLE nom (...);`         | Crée une nouvelle table                                                     |
| `DROP TABLE nom;`                 | Supprime une table                                                          |
| `INSERT INTO table VALUES (...);` | Insère des données dans une table                                           |
| `SELECT * FROM table;`            | Sélectionne toutes les données d’une table                                  |
| `UPDATE table SET ... WHERE ...;` | Modifie des données                                                         |
| `DELETE FROM table WHERE ...;`    | Supprime des données                                                        |
| `ALTER TABLE ...`                 | Modifie une table (ajout de colonne, renommage, etc.)                       |
| `\i chemin/fichier.sql`           | Exécute un script SQL depuis un fichier                                     |
| `\e`                              | Ouvre l’éditeur par défaut pour écrire une requête SQL                      |
| `\timing`                         | Active/désactive le chronométrage des requêtes                              |
| `\watch [secondes]`               | Exécute une commande à intervalle régulier                                  |


## sauvegarde 

| Type de sauvegarde                | Commande exemple                                                    | Description                                                                       |
|----------------------------       |---------------------------------------------------------------      |-----------------------------------------------------------------------------      |
| 🔁 Complète (structure + données) | `pg_dump -U user -d ma_base > full.sql`                             | Sauvegarde toute la base : tables, données, index, etc.                           |
| 📐 Structure uniquement           | `pg_dump -U user -d ma_base --schema-only > structure.sql`          | Sauvegarde uniquement les `CREATE TABLE`, `CREATE INDEX`, etc.                    |
| 💾 Données uniquement             | `pg_dump -U user -d ma_base --data-only > data.sql`                 | Ne contient que les `INSERT INTO`, pas les schémas.                               |
| 🎯 Table spécifique               | `pg_dump -U user -d ma_base -t nom_table > table.sql`               | Sauvegarde uniquement une table spécifique (structure + données).                 |
| 🧩 Format custom (compressé)      | `pg_dump -U user -d ma_base -F c -f base.backup`                    | Format binaire/restaurable avec `pg_restore`, utile pour les gros dumps.          |
| 🧠 Multi-table personnalisée      | `pg_dump -U user -d ma_base -t table1 -t table2 > multi.sql`        | Exporte plusieurs tables spécifiques.                                             |

## restaure
| Type de fichier / sauvegarde        | Commande de restauration                                                                 | Description                                                                 |
|------------------------------------|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| ✅ Base complète (.sql)            | `psql -U user -d base < fichier.sql`                                                      | Restaure toute la base (structure + données)                               |
| 🧩 Format custom (.backup)         | `pg_restore -U user -d base fichier.backup`                                               | Restaure depuis un dump compressé (format `-F c`)                          |
| 📐 Structure uniquement (.sql)     | `psql -U user -d base < structure.sql`                                                    | Restaure uniquement les tables/schéma                                      |
| 💾 Données uniquement (.sql)       | `psql -U user -d base < data.sql`                                                         | Restaure uniquement les données (`INSERT INTO ...`)                        |
| 🎯 Table spécifique (SQL)          | `psql -U user -d base < table_backup.sql`                                                 | Restaure une seule table (structure + données)                             |
| ❌ Supprimer une table avant       | `DROP TABLE nom_table;`                                                                   | Optionnel : si tu veux restaurer une table en la remplaçant complètement   |
| 🔧 Recréer une base vide           | `createdb -U user nom_base`                                                               | Nécessaire avant `pg_restore` si la base n'existe pas encore               |
| 📦 pg_restore : structure seule    | `pg_restore -U user -d base --schema-only fichier.backup`                                | Restaure uniquement les `CREATE TABLE`, etc. depuis un `.backup`           |
| 📦 pg_restore : données seules     | `pg_restore -U user -d base --data-only fichier.backup`                                  | Restaure uniquement les données depuis un `.backup`                        |
| 🔁 pg_restore : table spécifique   | `pg_restore -U user -d base -t nom_table fichier.backup`                                 | Restaure une table précise depuis un dump custom                           |

### cas d'erreure lors de restauration 

| Erreur                            | Cause probable                              | Solution recommandée                             | Commande à utiliser                                             |
|----------------------------------|---------------------------------------------|--------------------------------------------------|-----------------------------------------------------------------|
| Table already exists             | La table est déjà présente dans la base     | Supprimer la table avant de restaurer            | `DROP TABLE nom_table;`                                         |
| Duplicate key violates unique... | Données déjà présentes ou conflits          | Nettoyer les données ou utiliser une base vierge | `TRUNCATE TABLE nom_table;` ou restaurer dans base temporaire   |
| Role does not exist              | Le rôle utilisé dans le dump n'existe pas   | Créer le rôle avec les bons droits               | `CREATE ROLE nom WITH LOGIN PASSWORD 'xxx';`                    |
| Permission denied                | Pas les droits suffisants                   | Utiliser `postgres` ou ajuster les privilèges    | `GRANT ALL PRIVILEGES ON DATABASE ma_base TO mon_user;`         |
| Database already exists          | Tu essayes de recréer une base existante    | Supprimer la base ou en utiliser une autre       | `DROP DATABASE ma_base;` ou `pg_restore -d autre_base fichier`  |
| Foreign key violation            | Conflit d’intégrité entre tables            | Restaurer les tables dans le bon ordre           | `pg_restore -t table1 -t table2 ... fichier.backup`             |
| Syntax error in SQL              | Mauvais format ou fichier dump corrompu     | Vérifier ou régénérer le dump                    | Ouvrir le fichier `.sql` ou refaire le dump avec `pg_dump`      |

# Les droit 

| Type d'objet      | Droits disponibles                                                                                 | Exemple `GRANT`                                                                 |
|-------------------|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **Table**         | SELECT, INSERT, UPDATE, DELETE, TRUNCATE, REFERENCES, TRIGGER                                     | GRANT SELECT, UPDATE ON table_name TO user_name;                                |
| **Colonne (table)**| UPDATE, INSERT (sur colonnes spécifiques uniquement)                                              | GRANT UPDATE (col1, col2) ON table_name TO user_name;                           |
| **Vue**           | SELECT, UPDATE, INSERT, DELETE (si la vue le permet)                                              | GRANT SELECT ON view_name TO user_name;                                         |
| **Séquence**      | SELECT (voir valeur), UPDATE (changer valeur), USAGE (utiliser dans nextval)                      | GRANT USAGE, SELECT ON sequence_name TO user_name;                              |
| **Base de données**| CONNECT, CREATE, TEMP                                                                             | GRANT CONNECT ON DATABASE db_name TO user_name;                                 |
| **Schéma**        | USAGE (accès), CREATE (créer objets dans le schéma)                                               | GRANT USAGE, CREATE ON SCHEMA schema_name TO user_name;                         |
| **Fonction**      | EXECUTE                                                                                           | GRANT EXECUTE ON FUNCTION func_name(args) TO user_name;                         |
| **Langage**       | USAGE                                                                                             | GRANT USAGE ON LANGUAGE plpgsql TO user_name;                                   |
| **Type**          | USAGE                                                                                             | GRANT USAGE ON TYPE custom_type TO user_name;                                   |
| **Foreign Table** | SELECT, INSERT, UPDATE, DELETE                                                                    | GRANT SELECT ON foreign_table_name TO user_name;                                |
| **Aggregate**     | EXECUTE                                                                                           | GRANT EXECUTE ON AGGREGATE agg_name(args) TO user_name;                         |
| **All objets d’un type**| ALL [PRIVILEGES]                                                                            | GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO user_name;              |


## 🔹 Opérateurs de comparaison

| Opérateur   | Description               | Exemple                   |
|-------------|---------------------------|---------------------------|
| `=`         | Égal à                    | `age = 30`                |
| `!=` ou `<>`| Différent de              | `nom <> 'Alice'`          |
| `>`         | Supérieur à               | `salaire > 2000`          |
| `<`         | Inférieur à               | `quantité < 100`          |
| `>=`        | Supérieur ou égal à       | `note >= 10`              |
| `<=`        | Inférieur ou égal à       | `date <= '2023-12-31'`    |

## 🔹 Opérateurs logiques

| Opérateur | Description         | Exemple                              |
|----------|---------------------|--------------------------------------|
| `AND`    | ET logique           | `age > 18 AND ville = 'Paris'`       |
| `OR`     | OU logique           | `ville = 'Paris' OR ville = 'Lyon'`  |
| `NOT`    | Négation             | `NOT (age < 18)`                     |

## 🔹 Opérateurs arithmétiques

| Opérateur | Description     | Exemple               |
|----------|-----------------|------------------------|
| `+`      | Addition         | `prix + taxe`          |
| `-`      | Soustraction     | `total - remise`       |
| `*`      | Multiplication   | `quantité * prix`      |
| `/`      | Division         | `salaire / 12`         |
| `%`      | Modulo (reste)   | `age % 2`              |

## 🔹 Opérateurs spéciaux

| Opérateur     | Description                             | Exemple                           |
|---------------|-----------------------------------------|-----------------------------------|
| `BETWEEN`     | Entre deux valeurs incluses             | `age BETWEEN 18 AND 30`          |
| `IN`          | Dans une liste de valeurs               | `ville IN ('Paris', 'Lyon')`     |
| `LIKE`        | Recherche avec motif                    | `nom LIKE 'A%'`                  |
| `IS NULL`     | Est NULL                                | `adresse IS NULL`                |
| `IS NOT NULL` | N’est pas NULL                          | `adresse IS NOT NULL`            |
| `EXISTS`      | Vérifie l’existence d’un sous-ensemble  | `EXISTS (SELECT 1 FROM ...)`     |

## 🔹 Fonctions d'agrégation SQL

| Fonction   | Description                                      | Exemple                                 |
|------------|--------------------------------------------------|------------------------------------------|
| `COUNT()`  | Compte le nombre de lignes                       | `SELECT COUNT(*) FROM Produit;`          |
| `SUM()`    | Calcule la somme d'une colonne                   | `SELECT SUM(PrixUnit) FROM Produit;`     |
| `MAX()`    | Renvoie la valeur maximale d'une colonne         | `SELECT MAX(PrixUnit) FROM Produit;`     |
| `MIN()`    | Renvoie la valeur minimale d'une colonne         | `SELECT MIN(PrixUnit) FROM Produit;`     |
| `AVG()`    | Calcule la moyenne d'une colonne                 | `SELECT AVG(PrixUnit) FROM Produit;`     |


