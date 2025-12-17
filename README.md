#include <stdio.h>

// Fonction d'Euclide étendu
// Calcule le PGCD(a, b) et les coefficients x, y
// tels que : a*x + b*y = PGCD(a, b)
int euclide_etendu(int a, int b, int *x, int *y)
{
    if (b == 0)
    {
        *x = 1;
        *y = 0;
        return a;
    }

    int x1, y1;
    int d = euclide_etendu(b, a % b, &x1, &y1);

    *x = y1;
    *y = x1 - (a / b) * y1;

    return d;
}

int main()
{
    int a, b, c;
    int x, y;

    // Lecture des entiers
    printf("Entrez les entiers a, b et c pour resoudre a*x + b*y = c :\n");
    scanf("%d %d %d", &a, &b, &c);

    // Calcul du PGCD et des coefficients de Bézout
    int d = euclide_etendu(a, b, &x, &y);

    // Vérification de l'existence d'une solution
    if (c % d != 0)
    {
        printf("Aucune solution entiere : %d ne divise pas %d.\n", d, c);
    }
    else
    {
        // Calcul d'une solution particulière
        int x0 = x * (c / d);
        int y0 = y * (c / d);

        // Affichage de la solution particulière
        printf("Solution particuliere :\n");
        printf("x = %d, y = %d\n", x0, y0);

        // Affichage des solutions générales
        printf("Solutions generales :\n");
        printf("x = %d + %d*k\n", x0, b / d);
        printf("y = %d - %d*k\n", y0, a / d);
        printf("ou k est un entier relatif.\n");
    }

    return 0;
}
