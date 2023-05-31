# Réponses problèmes coding game

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
