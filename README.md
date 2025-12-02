# Lab7_C_CiobanuNicolae
# Scop:
# Familiarizarea studentului cu utilizarea platformei GitHub pentru gestionarea și publicarea proiectelor software.
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int** alocare(int n, int m);
void introducere(int **a, int n, int m);
void randomizare(int **a, int n, int m);
void afisare(int **a, int n, int m);
void eliberare(int **a, int n);
void sortare_coloane_desc(int **a, int n, int m);

int main() {
    int **a = NULL;
    int n, m;
    int optiune;

    srand(time(NULL));

    printf("Introduceti numarul de linii n = ");
    scanf("%d", &n);
    printf("Introduceti numarul de coloane m = ");
    scanf("%d", &m);

    do {
        printf("\n===== MENIU =====\n");
        printf("1. Alocarea dinamica a memoriei\n");
        printf("2. Introducerea elementelor\n");
        printf("3. Completarea cu valori aleatorii\n");
        printf("4. Sortarea coloanelor in ordine DESC (bubble sort)\n");
        printf("5. Afisarea matricei\n");
        printf("6. Eliberarea memoriei\n");
        printf("0. Iesire\n");
        printf("Optiunea: ");
        scanf("%d", &optiune);

        switch (optiune) {

        case 1:
            a = alocare(n, m);
            printf("Memoria a fost alocata.\n");
            break;

        case 2:
            if (a) introducere(a, n, m);
            else printf("Mai intai alocati memoria (opt. 1).\n");
            break;

        case 3:
            if (a) randomizare(a, n, m);
            else printf("Mai intai alocati memoria (opt. 1).\n");
            break;

        case 4:
            if (a) sortare_coloane_desc(a, n, m);
            else printf("Mai intai alocati memoria (opt. 1).\n");
            break;

        case 5:
            if (a) afisare(a, n, m);
            else printf("Mai intai alocati memoria (opt. 1).\n");
            break;

        case 6:
            if (a) {
                eliberare(a, n);
                a = NULL;
            }
            printf("Memoria a fost eliberata.\n");
            break;
        }

    } while (optiune != 0);

    if (a) eliberare(a, n);
    return 0;
}


int** alocare(int n, int m) {
    int **a = (int**)malloc(n * sizeof(int*));
    if (!a) {
        printf("EROARE la alocarea liniilor!\n");
        exit(1);
    }

    for (int i = 0; i < n; i++) {
        a[i] = (int*)malloc(m * sizeof(int));
        if (!a[i]) {
            printf("EROARE la alocarea coloanelor!\n");
            exit(1);
        }
    }

    return a;
}


void introducere(int **a, int n, int m) {
    printf("Introduceti elementele matricei:\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            printf("a[%d][%d] = ", i, j);
            scanf("%d", &a[i][j]);
        }
}


void randomizare(int **a, int n, int m) {
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            a[i][j] = rand() % 100 - 50;   // valori între -50 și +49

    printf("Matricea a fost completata cu valori random.\n");
}


void afisare(int **a, int n, int m) {
    printf("\nMatricea:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++)
            printf("%4d ", a[i][j]);
        printf("\n");
    }
}


void sortare_coloane_desc(int **a, int n, int m) {
    for (int col = 0; col < m; col++) {
        for (int pas = 0; pas < n - 1; pas++) {
            for (int i = 0; i < n - pas - 1; i++) {
                if (a[i][col] < a[i + 1][col]) {
                    int aux = a[i][col];
                    a[i][col] = a[i + 1][col];
                    a[i + 1][col] = aux;
                }
            }
        }
    }

    printf("Coloanele au fost sortate descrescator.\n");
}

void eliberare(int **a, int n) {
    for (int i = 0; i < n; i++)
        free(a[i]);
    free(a);
}

