#include <stdio.h>
#include <string.h>

#define MAX_ITEMS 5       // Maximum number of items in the first aid kit
#define MIN_THRESHOLD 2   // Minimum quantity before an item needs restocking

// Structure to store information about each first aid item
struct FirstAidItem {
    char name[50];
    int quantity;
    char guidance[200];  // Instructions on how to use the item
};

// Function to display the inventory of the first aid kit
void displayInventory(struct FirstAidItem kit[], int count) {
    printf("\nFirst Aid Kit Inventory:\n");
    for (int i = 0; i < count; i++) {
        printf("%d. %s (Quantity: %d)\n", i + 1, kit[i].name, kit[i].quantity);
        if (kit[i].quantity <= MIN_THRESHOLD) {
            printf("** Warning: Low stock for %s, please restock! **\n", kit[i].name);
        }
    }
}

// Function to restock an item
void restockItem(struct FirstAidItem kit[], int count) {
    int itemIndex, restockAmount;
    
    printf("\nEnter item number to restock (1 to %d): ", count);
    scanf("%d", &itemIndex);

    if (itemIndex < 1 || itemIndex > count) {
        printf("Invalid item number!\n");
        return;
    }

    printf("Enter quantity to add to %s: ", kit[itemIndex - 1].name);
    scanf("%d", &restockAmount);
    
    kit[itemIndex - 1].quantity += restockAmount;
    printf("%s restocked. New quantity: %d\n", kit[itemIndex - 1].name, kit[itemIndex - 1].quantity);
}

// Function to provide guidance on how to use an item
void provideGuidance(struct FirstAidItem kit[], int count) {
    int itemIndex;

    printf("\nEnter item number to get guidance (1 to %d): ", count);
    scanf("%d", &itemIndex);

    if (itemIndex < 1 || itemIndex > count) {
        printf("Invalid item number!\n");
        return;
    }

    printf("\nGuidance for using %s:\n%s\n", kit[itemIndex - 1].name, kit[itemIndex - 1].guidance);
}

int main() {
    // Initialize the first aid kit with some default items
    struct FirstAidItem kit[MAX_ITEMS] = {
        {"Bandages", 5, "Use bandages to cover small wounds to prevent infection."},
        {"Antiseptic Wipes", 2, "Use antiseptic wipes to clean wounds before applying bandages."},
        {"Gauze Pads", 1, "Use gauze pads to control bleeding from larger wounds."},
        {"Burn Ointment", 4, "Apply burn ointment to minor burns to prevent infection."},
        {"Adhesive Tape", 3, "Use adhesive tape to secure bandages or gauze pads."}
    };
    int choice;

    while (1) {
        printf("\n--- Smart First Aid Kit Menu ---\n");
        printf("1. Display Inventory\n");
        printf("2. Restock an Item\n");
        printf("3. Get Guidance on an Item\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: 
                displayInventory(kit, MAX_ITEMS);
                break;
            case 2:
                restockItem(kit, MAX_ITEMS);
                break;
            case 3:
                provideGuidance(kit, MAX_ITEMS);
                break;
            case 4:
                printf("Exiting the program. Stay safe!\n");
                return 0;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }

    return 0;
}
