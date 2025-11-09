# TP-math-code-source-en-c-PGCD-de-Nouhaila-Sebbane
Mon code en C résout les équations diophantiennes linéaires de la forme ax + by = c, en calculant le PGCD de a et b via l'algorithme d'Euclide étendu (fonction récursive extended_gcd).
Il demande les valeurs de a, b et c à l'utilisateur, gère les signes négatifs avec abs(), et vérifie si des solutions entières existent (si PGCD divise c).
S'il y en a, il affiche une solution particulière (xp, yp) et la forme générale des solutions avec un paramètre k.
Le programme est interactif, optimisé pour une exécution simple dans une interface comme Code::Blocks.

              
               #include <stdio.h>
               #include <stdlib.h>

                int extended_gcd(int a, int b, int *x, int *y) { /*Etape 1:forcement des valeurs positives pour que la fonction extended_gcd fonctionne mieux,(car le L'algorithme d'Euclide fonctionne mieux avec des nombres positifs)*/
    if (b == 0) { *x = 1; *y = 0; return a; } /*Etape 2:on renvoie directement a parce que quand b=0, le PGCD est a (par définition de l'algorithme d'Euclide)*/
    int x1, y1, gcd = extended_gcd(b,a % b, &x1, &y1);
    *x= y1; *y = x1 - (a / b) * y1; return gcd; /*Etape 3: gcd contient le PGCD calculé Comme le PGCD de a et b est le même que celui de b et a % b*/
                           }

                int main() {
    int a, b, c, x0, y0;
    printf(" veuillez Entrez les valeurs de a, b et c : ");/*Etape 4:demander l’utilisateur de taper les valeurs de a,b et c au clavier*/
    scanf("%d %d %d", &a, &b, &c);
    int d = extended_gcd(abs(a), abs(b), &x0, &y0);/*Etape 5:abs() enlève les signes négatifs pour simplifiert elle calcul le PGCD et met des valeurs dans x0 et y0 telles :que ax0 + by0 = d*/
    if (a < 0) x0 = -x0;
    if (b < 0) y0 = -y0;/*Etape 6:Si a est négatif,on inverse le signe de x0. pareil pour b et y0 parce qu'on a utilisé abs() avant, donc on corrige les signes pour que la solution corresponde à l'équation originale (avec signes) EX:Si a=-6, b=9, après calcul avec abs (6 et 9), x0 pourrait être -1, mais comme a<0, x0 devient 1 (inversé)*/
    if (d == 0 || c % d != 0){ /*Etape 6:Vérification si des solutions existent*/
    printf("Pas de solution entiere!\n");
    } else {
        int xp = x0 * (c / d), yp = y0 * (c / d);
        printf("Il existe des solutions entieres!:\n");/*Etape 7:si les solutions existent,Calcul et affichage*/
        printf("Solution particuliere : (%d, %d)\n", xp, yp);
        printf("Forme generale : (x, y) = (%d + %d k, %d - %d k), k ∈ Z\n", xp, abs(b)/d, yp, abs(a)/d);
        printf("Avec d = %d\n", d);
        printf("merci pour votre execution!");
    }
    return 0;
            }
