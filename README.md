# Résolution problèmes tests techniques

### I. Trouver la Paire idéale

<u>Problème :</u>
```
On souhaite retourne une paire de nombres (numbers) dans un tableau dont la somme est donnée(sum)
Contraintes :

1- Si on trouve une seule paire dans la liste de nombre, on retourne cette seule paire trouvée
2- Si on retrouve 2 paires ou plus, on retourne celle qui a l'indice de gauche la plus petite
3- Si on retrouve 2 paires ou plus avec les même indice de gauche, on retourne celle qui à l'indice de droite la plus petite.
4- Si on retrouve rien, on retourne [0,0]
```

<u>Résolution :</u>

```java
public int[] findSumPair(int[] numbers, int sum) {
      int[] pair = new int[]{0,0};

      outlerloop:
      for (int i = 0; i < numbers.length; i++) {
          for (int j = i + 1; j < numbers.length; j++) {
              if (numbers[i] + numbers[j] == sum) {
                  pair = new int[]{i,j};
                  break outlerloop;
              }
          }
      }

      return pair;
}
```

<br>

### II. Trouver le duo digit

<u>Problème :</u>
```
Je veux implémenter une fonction pour vérifier si un nombre donné contient plus de deux chiffres différents, 
que l'on appelle des duodigits :
1- 12 , 110 , -33333 : sont tous des duodigits , puisqu'ils n'ont pas plus de deux chiffres différents 
2- 102 : n'est pas un duodigit puisque ses chiffres ; 1 et 0 et 2 sont trois chiffres différents
```

<u>Résolution :</u>

```java
public boolean isDuoDigit(long number) {
  String numberString = String.valueOf(Math.abs(number));
  return (int) numberString.chars().distinct().count() <= 2;
}
```

<br>

### III. Calcul de currencys Version 1

<u>Problème :</u>

```
Considérons les billets et pièces de valeurs suivantes : 20 euros, 10 euros, 5 euros, 2 euros, 1 euros. 

Écrivez une fonction rendrecurrency qui prend en paramètres un entier prix et cinq valeurs entières x20, x10, x5, x2, x1 représentant le nombre de billets et de pièces de chaque sorte que donne un client pour payer l’objet dont le prix est mentionné. 

La fonction doit renvoyer cinq valeurs représentant la somme qu’il faut rendre au client, décomposée en billets et pièces (dans le même ordre que précédemment). 

La décomposition doit être faite en rendant le plus possible de billets et pièces de grosses valeurs (éventuellement avec d'autres billets que ceux apportés par le client; on suppose qu'il y a toujours assez de billets chez le vendeur).


Pour renvoyer les cinq valeurs, vous utilisez l'instruction:
return "res20, res10, res5, res2, res1"
où les cinq variables res20 à res1 contiennent les cinq valeurs à renvoyer (res20 contient le nombre de billets de 20 à remettre, ..., res1 le nombre de pièces de 1 à remettre).

S'il manque de l'argent, la fonction renverra cinq valeurs "Null"
```

<u>Résolution :</u>

```java
public String makeChange(int prix, int x20, int x10, int x5, int x2, int x1) {
    int amountPaid = (x20 * 20) + (x10 * 10) + (x5 * 5) + (x2 * 2) + x1;
    int amountReturned = amountPaid - prix;

    if (amountReturned < 0) {
        return "null";
    }

    int currency20 = amountReturned / 20;
    amountReturned %= 20;

    int currency10 = amountReturned / 10;
    amountReturned %= 10;

    int currency5 = amountReturned / 5;
    amountReturned %= 5;

    int currency2 = amountReturned / 2;
    amountReturned %= 2;

    int currency1 = amountReturned;

    return currency20 + ", " + currency10 + ", " + currency5 + ", " + currency2 + ", " + currency1;
}
```

<br>

### III. Calcul de currencys Version 2

<u>Problème :</u>

```
En s'appuyant sur la V1, On écrit une autre fonction qui prend en paramètre uniquement un prix et retourne le nombre de monnaie possible res20, res10, res5, res2 et res1
```

<u>Résolution :</u>

```java
public String makeChange(int prix) {
    int currency20 = prix / 20;
    int leftCurrency = prix % 20;

    int currency10 = leftCurrency / 10;
    leftCurrency %= 10;

    int currency5 = leftCurrency / 5;
    leftCurrency %= 5;

    int currency2 = leftCurrency / 2;
    leftCurrency %= 2;

    int currency1 = leftCurrency;

    return new StringBuilder().append(currency20).append(", ")
            .append(currency10).append(", ")
            .append(currency5).append(", ")
            .append(currency2).append(", ")
            .append(currency1).toString();
}
```

<br>

### IV. Entier plus proche de zéro

<u>Problème :</u>

```
J'ai un tableau d'entiers et je dois trouver celui qui est le plus proche de zéro les entiers positifs sont prioritaire sur les négatifs.
```

<u>Résolution :</u>

```java
public int findClosestToZero(int[] numbers) {
    if (numbers.length == 0) {
        throw new IllegalArgumentException("Le tableau ne doit pas être vide.");
    }

    int closest = numbers[0];

    for (int i = 1; i < numbers.length; i++) {
        int current = numbers[i];

        if (Math.abs(current) < Math.abs(closest) || (Math.abs(current) == Math.abs(closest) && current > 0)) {
            closest = current;
        }
    }

    return closest;
}
```

<br>

### V. Trouver le plus petit intervalle

<u>Problème :</u>

```
Implémenter la méthode findSmallestInterval(numbers) qui retourne le plus petit intervalle positif entre 2 éléments du tableau numbers(numbers est en fait un array de type int).
Par exemple: si je considère le tableau [1 6 4 8 2],le plus petit
intervalle est 1(différence entre 2 et 1).

Les contraintes:
1- Numbers contient au moins 2 éléments et au maximum 100000 éléments.
2- La solution qui privilégie la vitesse d'execution pour les tableaux
de grande taille obtiendra le plus de points.
3- La différence entre 2 éléments ne dépassera jamais la capacité d'un entier pour votre langage.
```

<u>Résolution :</u>

```java
import java.util.Arrays;

public int findSmallestInterval(int[] numbers) {
    if (numbers.length < 2 || numbers.length > 100000) {
        throw new IllegalArgumentException("Le tableau doit contenir entre 2 et 100000 éléments.");
    }

    Arrays.sort(numbers);
    int smallestInterval = Integer.MAX_VALUE;

    for (int i = 0; i < numbers.length - 1; i++) {
        int currentInterval = numbers[i + 1] - numbers[i];

        if (currentInterval < smallestInterval && currentInterval > 0) {
            smallestInterval = currentInterval;
        }
    }

    return smallestInterval;
}
```
<br>

### VI. Compter les caractères pour un mot

<u>Problème :</u>

```
On vous donne un tableau de chaînes de caractères words et une chaîne de caractères chars.

Une chaîne est bonne si elle peut être formée par les caractères de chars (chaque caractère ne peut être utilisé qu'une seule fois).

Retournez la somme des longueurs de toutes les bonnes chaînes de caractères en mots.

Exemple 1 :

Entrée : words = ["cat", "bt", "hat", "tree"], chars = "atach"
Sortie : 6
Explication : Les chaînes qui peuvent être formées sont "cat" et "hat", la réponse est donc 3 + 3 = 6.

Exemple 2 :

Entrée : words = ["hello", "world", "leetcode"], chars = "welldonehoneyr"
Résultat : 10
Explication : Les chaînes qui peuvent être formées sont "hello" et "world", la réponse est donc 5 + 5 = 10.

Contraintes :

. 1 <= words.length <= 1000
. 1 <= words[i].length, chars.length <= 100
. les mots[i] et les caractères sont des lettres minuscules anglaises.
```

<u>Résolution :</u>

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;

public static int countCharacters(String[] words, String chars) {
    validateInput(words, chars);

    Map<Character, Integer> charCountMap = getCharCount(chars);

    int totalLength = 0;
    for (String word : words) {
        Map<Character, Integer> wordCount = new HashMap<>(charCountMap);
        if (isValidWorld(word, wordCount)) {
            totalLength += word.length();
        }
    }

    return totalLength;
}

private Map<Character, Integer> getCharCount(String chars) {
    Map<Character, Integer> charCountMap = new HashMap<>();
    for (char c : chars.toCharArray()) {
        charCountMap.put(c, charCountMap.getOrDefault(c, 0) + 1);
    }
    return charCountMap;
}


private boolean isValidWorld(String word, Map<Character, Integer> wordCount) {
    for (char c : word.toCharArray()) {
        if (wordCount.containsKey(c) && wordCount.get(c) > 0) {
            wordCount.put(c, wordCount.get(c) - 1);
        } else {
            return false;
        }
    }

    return true;
}

private void validateInput(String[] words, String chars) {
    if (words.length < 1 || words.length > 1000) {
        throw new IllegalArgumentException("Contrainte : 1 <= words.length <= 1000");
    }

    if (chars.length() > 100) {
        throw new IllegalArgumentException("Contrainte : chars.length <= 100");
    }

    String smallString = Arrays.stream(words).min(Comparator.comparing(String::length)).get();
    if (smallString.length() < 1) {
        throw new IllegalArgumentException("Contrainte : 1 <= words[i].length");
    }
}
```
<br>

### VII. Trouver le noeud suivant :

<u>Problème 1er cas recherche à partir d'un noeud :</u>

```
Trouver le nœud suivant au même niveau que le nœud donné dans un arbre binaire

Étant donné un arbre binaire et un nœud dedans, écrivez un algorithme efficace pour trouver son prochain nœud au même niveau que le nœud.

Par exemple, considérons l'arbre binaire suivant :

              1
            /  \
           /    \
          2      3
         / \      \
        4   5      6
                  / \
                 7   8
    
```

<u>Résolution :</u>

```java
public class Node {
    private Node left = null;
    private Node right = null;
    private int value;

    public Node(int value) {
        this.value = value;
    }

    public static Node findRightNode(Node root, Node node){
        if (root == null) {
            return null;
        }

        Queue<Node> queue = new ArrayDeque<>();
        queue.add(root);
        Node currentNode;

        while(!queue.isEmpty()) {
            int queueSize = queue.size();
            while (queueSize-- > 0)
            {
                currentNode = queue.poll();

                if (currentNode == node)
                {
                    if (queueSize == 0) {
                        return null;
                    }
                    return queue.peek();
                }

                if (currentNode.left != null) {
                    queue.add(currentNode.left);
                }

                if (currentNode.right != null) {
                    queue.add(currentNode.right);
                }
            }
        }

        return null;
    }

    public int getValue() {
        return value;
    }

    public Node getLeft() {
        return left;
    }

    public Node getRight() {
        return right;
    }

    public void setLeft(Node left) {
        this.left = left;
    }

    public void setRight(Node right) {
        this.right = right;
    }
}
```

<u>Problème 2ème cas recherche à partir d'une valeur :</u>

```
Notre arbre binaire est construite de sorte que depuis la root, les valeurs inférieures à la route se trouvent à gauche et les valeurs supérieures se trouvent à droite. Nous répétons cette opération sur chaque noeud.

Par exemple, considérons l'arbre binaire suivant :

              8
            /  \
           /    \
          5      10
         / \      \
        4   6      11
       /           / \
      3          10  12
    
```

<u>Résolution :</u>

```java
public Node searchNode (Node node, int searchValue) {
    if (node == null) {
        return null;
    }


    if (node.getValue() == searchValue) {
        return node;
    }

    if (node.getValue() < searchValue) {
        return searchNode(node.getRight(), searchValue);
    }

    if (node.getValue() > searchValue) {
        return searchNode(node.getLeft(), searchValue);
    }

    return null;
}
````

<u>Problème 3ème cas recherche à partir d'une valeur sans noeud précisé :</u>

```
Par exemple, considérons l'arbre binaire suivant :

              8
            /  \
           /    \
          5      10
         / \      \
        4   6      11
       /           / \
      3          10  12
    
```

<u>Résolution :</u>

```java
public Nope find(int v) {
    Nope current = this;

    while (current != null) {
        if (current.value == v) {
            return current;
        }
        current = v < current.value ? current.left : current.right;
    }
    
    return null;
}

```


### VIII. Récupérer position final dans un labyrinthe

<u>Problème 1er :</u>

```
- La position initiale du personnage est (X=0, Y=0)
- width, height représente la surface (les limites)
- portalA l'obstacle A
- portalB l'obstacle B
- movements représente les mouvements de notre objet.
Avec les commandes (U: avancer, D: reculer, L: Aller à gauche, R: Aller à droite)
    
```

<u>Résolution :</u>

```java
import java.util.List;


public record Area(int width, int height) {}

-------------------------------------------------------------

public class Person {
    Position position;
    Area area;
    List<int[]> obstacles;

    public Person(Position position, Area area, List<int[]> obstacles) {
        this.position = position;
        this.area = area;
        this.obstacles = obstacles;
    }

    public void forward() {
        Position newPosition = position.moveForward("U");
        updateCurrentPosition(newPosition);
    }

    private void updateCurrentPosition(Position newPosition) {
        if (newPosition.isOnArea(area)) {
            position = newPosition;
        }
    }

    public void backward() {
        if (isNotInPortals(new Position(position.x(), position.y() - 1))) {
            position = new Position(position.x(), position.y() - 1);
        }
    }

    public void goToRight() {
        if (isNotInPortals(new Position(position.x() + 1, position.y()))) {
            position = new Position(position.x() + 1, position.y());
        }
    }

    public void goToLeft() {
        if (isNotInPortals(new Position(position.x() - 1, position.y()))) {
            position = new Position(position.x() - 1, position.y());
        }
    }

    public String displayFinalPosition() {
        return "(" + position.x() + " , " + position.y() + ")";
    }

    private boolean isNotInPortals(Position newPostion) {
        for (int[] obstacle: obstacles) {
            if (newPostion.x() != obstacle[0] && newPostion.y() != obstacle[1]) {
                return true;
            }
        }
        return false;
    }
}

-------------------------------------------------------------

public record Position(int x, int y) {
    Position moveForward(String direction) {
        return switch (direction) {
            case "U" -> new Position(x, y + 1);
            case "D" -> new Position(x, y - 1);
            case "L" -> new Position(x + 1, y);
            case "R" -> new Position(x - 1, y);
        };
    }

    public Position moveBackward(String direction) {
        return switch (direction) {
            case "U" -> new Position(x, y - 1);
            case "D" -> new Position(x, y + 1);
            case "L" -> new Position(x - 1, y);
            case "R" -> new Position(x + 1, y);
        };
    }

    public boolean isOnArea(Area area) {
        return y <= area.height() && y >= 0 && x <= area.width() && x >= 0;
    }
}

-------------------------------------------------------------


private String finalPositions(int width, int height, int[] portalA, int[] portalB, String movements) {
    Person person = new Person(new Position(0, 0), new Area(width, height), List.of(portalA, portalB));
    String[] commands = movements.split("");

    for (String command : commands) {
        move(person, command);
    }

    return person.displayFinalPosition();
}

 private static void move(Person person, String command) {
    switch (command) {
        case "U" -> person.forward();
        case "D" -> person.backward();
        case "L" -> person.goToLeft();
        case "R" -> person.goToRight();
    }
}



```