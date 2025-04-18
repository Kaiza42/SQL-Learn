# ici seras documenter les jointure en SQL

| Type de JOIN   | Conserve les lignes de...         | Lignes sans correspondance ?         | Valeurs NULL si pas de match |
|----------------|-----------------------------------|--------------------------------------|-------------------------------|
| INNER JOIN     | Seulement celles avec correspondance des deux tables | ❌ Ignorées                           | Non                          |
| LEFT JOIN      | Table de gauche                   | ✅ Oui, celles de gauche sans match  | ✅ Colonnes de droite         |
| RIGHT JOIN     | Table de droite                   | ✅ Oui, celles de droite sans match  | ✅ Colonnes de gauche         |
| FULL JOIN      | Les deux tables                   | ✅ Oui, des deux côtés                | ✅ Colonnes manquantes        |
| CROSS JOIN     | Aucune condition, toutes combinaisons possibles | ✅ Oui, tout croisé                | ❌ Pas de NULL (pas de condition) |


## exemple de jointure 

### Inner Join
```sql
SELECT etudiants.nom, cours.nom_cours
FROM etudiants
INNER JOIN cours ON etudiants.id = coursetudiant_id;
```


### Left Join

```sql
Select etudiants.nom, cours.nom_cours
from etudiants
left join cours on etudiants.id = cours.etudiant_id;
```

### Right Join

```sql 
Select etudiants.nom, cours.nom_cours
FROM etudiants
RIGHT JOIN cours ON etudiants.id = cours etudiant_id;
```




