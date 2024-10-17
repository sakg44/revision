
# Questions et Réponses sur l'API Java Collections

### 1. **Qu'est-ce qu'une collection en Java ?**
   Une collection est un objet qui regroupe plusieurs éléments dans une seule unité. L'API Java Collections fournit des classes et des interfaces pour stocker et manipuler des groupes d'objets.

### 2. **Quelle est la différence entre `Collection` et `Collections` ?**
   - `Collection` est une interface de base qui définit les opérations sur un groupe d'objets.
   - `Collections` est une classe utilitaire qui contient des méthodes statiques pour manipuler ou créer des collections.

### 3. **Quels sont les principaux types de collections en Java ?**
   - `List`
   - `Set`
   - `Queue`
   - `Map` (bien que `Map` ne soit pas une sous-interface de `Collection`, elle fait partie de l'API Collections)

### 4. **Quelles sont les classes principales qui implémentent l'interface `List` ?**
   - `ArrayList`
   - `LinkedList`
   - `Vector`
   - `Stack`

### 5. **Quelles sont les classes principales qui implémentent l'interface `Set` ?**
   - `HashSet`
   - `LinkedHashSet`
   - `TreeSet`

### 6. **Quelle est la différence entre une `List` et un `Set` ?**
   - Une `List` permet des éléments en doublon et maintient un ordre d'insertion.
   - Un `Set` ne permet pas de doublons et ne garantit pas un ordre particulier (à l'exception de `LinkedHashSet` et `TreeSet`).

### 7. **Quand utiliser un `HashSet` plutôt qu'un `TreeSet` ?**
   - Utilise `HashSet` pour une performance plus rapide en termes d'ajout, suppression et recherche.
   - Utilise `TreeSet` lorsque tu as besoin d'un ordre trié des éléments.

### 8. **Quelle est la différence entre `ArrayList` et `LinkedList` ?**
   - `ArrayList` est basée sur un tableau dynamique, offrant un accès rapide aux éléments (O(1)), mais une insertion/suppression lente (O(n)).
   - `LinkedList` est basée sur une structure de liste doublement chaînée, offrant une insertion/suppression rapide (O(1)), mais un accès lent (O(n)).

### 9. **Comment vérifier si une collection est vide ?**
   Utilise la méthode `isEmpty()`.

   ```java
   Collection<?> collection = ...;
   if (collection.isEmpty()) {
       // La collection est vide
   }
   ```

### 10. **Qu'est-ce qu'une `Queue` en Java ?**
   Une `Queue` est une interface qui étend `Collection` et représente une structure de données de type file (FIFO).

### 11. **Quelle est la différence entre `Queue` et `Deque` ?**
   - `Queue` suit la règle FIFO (First-In-First-Out).
   - `Deque` (Double Ended Queue) permet l'insertion et la suppression des deux côtés.

### 12. **Qu'est-ce qu'un `PriorityQueue` ?**
   Un `PriorityQueue` est une file de priorité qui trie automatiquement les éléments en fonction de leur ordre naturel ou d'un `Comparator` spécifié.

### 13. **Quelle est la différence entre `HashMap` et `TreeMap` ?**
   - `HashMap` ne garantit pas d'ordre pour ses clés.
   - `TreeMap` trie les clés dans l'ordre naturel ou en utilisant un comparateur.

### 14. **Comment accéder à une valeur dans un `Map` ?**
   Utilise la méthode `get()` pour accéder à la valeur associée à une clé.

   ```java
   Map<String, Integer> map = new HashMap<>();
   Integer value = map.get("key");
   ```

### 15. **Qu'est-ce qu'un `ConcurrentHashMap` ?**
   `ConcurrentHashMap` est une implémentation thread-safe de `HashMap` qui permet un accès concurrent sans verrouiller toute la carte.

### 16. **Qu'est-ce que l'interface `Iterator` ?**
   `Iterator` est une interface qui permet de parcourir les éléments d'une collection de manière séquentielle.

### 17. **Quelle est la différence entre `Iterator` et `ListIterator` ?**
   - `Iterator` permet uniquement de parcourir les éléments dans une direction (avant).
   - `ListIterator` permet de parcourir les éléments dans les deux directions (avant et arrière) et permet la modification des éléments.

### 18. **Comment supprimer un élément d'une collection pendant l'itération ?**
   Utilise la méthode `remove()` de l'`Iterator`.

   ```java
   Iterator<String> iterator = collection.iterator();
   while (iterator.hasNext()) {
       String element = iterator.next();
       if (condition) {
           iterator.remove();
       }
   }
   ```

### 19. **Qu'est-ce qu'une collection immuable ?**
   Une collection immuable est une collection dont les éléments ne peuvent pas être modifiés après sa création.

   Exemple :
   ```java
   List<String> immutableList = Collections.unmodifiableList(new ArrayList<>());
   ```

### 20. **Quelle est la différence entre `HashMap` et `Hashtable` ?**
   - `HashMap` n'est pas synchronisé et permet des valeurs `null`.
   - `Hashtable` est synchronisé et ne permet pas de valeurs `null`.

### 21. **Qu'est-ce qu'un `BlockingQueue` ?**
   `BlockingQueue` est une interface de file d'attente qui supporte les opérations qui attendent que l'espace soit disponible ou qu'un élément soit inséré, et est couramment utilisée en programmation concurrentielle.

### 22. **Comment trier une collection en Java ?**
   Utilise la méthode `Collections.sort()` pour trier une `List`.

   ```java
   Collections.sort(list);
   ```

   Ou avec un `Comparator` personnalisé :
   ```java
   Collections.sort(list, comparator);
   ```

### 23. **Qu'est-ce qu'un `Comparator` ?**
   `Comparator` est une interface qui définit une méthode pour comparer deux objets afin de les trier.

### 24. **Qu'est-ce qu'un `Comparable` ?**
   `Comparable` est une interface que les objets implémentent pour définir leur ordre naturel en implémentant la méthode `compareTo()`.

### 25. **Comment faire une copie superficielle d'une collection ?**
   Utilise le constructeur de copie :

   ```java
   List<String> copy = new ArrayList<>(originalList);
   ```

### 26. **Qu'est-ce qu'une copie profonde d'une collection ?**
   Une copie profonde d'une collection signifie que non seulement la collection est copiée, mais que tous les objets contenus dans la collection sont également copiés.

### 27. **Quelle est la différence entre une copie superficielle et une copie profonde ?**
   - La copie superficielle copie seulement la structure de la collection, pas les objets à l'intérieur.
   - La copie profonde copie à la fois la structure et les objets.


