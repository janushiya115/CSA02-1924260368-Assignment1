#include <stdio.h>

#define SQUARE(x) ((x) * (x))
#define MAX(a,b) ((a) > (b) ? (a) : (b))
#define RUPEES_TO_PAISE(x) ((x) * 100)

int main()
{
    int a = 5, b = 10;

    printf("Square of 5 = %d\n", SQUARE(a));
    printf("Maximum number = %d\n", MAX(a, b));
    printf("Rupees to paise = %d\n", RUPEES_TO_PAISE(50));

    return 0;
}
