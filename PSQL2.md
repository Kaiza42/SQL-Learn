# exemple de ligne de commande 

pour lancez : ```psql sudo -i -u postgres```<br>

pour se connecter a l'utilisateur postgres : ```psql -U postgres```<br>

### création d'un utilisateur et modification des role 
créer un utilisateur : ```create user utilisateur with password "1234";```<br>

plusieur ecriture possible pour les droit : ```create user utilisateur with password "1234" SUPERUSER createDB createrole;``` Ici c'est dans la création <br>

sinon on peut lui donner les role apres la création : ```alter user utilisateur with SUPERUSER;``` <br>

pour enlever un role suffit de rajouter NO devant le role exemple : ```alter user utilisateur with NOSUPERUSER``` <br>

pour quitter ```\q```

### création de base de donnée 

pour créer une database : ```create database nom_de_la_db```

créer une database avec un propriétaire : ```create database nom_de_la_db owner utilisateur```

pour consulter vos database : ```\l``` 

pour s'y connecter : ```\c nom_de_la_database``` 

pour se connecter a un utilisateur et une base de donner ```psql -U utilisateur -d nom-de-la-database``` <br>










