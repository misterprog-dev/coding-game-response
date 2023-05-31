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