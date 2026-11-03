#include <stdio.h>

int main()
{
    int p, c, units, i;
    float bill, total = 0;

    for(i = 1; i <= 5; i++)
    {
        printf("Enter previous and current reading: ");
        scanf("%d%d", &p, &c);

        units = c - p;

        if(units < 0)
        {
            printf("Invalid reading\n");
            continue;
        }

        if(units <= 100)
            bill = 50;
        else if(units <= 200)
            bill = 50 + (units - 100) * 2.25;
        else
            bill = 275 + (units - 200) * 4.50;

        printf("Units: %d\n", units);
        printf("Bill: Rs. %.2f\n", bill);

        total += bill;
    }

    printf("Total Bill: Rs. %.2f\n", total);

    return 0;
}
