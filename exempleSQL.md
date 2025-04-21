## création de table 

```sql
create table utilisateurs (
    id serial primary key,
    nom varhcar(50) not null,
    age int
);
```

## ajout de donnée dans une table 

```sql 
insert into utilisateurs (nom,age)
values ('jean',50), ('jacky', 45);
```

## afficher les donnée de ma table 

```sql 
select * from utilisateurs;
```


