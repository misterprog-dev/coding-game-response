```
En s'appuyant sur la V1, On écrit une autre fonction qui prend en paramètre uniquement un prix et retourne le nombre de monnaie possible res20, res10, res5, res2 et res1
```

```java

public class MonnaieCalculatorV2 {
    public static String calculerMonnaie(int prix) {
        int monnaie20 = prix / 20;
        int montantRestant = prix % 20;

        int monnaie10 = montantRestant / 10;
        montantRestant %= 10;

        int monnaie5 = montantRestant / 5;
        montantRestant %= 5;

        int monnaie2 = montantRestant / 2;
        montantRestant %= 2;

        int monnaie1 = montantRestant;

        return new StringBuilder().append(monnaie20).append(", ")
                .append(monnaie10).append(", ")
                .append(monnaie5).append(", ")
                .append(monnaie2).append(", ")
                .append(monnaie1).toString();
    }

    public static void main(String[] args) {
        int prix = 47;
        String resultat = calculerMonnaie(prix);
        System.out.println("Nombre de billets et pièces nécessaires : " + resultat);
    }
}

```