```
Je veux implémenter une fonction pour vérifier si un nombre donné contient plus de deux chiffres différents, que l'on appelle des duodigits :

- 12 , 110 , -33333 : sont tous des duodigits , puisqu'ils n'ont pas plus de deux chiffres différents 

- 102 : n'est pas un duodigit puisque ses chiffres ; 1 et 0 et 2 sont trois chiffres différents

```

```java

public class DuoDigit {

    public static boolean isDuoDigit(long number) {
        String numberString = String.valueOf(Math.abs(number));
        return (int) numberString.chars().distinct().count() <= 2;
    }

    public static void main(final String[] args) {
        long number1 = 223333423;
        long number2 = 223303;

        System.out.println(number1 + " is a duodigit? " + isDuodigit(number1));
        System.out.println(number2 + " is a duodigit? " + isDuodigit(number2));
    }
}
```