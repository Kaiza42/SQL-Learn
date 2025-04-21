## 🧰 Fonctions de formatage utiles en PostgreSQL

| Fonction                                 | Description                                      | Exemple SQL                                                                 | Résultat attendu                     |
|------------------------------------------|--------------------------------------------------|------------------------------------------------------------------------------|--------------------------------------|
| `INITCAP(texte)`                         | Met la première lettre de chaque mot en majuscule| `INITCAP('bonjour le monde')`                                               | `Bonjour Le Monde`                   |
| `UPPER(texte)`                           | Met tout le texte en majuscule                   | `UPPER('chat')`                                                             | `CHAT`                               |
| `LOWER(texte)`                           | Met tout le texte en minuscule                   | `LOWER('ChAt')`                                                             | `chat`                               |
| `TO_CHAR(nombre, format)`                | Formate un nombre comme du texte                 | `TO_CHAR(1234.5, 'FM9999.00')`                                              | `1234.50`                             |
| `TO_CHAR(date, format)`                  | Formate une date                                 | `TO_CHAR(NOW(), 'YYYY-MM-DD HH24:MI')`                                      | `2025-04-21 14:45`                   |
| `ROUND(nombre, décimales)`              | Arrondit un nombre à x décimales                 | `ROUND(12.3456, 2)`                                                         | `12.35`                              |
| `TRIM(texte)`                            | Supprime les espaces en début/fin                | `TRIM('   hello   ')`                                                       | `hello`                              |
| `CONCAT(texte1, texte2)`                 | Concatène plusieurs chaînes                      | `CONCAT('Jean', ' ', 'Dupont')`                                             | `Jean Dupont`                        |
| `COALESCE(valeur1, valeur2)`             | Renvoie la première valeur non nulle             | `COALESCE(NULL, 'Aucune donnée')`                                           | `Aucune donnée`                      |
| `NULLIF(val1, val2)`                     | Renvoie NULL si les deux valeurs sont égales     | `NULLIF(100, 100)`                                                          | `NULL`                               |
| `LENGTH(texte)`                          | Donne la longueur d'une chaîne                   | `LENGTH('bonjour')`                                                         | `7`                                  |
| `EXTRACT(part FROM date)`               | Extrait une partie d'une date (année, mois, etc.)| `EXTRACT(YEAR FROM NOW())`                                                  | `2025`                               |
| `CURRENT_DATE`                           | Date du jour                                     | `SELECT CURRENT_DATE;`                                                      | `2025-04-21`                         |
| `CURRENT_TIME`                           | Heure actuelle                                   | `SELECT CURRENT_TIME;`                                                      | `14:45:33.123456`                    |
| `NOW()`                                  | Date et heure actuelles                          | `SELECT NOW();`                                                              | `2025-04-21 14:45:33.123456+01`      |
