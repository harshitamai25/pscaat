# pscaat
bill calculator 

#include <stdio.h>

#include <time.h>

struct item
{
    char name[60];
    int quantity;
    float price;
};

int main()
{
    int n, i;
    struct item j[10];
    float total = 0, gst, discount, finalAmount;

    /* Time and Date */
    time_t t;
    struct tm *tm_info;
    char date[30];

    time(&t);
    tm_info = localtime(&t);
    strftime(date, 30, "%d-%M-%Y  %H:%M:%S", tm_info);

    printf("\t\tBILL CALCULATOR\n");
    printf("Please enter the details of your purchase\n");

    printf("Enter number of distinguished items: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++)
    {
        printf("\nItem %d\n", i + 1);

        printf("Enter item name: ");
        scanf("%s", j[i].name);

        printf("Enter quantity: ");
        scanf("%d", &j[i].quantity);

        printf("Enter price: ");
        scanf("%f", &j[i].price);

        total += j[i].quantity * j[i].price;
    }

    gst = 0.05 * total;
    discount = (total > 1000) ? 0.10 * total : 0;
    finalAmount = total + gst - discount;

    /* Display Receipt */
    printf("\n====================================\n");
    printf("           ABC MART\n");
    printf("        Bangalore, India\n");
    printf("====================================\n");
    printf("Date & Time : %s\n", date);
    printf("------------------------------------\n");
    printf("Item\tQty\tAmount\n");
    printf("------------------------------------\n");

    for (i = 0; i < n; i++)
    {
        printf("%s\t%d\t%.2f\n",
               j[i].name,
               j[i].quantity,
               j[i].quantity * j[i].price);
    }

    printf("------------------------------------\n");
    printf("Total        : %.2f\n", total);
    printf("GST (5%%)     : %.2f\n", gst);
    printf("Discount     : %.2f\n", discount);
    printf("Final Amount : %.2f\n", finalAmount);
    printf("------------------------------------\n");
    printf("      THANK YOU! VISIT AGAIN\n");
    printf("====================================\n");

    /* Save Receipt to PDF */
    FILE *fp;
    fp = fopen("receipt.pdf", "w");
    fprintf(fp, "%%PDF-1.4\n");
    fprintf(fp, "====================================\n");
    fprintf(fp, "           ABC MART\n");
    fprintf(fp, "        Bangalore, India\n");
    fprintf(fp, "====================================\n");
    fprintf(fp, "Date & Time : %s\n", date);
    fprintf(fp, "------------------------------------\n");
    fprintf(fp, "Item\tQty\tAmount\n");
    fprintf(fp, "------------------------------------\n");

    for (i = 0; i < n; i++)
    {
        fprintf(fp, "%s\t%d\t%.2f\n",
                j[i].name,
                j[i].quantity,
                j[i].quantity * j[i].price);
    }

    fprintf(fp, "------------------------------------\n");
    fprintf(fp, "Total        : %.2f\n", total);
    fprintf(fp, "GST (5%%)     : %.2f\n", gst);
    fprintf(fp, "Discount     : %.2f\n", discount);
    fprintf(fp, "Final Amount : %.2f\n", finalAmount);
    fprintf(fp, "------------------------------------\n");
    fprintf(fp, "      THANK YOU! VISIT AGAIN\n");
    fprintf(fp, "====================================\n");

    fclose(fp);

    printf("\nReceipt saved successfully as receipt.pdf\n");

    return 0;
}
