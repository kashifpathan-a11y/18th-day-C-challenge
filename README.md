# 18th-day-C-challenge
/*
    Name: pathan kashif
    Registration Number: AP25110090173
    Day 18 – Inventory Management System
*/

#include <stdio.h>

int main() {

    int productID[10], quantity[10];
    float price[10];
    char name[10][50];

    int totalProducts = 0;
    int choice;

    while (1) {

        printf("\n==============================\n");
        printf("   INVENTORY MANAGEMENT MENU   \n");
        printf("==============================\n");
        printf("1. Add Product\n");
        printf("2. Display All Products\n");
        printf("3. Inventory Value + Highest & Lowest Value Products\n");
        printf("4. Search Product by ID\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        /* --- OPTION 1: ADD PRODUCT --- */
        if (choice == 1) {
            if (totalProducts >= 10) {
                printf("\nCannot add more than 10 products!\n");
                continue;
            }

            printf("\nEnter Product ID: ");
            scanf("%d", &productID[totalProducts]);

            printf("Enter Product Name: ");
            scanf("%s", name[totalProducts]);

            printf("Enter Quantity: ");
            scanf("%d", &quantity[totalProducts]);

            printf("Enter Price per Item: ");
            scanf("%f", &price[totalProducts]);

            totalProducts++;
            printf("\nProduct Added Successfully!\n");
        }

        /* --- OPTION 2: DISPLAY ALL PRODUCTS --- */
        else if (choice == 2) {
            if (totalProducts == 0) {
                printf("\nNo products available!\n");
            } 
            else {
                printf("\n--- PRODUCT LIST ---\n");
                for (int i = 0; i < totalProducts; i++) {
                    printf("ID: %d | Name: %s | Qty: %d | Price: %.2f\n",
                           productID[i], name[i], quantity[i], price[i]);
                }
            }
        }

        /* --- OPTION 3: CALCULATE TOTAL INVENTORY VALUE & EXTREMES --- */
        else if (choice == 3) {
            if (totalProducts == 0) {
                printf("\nNo products available!\n");
            }
            else {
                float totalValue = 0;
                float highestValue = quantity[0] * price[0];
                float lowestValue = quantity[0] * price[0];
                int highIndex = 0, lowIndex = 0;

                for (int i = 0; i < totalProducts; i++) {
                    float value = quantity[i] * price[i];
                    totalValue += value;

                    if (value > highestValue) {
                        highestValue = value;
                        highIndex = i;
                    }

                    if (value < lowestValue) {
                        lowestValue = value;
                        lowIndex = i;
                    }
                }

                printf("\nTotal Inventory Value: %.2f\n", totalValue);

                printf("\nHighest Value Product: %s (%.2f)\n",
                       name[highIndex], highestValue);

                printf("Lowest Value Product: %s (%.2f)\n",
                       name[lowIndex], lowestValue);
            }
        }

        /* --- OPTION 4: SEARCH PRODUCT BY ID --- */
        else if (choice == 4) {
            if (totalProducts == 0) {
                printf("\nNo products available!\n");
            }
            else {
                int searchID, found = 0;
                printf("\nEnter Product ID to Search: ");
                scanf("%d", &searchID);

                for (int i = 0; i < totalProducts; i++) {
                    if (productID[i] == searchID) {
                        found = 1;
                        printf("\nProduct Found:\n");
                        printf("ID: %d | Name: %s | Qty: %d | Price: %.2f\n",
                               productID[i], name[i], quantity[i], price[i]);
                        break;
                    }
                }

                if (!found) {
                    printf("\nProduct with ID %d not found.\n", searchID);
                }
            }
        }

        /* --- OPTION 5: EXIT PROGRAM --- */
        else if (choice == 5) {
            printf("\nExiting Program...\n");
            break;
        }

        /* --- INVALID CHOICE --- */
        else {
            printf("\nInvalid choice! Please try again.\n");
        }
    }

    return 0;
}
