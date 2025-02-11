# Employee-Leave-Management-System.java
public class Employee {
    private String name;
    private String employeeId;
    private int leaveBalance;

    public Employee(String name, String employeeId, int leaveBalance) {
        this.name = name;
        this.employeeId = employeeId;
        this.leaveBalance = leaveBalance;
    }

    public String getName() {
        return name;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public int getLeaveBalance() {
        return leaveBalance;
    }

    public void setLeaveBalance(int leaveBalance) {
        this.leaveBalance = leaveBalance;
    }
}


Leave.java

public class Leave {
    private String leaveType;
    private int numberOfDays;

    public Leave(String leaveType, int numberOfDays) {
        this.leaveType = leaveType;
        this.numberOfDays = numberOfDays;
    }

    public String getLeaveType() {
        return leaveType;
    }

    public int getNumberOfDays() {
        return numberOfDays;
    }
}


EmployeeLeaveManagementSystem.java

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class EmployeeLeaveManagementSystem {
    private List<Employee> employees;
    private Scanner scanner;

    public EmployeeLeaveManagementSystem() {
        employees = new ArrayList<>();
        scanner = new Scanner(System.in);
    }

    public void run() {
        while (true) {
            System.out.println("Employee Leave Management System");
            System.out.println("1. Add Employee");
            System.out.println("2. Apply Leave");
            System.out.println("3. View Employee Leave Balance");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            switch (option) {
                case 1:
                    addEmployee();
                    break;
                case 2:
                    applyLeave();
                    break;
                case 3:
                    viewEmployeeLeaveBalance();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid option. Please choose again.");
            }
        }
    }

    private void addEmployee() {
        System.out.print("Enter employee name: ");
        String name = scanner.nextLine();
        System.out.print("Enter employee ID: ");
        String employeeId = scanner.nextLine();
        System.out.print("Enter leave balance: ");
        int leaveBalance = scanner.nextInt();
        scanner.nextLine(); // Consume newline left-over

        Employee employee = new Employee(name, employeeId, leaveBalance);
        employees.add(employee);
        System.out.println("Employee added successfully!");
    }

    private void applyLeave() {
        System.out.print("Enter employee ID: ");
        String employeeId = scanner.nextLine();
        Employee employee = findEmployee(employeeId);

        if (employee != null) {
            System.out.print("Enter leave type: ");
            String leaveType = scanner.nextLine();
            System.out.print("Enter number of days: ");
            int numberOfDays = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            Leave leave = new Leave(leaveType, numberOfDays);
            employee.setLeaveBalance(employee.getLeaveBalance() - numberOfDays);
            System.out.println("Leave applied successfully!");
        } else {
            System.out.println("Employee not found!");
        }
    }

    private void viewEmployeeLeaveBalance() {
        System.out.print("Enter employee ID: ");
        String employeeId = scanner.nextLine();
        Employee employee = findEmployee(employeeId);

        if (employee != null) {
            System.out.println("Leave balance: " + employee.getLeaveBalance());
        } else {
            System.out.println("Employee not found!");
        }
    }

    private Employee findEmployee(String employeeId) {
        for (Employee employee : employees) {
            if (employee.getEmployeeId().equals(employeeId)) {
                return employee;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        EmployeeLeaveManagementSystem system = new EmployeeLeaveManagementSystem();
        system.run();
    }
}
