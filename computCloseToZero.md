J'ai un tableau d'entiers et je dois trouver celui qui est le plus proche de zéro 
(les entiers positifs ont priorité sur les négatifs.

// La correction de l'algorithme
public static int computeClosestToZero(int[] ts) {
    if (ts.length == 0) return 0;
    int closest = ts[0];
    int absClosest = Math.abs(closest);
    for (int i = 1; i < ts.length; i++) {
        int abs = Math.abs(ts[i]);
        if (abs < absClosest || (abs == absClosest && ts[i] > 0)) {
            closest = ts[i];
            absClosest = abs;
        }
    }
    return closest;
}