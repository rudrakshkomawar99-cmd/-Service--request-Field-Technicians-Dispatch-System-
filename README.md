# -Service--request-Field-Technicians-Dispatch-System-
This is code of a technicians request system in which both DOMESTIC/COMMERCIAL user can request for available technicians and can get a quotation for their total cost
#include <stdio.h>

int main() {
    char name[50], address[100], contact[20];
    int user_type, tech_type, num_tech, n;
    float cost = 0, budget = 0, total_cost = 0;

    printf("WELCOME TO TECHNICIANS DISPATCH SYSTEM\n");

    printf("Enter Your Name: ");
    scanf("%s", name);

    printf("Enter Your Address: ");
    scanf("%s", address);

    printf("Enter Your Contact Info: ");
    scanf("%s", contact);

    printf("Are you DOMESTIC (1) or COMMERCIAL (0)? ");
    scanf("%d", &user_type);

    printf("\nAvailable Technicians:\n");
    printf("1. Electrician\n2. Plumber\n3. Medical Help\n4. Emergency Services\n");

    // Domestic user logic (simplified)
    if (user_type == 1) {
    start_domestic:
        printf("\nSelect Technician:\nChoice: ");
        scanf("%d", &tech_type);

        if (tech_type == 1) cost = 100;
        else if (tech_type == 2) cost = 80;
        else if (tech_type == 3) cost = 120;
        else if (tech_type == 4) cost = 150;
        else {
            printf("Invalid Technician choice.\n");
            goto start_domestic;
        }

        total_cost = cost - (cost * 0.20); // 20% discount for domestic user
        num_tech = 1;

        printf("\n--- SUMMARY ---\n");
        printf("Name: %s\nAddress: %s\nContact: %s\n", name, address, contact);
        printf("User Type: Domestic\n");
        printf("Selected Technician: ");
        if (tech_type == 1) printf("Electrician\n");
        else if (tech_type == 2) printf("Plumber\n");
        else if (tech_type == 3) printf("Medical Help\n");
        else printf("Emergency Services\n");

        printf("Total Technicians: %d\n", num_tech);
        printf("Total Cost: ₹%f\n", total_cost);
    }

    //  for Commercial 
    else {
        printf("How many types of services do you need: ");
        scanf("%d", &n);

        int total_techs = 0;

        for (int i = 1; i <= n; i++) {
        start_commercial:
            printf("\nSelect Technician Type %d:\n", i);
            printf("1. Electrician\n2. Plumber\n3. Medical Help\n4. Emergency Services\nChoice: ");
            scanf("%d", &tech_type);

            if (tech_type == 1) cost = 100;
            else if (tech_type == 2) cost = 80;
            else if (tech_type == 3) cost = 120;
            else if (tech_type == 4) cost = 150;
            else {
                printf("Invalid Technician choice.\n");
                goto start_commercial;
            }

            printf("Number of technicians needed: ");
            scanf("%d", &num_tech);

            total_cost += cost * num_tech;
            total_techs += num_tech;
        }

    budget_entry:
        printf("\nEnter your budget: ");
        scanf("%f", &budget);

        if (budget == 0) {
            printf("Request cancelled.\n");
            return 0;
        }
        if (budget < total_cost) {
            printf("Budget too low. Total cost is %f\n", total_cost);
            goto budget_entry;
        }
        if (budget > total_cost) {
            total_cost = budget;
        }

        printf("\n--- SUMMARY ---\n");
        printf("Name: %s\nAddress: %s\nContact: %s\n", name, address, contact);
        printf("User Type: Commercial\n");
        printf("Total Technicians: %d\n", total_techs);
        printf("Total Cost: ₹%f\n", total_cost);
    }

    return 0;
}
