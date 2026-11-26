[IO-61_Denysenko_Lab2,1.c](https://github.com/user-attachments/files/35463817/IO-61_Denysenko_Lab2.1.c)
#include <stdio.h>

#define MAX 100

int binarySearch(double a[][MAX], int m, int n,
                 double x, int row)
{
    int left = 0;
    int right = (row ? n : m) - 1;
    int result = -1;

    while (left <= right && result == -1) {
        int mid = left + (right - left) / 2;

        double value = row ? a[m - 1][mid] : a[mid][0];

        if (value == x)
            result = mid;
        else if (value > x)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return result;
}

int main(void)
{
    double a[MAX][MAX], x;
    int m, n;

    printf("Enter m and n: ");

    if (scanf("%d%d", &m, &n) != 2 ||
        m < 1 || n < 1 || m > MAX || n > MAX)
        return 1;

    printf("Enter matrix:\n");

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (scanf("%lf", &a[i][j]) != 1)
                return 1;

    printf("Enter X: ");

    if (scanf("%lf", &x) != 1)
        return 1;

    printf("Matrix:\n");

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++)
            printf("%9.4g", a[i][j]);

        printf("\n");
    }

    int col = binarySearch(a, m, n, x, 1);
    int row = binarySearch(a, m, n, x, 0);

    printf("X = %g\n", x);

    if (col != -1)
        printf("Last row: A[%d][%d]\n", m - 1, col);
    else
        printf("Last row: not found\n");

    if (row != -1)
        printf("First column: A[%d][0]\n", row);
    else
        printf("First column: not found\n");

    return 0;
}
