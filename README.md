# Employee-working-hour-schedule
Employee working hour Schedulee
#include <stdio.h>
#include <string.h>

struct Employee {
    int empID;
    char name[50];
    int hoursWorked[7]; // Hours for each day of the week (7 days)
};

void addEmployee(struct Employee employees[], int *count) {
    if (*count >= 100) {
        printf("Database full.\n");
        return;
    }

    printf("Enter Employee ID: ");
    scanf("%d", &employees[*count].empID);
    printf("Enter Employee Name: ");
    scanf(" %[^\n]", employees[*count].name);

    printf("Enter hours worked for each day (Mon to Sun):\n");
    for (int i = 0; i < 7; i++) {
        printf("Day %d: ", i + 1);
        scanf("%d", &employees[*count].hoursWorked[i]);
    }

    (*count)++;
    printf("Employee work schedule added.\n");
}

void displaySchedule(struct Employee employees[], int count) {
    printf("\n--- Employee Work Schedules ---\n");
    for (int i = 0; i < count; i++) {
        printf("ID: %d | Name: %s | Weekly Hours: ",
               employees[i].empID, employees[i].name);
        int total = 0;
        for (int j = 0; j < 7; j++) {
            printf("%d ", employees[i].hoursWorked[j]);
            total += employees[i].hoursWorked[j];
        }
        printf("| Total Hours: %d\n", total);
    }
}

void searchEmployee(struct Employee employees[], int count) {
    int id;
    printf("Enter Employee ID to search: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (employees[i].empID == id) {
            printf("Found Employee: %s\n", employees[i].name);
            printf("Daily Hours: ");
            int total = 0;
            for (int j = 0; j < 7; j++) {
                printf("%d ", employees[i].hoursWorked[j]);
                total += employees[i].hoursWorked[j];
            }
            printf("| Total Weekly Hours: %d\n", total);
            return;
        }
    }
    printf("Employee not found.\n");
}

int main() {
    struct Employee employees[100];
    int count = 0;
    int choice;

    while (1) {
        printf("\n--- Employee Working Hours Menu ---\n");
        printf("1. Add Employee Schedule\n");
        printf("2. Display All Schedules\n");
        printf("3. Search Employee Schedule\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            addEmployee(employees, &count);
            break;
        case 2:
            displaySchedule(employees, count);
            break;
        case 3:
            searchEmployee(employees, count);
            break;
        case 4:
            printf("Exiting...\n");
            return 0;
        default:
            printf("Invalid choice. Try again.\n");
        }
    }

    return 0;
}
