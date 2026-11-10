code01 billing.h
#include <stdio.h>

#define FIXED_CHARGE 5000
#define RATE2 225
#define RATE3 450

long compute_bill(int units);

long compute_bill(int units)
{
    long bill = FIXED_CHARGE;

    if (units > 200)
    {
        bill += 100 * RATE2;
        bill += (units - 200) * RATE3;
    }
    else if (units > 100)
    {
        bill += (units - 100) * RATE2;
    }

    return bill;
}

int main()
{
    int units = 150;

#ifdef DEBUG
    printf("DEBUG: Units = %d\n", units);
#endif

    long bill = compute_bill(units);

    printf("Units Consumed = %d\n", units);
    printf("Electricity Bill = Rs %ld.%02ld\n",
           bill / 100, bill % 100);

    return 0;
}

code02 main.c
#include <stdio.h>
#include "billing.h"

long compute_bill(int units)
{
    long bill = FIXED_CHARGE;

    if (units > 200)
    {
        bill += 100 * RATE2;
        bill += (units - 200) * RATE3;
    }
    else if (units > 100)
    {
        bill += (units - 100) * RATE2;
    }

    return bill;
}

int main()
{
    int units = 150;

    #ifdef DEBUG
    printf("DEBUG: Units = %d\n", units);
    #endif

    printf("Electricity Bill = Rs %ld.%02ld\n",
           compute_bill(units) / 100,
           compute_bill(units) % 100);

    return 0;
}
