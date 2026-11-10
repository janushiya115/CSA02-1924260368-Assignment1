#include <stdio.h>

#define PEAK_START 18
#define PEAK_END 22

int main()
{
    long long rate, fixed;
    long long peak_wh = 0, normal_wh = 0;
    long long energy_charge, total_bill;
    int n, hour;
    long long wh;

    printf("Enter normal rate (paise per kWh): ");
    scanf("%lld", &rate);

    printf("Enter fixed charge (paise): ");
    scanf("%lld", &fixed);

    printf("Enter number of readings: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        printf("Enter hour and watt-hours: ");
        scanf("%d %lld", &hour, &wh);

        if (hour >= PEAK_START && hour < PEAK_END)
            peak_wh += wh;
        else
            normal_wh += wh;
    }

    energy_charge =
        (normal_wh * rate * 100 +
         peak_wh * rate * 120 + 50000) / 100000;

    total_bill = energy_charge + fixed;

    printf("\nNormal Usage = %lld Wh\n", normal_wh);
    printf("Peak Usage = %lld Wh\n", peak_wh);

    printf("Energy Charge = Rs %lld.%02lld\n",
           energy_charge / 100, energy_charge % 100);

    printf("Total Bill = Rs %lld.%02lld\n",
           total_bill / 100, total_bill % 100);

    return 0;
}
