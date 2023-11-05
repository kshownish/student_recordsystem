
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.stream.Collectors;

class Student {
    private String name;
    private int id;
    private double grade;
    private String section;

    public Student(String name, int id, double grade, String section) {
        this.name = name;
        this.id = id;
        this.grade = grade;
        this.section = section;
    }

    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }

    public double getGrade() {
        return grade;
    }

    public String getSection() {
        return section;
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("Student Record System Menu:");
            System.out.println("1. Add Student");
            System.out.println("2. Generate Report");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    addStudent(students, scanner);
                    break;
                case 2:
                    generateReport(students, scanner);
                    break;
                case 3:
                    System.out.println("Exiting the program.");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    private static void addStudent(List<Student> students, Scanner scanner) {
        System.out.print("Enter student name: ");
        String name = scanner.nextLine();

        System.out.print("Enter student ID: ");
        int id = scanner.nextInt();

        scanner.nextLine(); // Consume newline

        System.out.print("Enter student section: ");
        String section = scanner.nextLine();

        System.out.print("Enter student grade: ");
        double grade = scanner.nextDouble();

        Student student = new Student(name, id, grade, section);
        students.add(student);
        System.out.println("Student added successfully.");
    }

    private static void generateReport(List<Student> students, Scanner scanner) {
        if (students.isEmpty()) {
            System.out.println("No students in the record.");
            return;
        }

        System.out.println("Student Report Menu:");
        System.out.println("1. Print specific student info");
        System.out.println("2. Print everyone's records");
        System.out.println("3. Print records for a specific section");
        System.out.print("Enter your choice: ");

        int choice = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        switch (choice) {
            case 1:
                System.out.print("Enter student ID to print info: ");
                int studentId = scanner.nextInt();
                printStudentInfo(students, studentId);
                break;
            case 2:
                printAllRecords(students);
                break;
            case 3:
                System.out.print("Enter section to print records: ");
                String section = scanner.nextLine();
                printSectionRecords(students, section);
                break;
            default:
                System.out.println("Invalid choice. Please try again.");
        }
    }

    private static void printStudentInfo(List<Student> students, int studentId) {
        for (Student student : students) {
            if (student.getId() == studentId) {
                System.out.println("Name: " + student.getName());
                System.out.println("ID: " + student.getId());
                System.out.println("Section: " + student.getSection());
                System.out.println("Grade: " + student.getGrade());
                return;
            }
        }
        System.out.println("Student with ID " + studentId + " not found.");
    }

    private static void printAllRecords(List<Student> students) {
        System.out.println("Student Report:");
        for (Student student : students) {
            System.out.println("Name: " + student.getName());
            System.println("ID: " + student.getId());
            System.out.println("Section: " + student.getSection());
            System.out.println("Grade: " + student.getGrade());
            System.out.println();
        }
    }

    private static void printSectionRecords(List<Student> students, String section) {
        List<Student> sectionStudents = students.stream()
            .filter(student -> student.getSection().equals(section))
            .collect(Collectors.toList());

        if (sectionStudents.isEmpty()) {
            System.out.println("No students in the section: " + section);
            return;
        }

        System.out.println("Student Report for Section " + section + ":");
        for (Student student : sectionStudents) {
            System.out.println("Name: " + student.getName());
            System.out.println("ID: " + student.getId());
            System.out.println("Grade: " + student.getGrade());
            System.out.println();
        }
    }
}
```

In this modified code, the edit and delete functions have been removed, and the program focuses on adding students, generating reports, and managing student information without the edit or delete functionality.
