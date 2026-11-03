Code 1- billing.h

#ifndef BILLING_H
#define BILLING_H

#include <stdio.h>

#define SLAB1 100
#define SLAB2 200

#define RATE2 225L
#define RATE3 450L
#define FIXED 5000L

typedef unsigned short meter_t;

unsigned int consumption(meter_t previous,
                         meter_t current);

long compute_bill(unsigned int units);

#ifdef DEBUG
#define DEBUG_PRINT(...) printf(__VA_ARGS__)
#else
#define DEBUG_PRINT(...) ((void)0)
#endif

#endif



Code 2 - billing.c


#include "billing.h"
#include <limits.h>

unsigned int consumption(meter_t previous,
                         meter_t current)
{
    if (current >= previous)
        return current - previous;

    if (previous >= 65000 && current <= 1000)
        return USHRT_MAX - previous + 1U + current;

    return UINT_MAX;
}

long compute_bill(unsigned int units)
{
    long energy = 0;

    if (units > SLAB2)
    {
        energy = (SLAB2 - SLAB1) * RATE2
               + (units - SLAB2) * RATE3;
    }
    else if (units > SLAB1)
    {
        energy = (units - SLAB1) * RATE2;
    }

    return energy + FIXED;
}

int main()
{
    unsigned int p, c, units;
    long bill;

    printf("Enter previous reading: ");

    if (scanf("%u", &p) != 1 || p > USHRT_MAX)
    {
        printf("Invalid input\n");
        return 1;
    }

    printf("Enter current reading: ");

    if (scanf("%u", &c) != 1 || c > USHRT_MAX)
    {
        printf("Invalid input\n");
        return 1;
    }

    units = consumption((meter_t)p, (meter_t)c);

    if (units == UINT_MAX)
    {
        printf("Invalid meter reading\n");
        return 1;
    }

    bill = compute_bill(units);

    DEBUG_PRINT("Units consumed: %u\n", units);

    printf("Units consumed: %u\n", units);
    printf("Electricity Bill: Rs %ld.%02ld\n",
           bill / 100, bill % 100);

    return 0;
}
