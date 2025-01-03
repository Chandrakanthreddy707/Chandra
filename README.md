#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 100

typedef struct {
    int id;
    char name[100];
    char grade[3];
    float marks;
} Student;

Student students[MAX_STUDENTS];
int student_count = 0;

void add_student() {
    if (student_count >= MAX_STUDENTS) {
        printf("Max student limit reached.\n");
        return;
    }

    Student new_student;
    printf("Enter ID: ");
    scanf("%d", &new_student.id);
    printf("Enter name: ");
    scanf("%s", new_student.name);
    printf("Enter grade: ");
    scanf("%s", new_student.grade);
    printf("Enter marks: ");
    scanf("%f", &new_student.marks);

    students[student_count++] = new_student;
    printf("Student added successfully.\n");
}

void search_student_by_id(int id) {
    for (int i = 0; i < student_count; i++) {
        if (students[i].id == id) {
            printf("ID: %d, Name: %s, Grade: %s, Marks: %.2f\n", students[i].id, students[i].name, students[i].grade, students[i].marks);
            return;
        }
    }
    printf("Student not found.\n");
}

void search_student_by_name(char name[]) {
    for (int i = 0; i < student_count; i++) {
        if (strcmp(students[i].name, name) == 0) {
            printf("ID: %d, Name: %s, Grade: %s, Marks: %.2f\n", students[i].id, students[i].name, students[i].grade, students[i].marks);
            return;
        }
    }
    printf("Student not found.\n");
}

void display_all_students() {
    for (int i = 0; i < student_count; i++) {
        printf("ID: %d, Name: %s, Grade: %s, Marks: %.2f\n", students[i].id, students[i].name, students[i].grade, students[i].marks);
    }
}

void calculate_average_marks() {
    if (student_count == 0) {
        printf("No student records available.\n");
        return;
    }

    float total_marks = 0.0;
    for (int i = 0; i < student_count; i++) {
        total_marks += students[i].marks;
    }
    printf("Average Marks: %.2f\n", total_marks / student_count);
}

int main() {
    int choice, id;
    char name[100];

    while (1) {
        printf("\nStudent Record Management System\n");
        printf("1. Add Student Record\n");
        printf("2. Search Student by ID\n");
        printf("3. Search Student by Name\n");
        printf("4. Display All Student Records\n");
        printf("5. Calculate Average Marks\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                add_student();
                break;
            case 2:
                printf("Enter ID: ");
                scanf("%d", &id);
                search_student_by_id(id);
                break;
            case 3:
                printf("Enter name: ");
                scanf("%s", name);
                search_student_by_name(name);
                break;
            case 4:
                display_all_students();
                break;
            case 5:
                calculate_average_marks();
                break;
            case 6:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
