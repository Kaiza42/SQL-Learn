# 📘 Documentation SQL – Utilisateurs & Commandes

---

## Création de la table `utilisateurs`

```sql
-- Création de la table utilisateurs
CREATE TABLE utilisateurs (
    id SERIAL PRIMARY KEY,        -- Identifiant unique auto-incrémenté
    nom VARCHAR(50) NOT NULL,     -- Nom de l'utilisateur (obligatoire)
    age INT                       -- Âge de l'utilisateur
);
```
## insertion de donnée dans la table utilisateur 

```sql
INSERT INTO utilisateurs (nom, age)
VALUES 
  ('Jean', 50),   -- Utilisateur 1
  ('Jacky', 45);  -- Utilisateur 2
```
## affichage des donnée insséré 

```sql
SELECT * FROM utilisateurs;
```

## Création de la table commandes

```sql
CREATE TABLE commandes (
    id SERIAL PRIMARY KEY,                          -- Identifiant unique
    utilisateurs_id INT REFERENCES utilisateurs(id),-- Clé étrangère vers utilisateurs
    produit TEXT NOT NULL,                          -- Nom du produit commandé
    montant NUMERIC(10, 2),                         -- Prix en euros (ex: 49.99)
    date_comande TIMESTAMP DEFAULT CURRENT_TIMESTAMP-- Date de commande générée automatiquement
);
```

## Insertion de plusieurs commandes associées à des utilisateurs
```sql
INSERT INTO commandes (utilisateurs_id, produit, montant)
VALUES 
  (1, 'Clavier', 49.99),    -- Commande pour Jean
  (2, 'Souris', 29.95),     -- Commande pour Jacky
  (1, 'Écran', 199.00);     -- Deuxième commande pour Jean
```

## Affichage des commandes avec le nom des utilisateurs associés
```sql
SELECT 
  u.nom AS "Utilisateur",                                          -- Nom de l'utilisateur
  INITCAP(c.produit) AS "Produit",                                 -- Produit (première lettre en majuscule)
  TO_CHAR(c.montant, 'FM999999.00 €') AS "Montant",                -- Format de montant en euros
  TO_CHAR(c.date_comande, 'YYYY-MM-DD HH24:MI') AS "Date commande" -- Formatage de la date 
FROM commandes c
JOIN utilisateurs u 
  ON c.utilisateurs_id = u.id
ORDER BY c.date_comande DESC; -- Tri des commandes par date décroissante
```
## table des catégories 
```sql
create table categories ( -- création de la table catégories 
    id serial primary key, -- la primary key de categorie autoincrémentée donc UNIQUE 
    nom varchar(100) not null UNIQUE  -- le nom de la categorie en unique ne peut pas etre vide et peut contenir 100 caractère 
    );
```

## table des produits 

```sql
create table produits (  -- création de la table produit 
    id serial primary key,  -- la primary key de produits en serial auto incrémenté donc UNIQUE
    nom varchar(100) not null, -- le nom du produit ne peut pas etre vide et peut etre d'une longueur de 100 caractère 
    prix numeric(10,2) not null check (prix >= 0), -- le prix en numéric donc peut contenir 10 chiffre et suelement 2 apres la virgule le prix ne peut pas etre endessous de 0 
    categorie_id int references produits(id) -- création de la foreign key de categorie id et lien avec produit id 
);
``` 

## ajout de la colonne produit_id dans la table commandes 

```sql
alter table commandes -- alteration de la colonne commandes
add column produit_id int references produits(id);  -- ajout d'une colonne qui contient le produit id 
```

## table des paiement 

```sql
create table paiements ( -- création de la table paiement 
    id serial primary key,  -- id paiement unique en tant que primary key 
    comande_id int unique references commandes(id) on delete cascade, -- clé étrangère de commande dans paiement et se detruit si la commande est annulé ou suprimer  
    montant Numeric(10,2) not null check (montant >= 0), -- montant du paiement ne peut pas etre nul ne peut pas etre endessous de 0 et le type numéric permet 10 chiffre et seulement 2 derriere la virgule 
    date_paiement timestamp default current_timestamp -- la date du paiement par defaut prends la date actuel 
)
```
