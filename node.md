Trouver le nœud suivant au même niveau que le nœud donné dans un arbre binaire

Étant donné un arbre binaire et un nœud dedans, écrivez un algorithme efficace pour trouver son prochain nœud au même niveau que le nœud.

Par exemple, considérons l'arbre binaire suivant :

 /* Construire l'arbre suivant
              1
            /  \
           /    \
          2      3
         / \      \
        4   5      6
                  / \
                 7   8
    */

<!DOCTYPE html>
<html>
 
    <head>
        <meta charset="utf-8" />
    </head>
 
    <body>
        <p>Le lien du noeud :</p>
        <img src="https://www.techiedelight.com/wp-content/uploads/Find-Next-Node.png">
    </body>
 
</html>

The next node of 2 is 3
The next node of 5 is 6
The next node of 7 is 8
The next node of 8 is null

class Nope {
    
    Nope left, right;
    int value;

    public Nope find(int v){
        // completer le code
        return null;
    }
}