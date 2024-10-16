
# Guide SQL pour les Entretiens

## Table des Matières
1. DDL (Data Definition Language)
2. DML (Data Manipulation Language)
3. DQL (Data Query Language)
4. DCL (Data Control Language)
5. TCL (Transaction Control Language)
6. Types de données en SQL
7. Opérateurs SQL
8. Fonctions en SQL

---

## DDL (Data Definition Language)

### 1. Qu'est-ce que le DDL ?
Le DDL est le sous-ensemble de SQL utilisé pour définir et modifier la structure des objets de la base de données, comme les tables et les index. Les commandes principales du DDL sont `CREATE`, `ALTER`, `DROP`, et `TRUNCATE`.

### 2. Quelle est la différence entre `DROP` et `TRUNCATE` ?
- `DROP` supprime une table de la base de données ainsi que toutes les données qu'elle contient, sans possibilité de récupération.
- `TRUNCATE` supprime toutes les lignes d'une table, mais la table elle-même est conservée, avec sa structure intacte.

### 3. Quand utiliser `ALTER` ?
`ALTER` est utilisé pour modifier la structure d'une table existante, par exemple pour ajouter une colonne, modifier son type ou en supprimer une.

### 4. Comment créer une table en SQL ?
```sql
CREATE TABLE employes (
    id INT PRIMARY KEY,
    nom VARCHAR(50),
    poste VARCHAR(50),
    salaire DECIMAL(10, 2)
);
```

### 5. Peut-on ajouter une contrainte à une table existante ?
Oui, avec la commande `ALTER TABLE` :
```sql
ALTER TABLE employes
ADD CONSTRAINT chk_salaire CHECK (salaire > 0);
```

---

## DML (Data Manipulation Language)

### 1. Qu'est-ce que le DML ?
Le DML est utilisé pour manipuler les données d'une base, incluant les commandes `INSERT`, `UPDATE`, `DELETE`.

### 2. Comment insérer des données dans une table ?
```sql
INSERT INTO employes (id, nom, poste, salaire)
VALUES (1, 'Jean', 'Développeur', 45000);
```

### 3. Quelle est la différence entre `DELETE` et `TRUNCATE` ?
`DELETE` supprime des lignes spécifiques d'une table en fonction d'une condition, alors que `TRUNCATE` supprime toutes les lignes sans condition. De plus, `DELETE` peut être annulé avec `ROLLBACK`, pas `TRUNCATE`.

### 4. Comment mettre à jour des données dans une table ?
```sql
UPDATE employes
SET salaire = 48000
WHERE id = 1;
```

### 5. Peut-on utiliser des sous-requêtes avec `UPDATE` ?
Oui, comme ceci :
```sql
UPDATE employes
SET salaire = (SELECT MAX(salaire) FROM employes)
WHERE poste = 'Manager';
```

---

## DQL (Data Query Language)

### 1. Qu'est-ce que le DQL ?
Le DQL concerne principalement la commande `SELECT`, qui permet de récupérer des données à partir d'une ou plusieurs tables.

### 2. Comment récupérer toutes les données d'une table ?
```sql
SELECT * FROM employes;
```

### 3. Comment récupérer des colonnes spécifiques d'une table ?
```sql
SELECT nom, poste FROM employes;
```

### 4. Qu'est-ce qu'une clause `WHERE` ?
`WHERE` est utilisée pour filtrer les résultats en fonction de certaines conditions :
```sql
SELECT * FROM employes WHERE salaire > 30000;
```

### 5. Quelle est la différence entre `INNER JOIN` et `LEFT JOIN` ?
- `INNER JOIN` renvoie uniquement les lignes qui ont des correspondances dans les deux tables.
- `LEFT JOIN` renvoie toutes les lignes de la table de gauche et les lignes correspondantes de la table de droite. Si aucune correspondance n'est trouvée, les colonnes de droite seront `NULL`.

---

## DCL (Data Control Language)

### 1. Qu'est-ce que le DCL ?
Le DCL concerne les commandes liées aux droits et permissions sur les objets de la base de données. Les commandes principales sont `GRANT` et `REVOKE`.

### 2. Comment donner des permissions à un utilisateur ?
```sql
GRANT SELECT, INSERT ON employes TO 'utilisateur';
```

### 3. Comment retirer des permissions ?
```sql
REVOKE INSERT ON employes FROM 'utilisateur';
```

### 4. Qu'est-ce qu'une commande `GRANT ALL` ?
Cette commande accorde tous les privilèges disponibles à un utilisateur sur un objet particulier :
```sql
GRANT ALL ON employes TO 'admin';
```

---

## TCL (Transaction Control Language)

### 1. Qu'est-ce que le TCL ?
Le TCL gère les transactions dans une base de données. Les commandes principales sont `COMMIT`, `ROLLBACK`, et `SAVEPOINT`.

### 2. Quelle est la fonction de `COMMIT` ?
`COMMIT` valide les changements faits dans une transaction et les rend permanents dans la base de données.

### 3. Que fait `ROLLBACK` ?
`ROLLBACK` annule une transaction non validée, rétablissant l'état précédent des données.

### 4. Comment utiliser un point de sauvegarde (`SAVEPOINT`) ?
```sql
SAVEPOINT point1;
UPDATE employes SET salaire = salaire + 1000 WHERE id = 1;
ROLLBACK TO point1;
```

---

## Types de données en SQL

### 1. Quels sont les principaux types de données en SQL ?
- **INT** : Entiers
- **VARCHAR** : Chaîne de caractères de longueur variable
- **DECIMAL** : Nombres à virgule fixe
- **DATE** : Dates
- **BOOLEAN** : Vrai ou faux

### 2. Quelle est la différence entre `CHAR` et `VARCHAR` ?
`CHAR` a une longueur fixe, tandis que `VARCHAR` a une longueur variable. Si une chaîne de caractères est plus courte que la longueur définie pour `CHAR`, elle sera remplie avec des espaces.

### 3. Comment déclarer une colonne comme clé primaire ?
```sql
id INT PRIMARY KEY;
```

---

## Opérateurs SQL

### 1. Quels sont les principaux opérateurs en SQL ?
Les principaux opérateurs incluent :
- **=** : Égal
- **<>** ou **!=** : Différent
- **>**, **<**, **>=**, **<=** : Comparaison
- **BETWEEN** : Intervalle
- **IN** : Liste de valeurs
- **LIKE** : Modèle

### 2. Comment utiliser l'opérateur `LIKE` ?
```sql
SELECT * FROM employes WHERE nom LIKE 'J%';
```

### 3. Qu'est-ce que `BETWEEN` ?
Il filtre les résultats dans un intervalle donné :
```sql
SELECT * FROM employes WHERE salaire BETWEEN 30000 AND 50000;
```

---

## Fonctions en SQL

### 1. Quelles sont les principales fonctions SQL ?
Les principales fonctions incluent :
- **COUNT()** : Compte le nombre de lignes
- **SUM()** : Somme des valeurs
- **AVG()** : Moyenne des valeurs
- **MAX()** : Valeur maximale
- **MIN()** : Valeur minimale

### 2. Comment utiliser la fonction `COUNT()` ?
```sql
SELECT COUNT(*) FROM employes WHERE salaire > 40000;
```

### 3. Comment calculer une moyenne avec `AVG()` ?
```sql
SELECT AVG(salaire) FROM employes;
```

---

## Ressources supplémentaires
- [Documentation officielle de SQL](https://dev.mysql.com/doc/)
- [Tutoriels SQL en ligne](https://www.w3schools.com/sql/)
