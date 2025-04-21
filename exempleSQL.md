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
