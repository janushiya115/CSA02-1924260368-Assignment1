#include <stdio.h>
#include <limits.h>

typedef unsigned short meter_t;

#define SLAB1 100
#define SLAB2 200
#define RATE2 225
#define RATE3 450
#define FIXED 5000L

unsigned int consumption(meter_t previous, meter_t current)
{
    return (meter_t)(current - previous);
}

long long compute_bill(unsigned int units)
{
    long long bill = FIXED;

    if (units > SLAB2)
    {
        bill += 100LL * RATE2;
        bill += (long long)(units - SLAB2) * RATE3;
    }
    else if (units > SLAB1)
    {
        bill += (long long)(units - SLAB1) * RATE2;
    }

    return bill;
}

int main()
{
    meter_t previous = 1200;
    meter_t current = 1530;

    unsigned int units = consumption(previous, current);

    long long bill = compute_bill(units);

    printf("Previous Reading = %u\n", previous);
    printf("Current Reading = %u\n", current);
    printf("Units Consumed = %u\n", units);

    printf("Total Bill = Rs %lld.%02lld\n",
           bill / 100, bill % 100);

    printf("Maximum Meter Reading = %u\n", USHRT_MAX);

    return 0;
}
