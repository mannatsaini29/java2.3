import java.util.*;
import java.util.stream.*;

public class Employee {
    int id;
    String name;
    double salary;
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }
    public String toString() {
        return id + " " + name + " " + salary;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("1. Sort Employees");
        System.out.println("2. Filter and Sort Students");
        System.out.println("3. Stream Operations on Products");
        System.out.print("Enter choice: ");
        int choice = sc.nextInt();

        switch (choice) {
            case 1:
                List<Employee> employees = Arrays.asList(
                        new Employee(101, "Amit", 45000),
                        new Employee(102, "Riya", 52000),
                        new Employee(103, "Karan", 40000),
                        new Employee(104, "Neha", 60000)
                );
                System.out.println("\nOriginal List:");
                employees.forEach(System.out::println);
                System.out.println("\nSorted by Name:");
                employees.stream()
                         .sorted((e1, e2) -> e1.name.compareTo(e2.name))
                         .forEach(System.out::println);
                System.out.println("\nSorted by Salary (Descending):");
                employees.stream()
                         .sorted((e1, e2) -> Double.compare(e2.salary, e1.salary))
                         .forEach(System.out::println);
                break;

            case 2:
                class Student {
                    int rollNo;
                    String name;
                    double marks;
                    Student(int rollNo, String name, double marks) {
                        this.rollNo = rollNo;
                        this.name = name;
                        this.marks = marks;
                    }
                    public String toString() {
                        return rollNo + " " + name + " " + marks;
                    }
                }
                List<Student> students = Arrays.asList(
                        new Student(1, "Ravi", 85.5),
                        new Student(2, "Meena", 92.0),
                        new Student(3, "Asha", 74.2),
                        new Student(4, "Raj", 88.6)
                );
                System.out.println("\nStudents with marks > 80 (sorted by marks):");
                students.stream()
                        .filter(s -> s.marks > 80)
                        .sorted(Comparator.comparingDouble(s -> s.marks))
                        .forEach(System.out::println);
                System.out.println("\nStudents sorted by name:");
                students.stream()
                        .sorted(Comparator.comparing(s -> s.name))
                        .forEach(System.out::println);
                break;

            case 3:
                class Product {
                    int id;
                    String name;
                    double price;
                    Product(int id, String name, double price) {
                        this.id = id;
                        this.name = name;
                        this.price = price;
                    }
                    public String toString() {
                        return id + " " + name + " " + price;
                    }
                }
                List<Product> products = Arrays.asList(
                        new Product(1, "Laptop", 65000),
                        new Product(2, "Phone", 35000),
                        new Product(3, "Tablet", 25000),
                        new Product(4, "Monitor", 15000)
                );
                System.out.println("\nProducts with price > 20000:");
                products.stream()
                        .filter(p -> p.price > 20000)
                        .forEach(System.out::println);
                System.out.println("\nProduct Names:");
                products.stream()
                        .map(p -> p.name)
                        .forEach(System.out::println);
                double totalPrice = products.stream()
                        .map(p -> p.price)
                        .reduce(0.0, Double::sum);
                System.out.println("\nTotal Price of All Products: " + totalPrice);
                List<String> names = products.stream()
                        .map(p -> p.name)
                        .collect(Collectors.toList());
                System.out.println("\nCollected Names List: " + names);
                break;

            default:
                System.out.println("Invalid choice");
        }
        sc.close();
    }
}
