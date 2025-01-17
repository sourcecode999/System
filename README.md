#include <stdio.h>
#include <string.h>

#define MAX_EMPLOYEES 10

// Structure to hold employee data
typedef struct {
    int id;
    char name[50];
    float salary;
} Employee;

// Array to store employees
Employee employees[MAX_EMPLOYEES];
int employeeCount = 0;

// Function prototypes
void addEmployee();
void displayEmployees();
void updateEmployee();
void deleteEmployee();

int main() {
    int choice;

    do {
        printf("\nEmployee Management System\n");
        printf("1. Add Employee\n");
        printf("2. Display Employees\n");
        printf("3. Update Employee\n");
        printf("4. Delete Employee\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addEmployee();
                break;
            case 2:
                displayEmployees();
                break;
            case 3:
                updateEmployee();
                break;
            case 4:
                deleteEmployee();
                break;
            case 5:
                printf("Exiting the program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 5);

    return 0;
}

// Function to add a new employee
void addEmployee() {
    if (employeeCount >= MAX_EMPLOYEES) {
        printf("Cannot add more employees. Maximum limit reached.\n");
        return;
    }

    Employee emp;
    printf("Enter Employee ID: ");
    scanf("%d", &emp.id);
    printf("Enter Employee Name: ");
    scanf(" %[^\n]", emp.name);
    printf("Enter Employee Salary: ");
    scanf("%f", &emp.salary);

    employees[employeeCount++] = emp;
    printf("Employee added successfully!\n");
}

// Function to display all employees
void displayEmployees() {
    if (employeeCount == 0) {
        printf("No employees to display.\n");
        return;
    }

    printf("\nEmployee List:\n");
    for (int i = 0; i < employeeCount; i++) {
        printf("ID: %d, Name: %s, Salary: %.2f\n",
               employees[i].id, employees[i].name, employees[i].salary);
    }
}

// Function to update an employee's details
void updateEmployee() {
    int id, found = 0;
    printf("Enter Employee ID to update: ");
    scanf("%d", &id);

    for (int i = 0; i < employeeCount; i++) {
        if (employees[i].id == id) {
            printf("Enter New Name: ");
            scanf(" %[^\n]", employees[i].name);
            printf("Enter New Salary: ");
            scanf("%f", &employees[i].salary);
            found = 1;
            printf("Employee updated successfully!\n");
            break;
        }
    }

    if (!found) {
        printf("Employee with ID %d not found.\n", id);
    }
}

// Function to delete an employee by ID
void deleteEmployee() {
    int id, found = 0;
    printf("Enter Employee ID to delete: ");
    scanf("%d", &id);

    for (int i = 0; i < employeeCount; i++) {
        if (employees[i].id == id) {
            for (int j = i; j < employeeCount - 1; j++) {
                employees[j] = employees[j + 1];
            }
            employeeCount--;
            found = 1;
            printf("Employee deleted successfully!\n");
            break;
        }
    }

    if (!found) {
        printf("Employee with ID %d not found.\n", id);
    }
}


