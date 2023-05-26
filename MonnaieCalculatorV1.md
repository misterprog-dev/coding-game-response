```
Considérons les billets et pièces de valeurs suivantes : 20 euros, 10 euros, 5 euros, 2 euros, 1 euros. 

Écrivez une fonction rendreMonnaie qui prend en paramètres un entier prix et cinq valeurs entières x20, x10, x5, x2, x1 représentant le nombre de billets et de pièces de chaque sorte que donne un client pour payer l’objet dont le prix est mentionné. 

La fonction doit renvoyer cinq valeurs représentant la somme qu’il faut rendre au client, décomposée en billets et pièces (dans le même ordre que précédemment). 

La décomposition doit être faite en rendant le plus possible de billets et pièces de grosses valeurs (éventuellement avec d'autres billets que ceux apportés par le client; on suppose qu'il y a toujours assez de billets chez le vendeur).


Pour renvoyer les cinq valeurs, vous utilisez l'instruction:
return "res20, res10, res5, res2, res1"
où les cinq variables res20 à res1 contiennent les cinq valeurs à renvoyer (res20 contient le nombre de billets de 20 à remettre, ..., res1 le nombre de pièces de 1 à remettre).

S'il manque de l'argent, la fonction renverra cinq valeurs "Null"
```

```java

public class MonnaieCalculatorV1 {

    public static String rendreMonnaie(int prix, int x20, int x10, int x5, int x2, int x1) {
        int montantPaye = (x20 * 20) + (x10 * 10) + (x5 * 5) + (x2 * 2) + x1;
        int montantRendu = montantPaye - prix;

        if (montantRendu < 0) {
            return "null";
        }

        int monnaie20 = montantRendu / 20;
        montantRendu %= 20;

        int monnaie10 = montantRendu / 10;
        montantRendu %= 10;

        int monnaie5 = montantRendu / 5;
        montantRendu %= 5;

        int monnaie2 = montantRendu / 2;
        montantRendu %= 2;

        int monnaie1 = montantRendu;

        return monnaie20 + ", " + monnaie10 + ", " + monnaie5 + ", " + monnaie2 + ", " + monnaie1;
    }

    public static void main(final String[] args) {
        int prix = 130;
        int x20 = 2;
        int x10 = 1;
        int x5 = 0;
        int x2 = 3;
        int x1 = 2;

        String resultat = rendreMonnaie(prix, x20, x10, x5, x2, x1);
        System.out.println("Montant à rendre : " + resultat);
    }
}

```