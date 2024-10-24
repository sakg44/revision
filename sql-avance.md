# SQL Avancé: Questions et Réponses

1. **Qu'est-ce qu'une séquence dans SQL et comment la créer ?**

    ```sql
    CREATE SEQUENCE seq_example
    START WITH 1
    INCREMENT BY 1
    MINVALUE 1
    MAXVALUE 1000
    CYCLE;
    ```

    Une séquence est un objet qui génère des valeurs uniques (souvent utilisées pour les identifiants). La commande ci-dessus crée une séquence qui commence à 1 et s'incrémente de 1 jusqu'à 1000.

2. **Comment obtenir la prochaine valeur d'une séquence ?**

    ```sql
    SELECT seq_example.NEXTVAL FROM dual;
    ```

    La fonction `NEXTVAL` récupère la prochaine valeur disponible dans la séquence.

3. **Quelle est la différence entre NEXTVAL et CURRVAL ?**

    - `NEXTVAL` incrémente la séquence et renvoie la nouvelle valeur.
    - `CURRVAL` renvoie la valeur actuelle de la séquence dans la session courante, sans incrémentation.

4. **Comment créer une procédure stockée simple en SQL ?**

    ```sql
    CREATE PROCEDURE increment_salary(p_employee_id INT, p_increment DECIMAL)
    AS
    BEGIN
        UPDATE employees
        SET salary = salary + p_increment
        WHERE employee_id = p_employee_id;
    END;
    ```

    Cette procédure stockée permet d'incrémenter le salaire d'un employé.

5. **Comment appeler une procédure stockée en SQL ?**

    ```sql
    EXEC increment_salary(1001, 500);
    ```

    Ici, on appelle la procédure `increment_salary` pour augmenter le salaire de l'employé d'ID 1001 de 500.

6. **Comment créer une fonction en SQL ?**

    ```sql
    CREATE FUNCTION get_employee_salary(p_employee_id INT)
    RETURNS DECIMAL
    AS
    BEGIN
        DECLARE emp_salary DECIMAL;
        SELECT salary INTO emp_salary FROM employees WHERE employee_id = p_employee_id;
        RETURN emp_salary;
    END;
    ```

    Cette fonction renvoie le salaire de l'employé spécifié.

7. **Différence entre une procédure stockée et une fonction ?**

    - Une procédure n'a pas de valeur de retour, mais peut retourner plusieurs résultats via des paramètres OUT.
    - Une fonction retourne toujours une seule valeur.

8. **Comment optimiser une requête SQL avec des index ?**

    Les index accélèrent les requêtes en permettant à la base de données de rechercher plus rapidement dans les tables.

    ```sql
    CREATE INDEX idx_employee_lastname ON employees(last_name);
    ```

    Cet index est créé sur la colonne `last_name` de la table `employees`, ce qui accélérera les recherches basées sur le nom de famille.

9. **Quels types d'index existe-t-il en SQL ?**

    - **Index unique**: Empêche la duplication des valeurs.

    ```sql
    CREATE UNIQUE INDEX idx_unique_email ON employees(email);
    ```

    - **Index composite**: Index sur plusieurs colonnes.

    ```sql
    CREATE INDEX idx_composite_name ON employees(first_name, last_name);
    ```

    - **Index plein-texte**: Utilisé pour la recherche de texte dans de grandes quantités de données textuelles.

10. **Quand utiliser un index unique ?**

    Un index unique est utile lorsqu'on veut garantir que les valeurs d'une colonne (ou d'un ensemble de colonnes) sont uniques. Par exemple, pour les emails dans une table `users`.

11. **Comment modifier une procédure stockée existante ?**

    ```sql
    CREATE OR REPLACE PROCEDURE increment_salary(p_employee_id INT, p_increment DECIMAL)
    AS
    BEGIN
        UPDATE employees
        SET salary = salary + p_increment
        WHERE employee_id = p_employee_id;
        COMMIT;
    END;
    ```

    L'utilisation de `CREATE OR REPLACE` permet de modifier une procédure existante.

12. **Comment gérer les erreurs dans une procédure stockée ?**

    ```sql
    CREATE PROCEDURE safe_increment_salary(p_employee_id INT, p_increment DECIMAL)
    AS
    BEGIN
        BEGIN
            UPDATE employees SET salary = salary + p_increment WHERE employee_id = p_employee_id;
            COMMIT;
        EXCEPTION
            WHEN OTHERS THEN
                ROLLBACK;
                RAISE_APPLICATION_ERROR(-20001, 'Erreur lors de la mise à jour du salaire.');
        END;
    END;
    ```

    L'exception `WHEN OTHERS` permet de capturer toutes les erreurs possibles et d'effectuer un rollback en cas d'échec.

13. **Comment supprimer une séquence dans SQL ?**

    ```sql
    DROP SEQUENCE seq_example;
    ```

14. **Comment passer des paramètres IN, OUT, INOUT dans une procédure stockée ?**

    ```sql
    CREATE PROCEDURE proc_example(IN p_input INT, OUT p_output INT, INOUT p_inout INT)
    AS
    BEGIN
        SET p_output = p_input * 2;
        SET p_inout = p_inout + p_input;
    END;
    ```

    Les paramètres `IN` sont en lecture seule, `OUT` permet de renvoyer une valeur, et `INOUT` permet de passer et modifier une valeur.

15. **Comment créer une table temporaire en SQL ?**

    ```sql
    CREATE TEMPORARY TABLE temp_table (
        id INT,
        name VARCHAR(50)
    );
    ```

    Les tables temporaires sont spécifiques à la session et sont supprimées automatiquement une fois la session terminée.

16. **Qu'est-ce qu'une transaction dans SQL ?**

    Une transaction est un ensemble d'instructions SQL qui s'exécutent comme une unité de travail. Elles permettent de garantir la cohérence des données en cas de succès ou d'échec.

17. **Comment démarre-t-on une transaction manuellement ?**

    ```sql
    BEGIN TRANSACTION;
    -- Exécution de requêtes
    COMMIT;
    ```

    On peut aussi utiliser `ROLLBACK` pour annuler les modifications en cas d'erreur.

18. **Qu'est-ce que l'isolation des transactions ?**

    Le niveau d'isolation détermine comment les transactions interagissent entre elles. Les niveaux incluent :

    - `READ UNCOMMITTED`
    - `READ COMMITTED`
    - `REPEATABLE READ`
    - `SERIALIZABLE`

19. **Comment créer une transaction implicite ?**

    Chaque requête DML (comme `INSERT`, `UPDATE`, `DELETE`) sans `BEGIN TRANSACTION` est exécutée dans une transaction implicite, qui est validée automatiquement une fois la requête terminée.

20. **Qu'est-ce qu'une vue matérialisée ?**

    Une vue matérialisée stocke physiquement les résultats de la requête dans la base de données et peut être mise à jour périodiquement.

    ```sql
    CREATE MATERIALIZED VIEW mv_example AS
    SELECT department_id, SUM(salary) FROM employees GROUP BY department_id;
    ```

21. **Comment rafraîchir une vue matérialisée ?**

    ```sql
    REFRESH MATERIALIZED VIEW mv_example;
    ```

22. **Comment utiliser une fonction dans une requête SQL ?**

    ```sql
    SELECT get_employee_salary(1001) AS salary;
    ```

23. **Qu'est-ce qu'un trigger en SQL et comment en créer un ?**

    Un trigger est un ensemble d'instructions SQL qui s'exécute automatiquement lorsqu'un événement particulier se produit sur une table.

    ```sql
    CREATE TRIGGER before_employee_insert
    BEFORE INSERT ON employees
    FOR EACH ROW
    BEGIN
        IF :NEW.salary < 0 THEN
            RAISE_APPLICATION_ERROR(-20001, 'Le salaire ne peut pas être négatif.');
        END IF;
    END;
    ```

24. **Différence entre un trigger BEFORE et AFTER ?**

    - **BEFORE**: S'exécute avant que l'instruction DML ne modifie la table.
    - **AFTER**: S'exécute après que l'instruction DML a modifié la table.

25. **Qu'est-ce qu'une fonction agrégée définie par l'utilisateur (UDAF) ?**

    Une UDAF est une fonction personnalisée qui opère sur plusieurs lignes pour retourner une valeur unique. Elle est souvent utilisée dans des scénarios où les fonctions agrégées natives ne sont pas suffisantes.

26. **Comment ajouter un index sur une fonction ?**

    ```sql
    CREATE INDEX idx_lower_last_name ON employees(LOWER(last_name));
    ```

    Cela permet d'accélérer les recherches insensibles à la casse sur le nom de famille.

27. **Comment gérer les index inutilisés ?**

    Vous pouvez vérifier si un index est utilisé via les outils d'analyse des performances ou en surveillant l'utilisation des index, puis les supprimer si nécessaire.

    ```sql
    DROP INDEX idx_employee_lastname;
    ```

28. **Qu'est-ce que la partition d'une table ?**

    La partition d'une table consiste à diviser une grande table en sous-tables plus petites (partitions), ce qui améliore les performances des requêtes.

29. **Comment créer une table partitionnée ?**

    ```sql
    CREATE TABLE sales (
        sale_id INT,
        sale_date DATE,
        amount DECIMAL
    ) PARTITION BY ...
    ```
