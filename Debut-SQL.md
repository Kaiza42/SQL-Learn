# les debut

# Classification des commande SQL

| **Catégorie** | **Nom complet**                    | **Fonction**                                                                 | **Commandes principales**                         | **Utilisation**                             |
|---------------|------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------|---------------------------------------------|
| **DDL**        | Data Definition Language           | Créer, modifier ou supprimer des objets dans la base                        | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`            | Définir la **structure** des tables         |
| **DML**        | Data Manipulation Language         | Insérer, lire, modifier ou supprimer des données                            | `SELECT`, `INSERT`, `UPDATE`, `DELETE`           | Gérer le **contenu** des tables             |
| **DCL**        | Data Control Language              | Gérer les **droits d’accès** des utilisateurs                               | `GRANT`, `REVOKE`                                | Sécurité et **autorisations**               |
| **TCL**        | Transaction Control Language       | Gérer les **transactions** pour garantir la cohérence des données           | `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `SET TRANSACTION` | Valider ou annuler des modifications groupées |
 

## 🧾 Les types de données en PostgreSQL

| Type SQL         | Description                                      | Exemple de valeur             |
|------------------|--------------------------------------------------|-------------------------------|
| `INT` / `INTEGER`| Entier (32 bits)                                 | `42`                          |
| `BIGINT`         | Grand entier (64 bits)                           | `9223372036854775807`         |
| `SMALLINT`       | Petit entier (16 bits)                           | `32767`                       |
| `SERIAL`         | Entier auto-incrémenté (équivalent à `AUTO_INCREMENT`) | `1`, `2`, `3`, ...    |
| `REAL`           | Nombre à virgule flottante (précision 6 chiffres) | `3.14`                        |
| `DOUBLE PRECISION` | Nombre flottant en double précision (15 chiffres) | `2.718281828459`          |
| `NUMERIC(p,s)`   | Nombre exact avec précision (`p`) et échelle (`s`) | `123.45`, `9999.99`         |
| `VARCHAR(n)`     | Chaîne de caractères avec limite (`n`)           | `'Alice'`                     |
| `CHAR(n)`        | Chaîne fixe de `n` caractères (complétée avec espaces) | `'ABCD    '`             |
| `TEXT`           | Texte de longueur illimitée                      | `'Un long paragraphe...'`     |
| `BOOLEAN`        | Valeur logique `true` ou `false`                 | `true`, `false`               |
| `DATE`           | Date (année-mois-jour)                           | `'2025-04-21'`                |
| `TIMESTAMP`      | Date + heure sans fuseau                         | `'2025-


### 🔐 Contraintes dans une création de table PostgreSQL

| Contrainte             | Description                                                | Exemple SQL                                           |
|------------------------|------------------------------------------------------------|-------------------------------------------------------|
| `PRIMARY KEY`          | Identifiant unique de la table                             | `id SERIAL PRIMARY KEY`                               |
| `FOREIGN KEY`          | Lie une colonne à une autre table                          | `FOREIGN KEY (film_id) REFERENCES films(id)`          |
| `NOT NULL`             | Rend la colonne obligatoire                                | `nom VARCHAR(50) NOT NULL`                            |
| `NULL`                 | Autorise les valeurs vides (valeur par défaut)             | `bio TEXT` ou `bio TEXT NULL`                         |
| `UNIQUE`               | Interdit les doublons                                      | `email VARCHAR(100) UNIQUE`                           |
| `DEFAULT`              | Valeur par défaut si aucune n’est fournie                  | `note INT DEFAULT 0`                                  |
| `CHECK`                | Valide la donnée selon une condition                       | `CHECK (note >= 0 AND note <= 10)`                    |
| `GENERATED ALWAYS AS`  | Colonne générée automatiquement à partir d'une expression  | `age INT GENERATED ALWAYS AS (YEAR(NOW()) - annee_naissance) STORED` |
| `SERIAL` / `BIGSERIAL` | Simule l’auto-incrémentation (`AUTO INCREMENT`)            | `id SERIAL PRIMARY KEY`                               |
| `ON DELETE CASCADE`    | Supprime les lignes liées quand la ligne principale est supprimée | `FOREIGN KEY (...) REFERENCES ... ON DELETE CASCADE` |
| `ON DELETE SET NULL`   | Remplace la clé étrangère par `NULL` en cas de suppression | `FOREIGN KEY (...) REFERENCES ... ON DELETE SET NULL` |
| `ON UPDATE CASCADE`    | Met à jour la clé étrangère si la clé primaire liée change | `FOREIGN KEY (...) REFERENCES ... ON UPDATE CASCADE` |
| `COLLATE`              | Détermine la collation (ordre de tri, casse)               | `nom TEXT COLLATE "fr_FR"`                            |






