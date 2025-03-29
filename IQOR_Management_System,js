const readline = require("readline-sync");

class Employee {
    constructor(id, name, department, status, ratePerHr, hoursWorked, dateHired) {
        this.employeeID = id;
        this.employeeName = name;
        this.department = department;
        this.employeeStatus = this.getStatusFromNumber(status);
        this.ratePerHr = ratePerHr;
        this.hoursWorked = hoursWorked;
        this.dateHired = dateHired;
        this.Salary();
    }

    getStatusFromNumber(num) {
        const statuses = { "1": "Probational", "2": "Permanent", "3": "Contractual" };
        return statuses[num] || "Unknown";
    }

    Salary() {
        let baseMultiplier;
        let overtimeRate;

        if (this.employeeStatus === "Permanent") {
            baseMultiplier = 1.2;
            overtimeRate = 2.0;
        } else if (this.employeeStatus === "Probational") {
            baseMultiplier = 1.1;
            overtimeRate = 1.75;
        } else {
            baseMultiplier = 1.0;
            overtimeRate = 1.5;
        }

        this.grossPay = this.hoursWorked * this.ratePerHr * baseMultiplier;
        let overtimeHours = Math.max(0, this.hoursWorked - 40);
        this.overtimePay = overtimeHours * this.ratePerHr * overtimeRate;
        this.totalPay = this.grossPay + this.overtimePay;
    }
}

class EmployeeManager {
    constructor() {
        this.employees = [];
    }

    addEmployee(emp) {
        this.employees.push(emp);
    }

    findEmployee(id) {
        return this.employees.find(emp => emp.employeeID === id);
    }

    deleteEmployee(id) {
        let index = this.employees.findIndex(emp => emp.employeeID === id);
        if (index !== -1) {
            this.employees.splice(index, 1);
            return true;
        }
        return false;
    }
}

const manager = new EmployeeManager();

function Menu() {
    console.log("      IQOR EMPLOYEE MANAGEMENT SYSTEM      ");
    console.log("==========================================\n");
    console.log("1. Add Employee Record");
    console.log("2. Edit Employee Information");
    console.log("3. Delete Employee Record");
    console.log("4. Search Employee");
    console.log("5. Exit\n");
}

function handleUserInput() {
    let isRunning = true;

    while (isRunning) {
        Menu();
        let option = readline.question("Enter Option Number [1-5]: ").trim();

        switch (option) {
            case "1":
                addEmployeeRecord();
                break;
            case "2":
                editEmployeeRecord();
                break;
            case "3":
                deleteEmployeeRecord();
                break;
            case "4":
                searchEmployee();
                break;
            case "5":
                console.log("\nExiting Program...");
                isRunning = false;
                break;
            default:
                console.log("\nInsert a valid input! Please choose between 1-5.");
                break;
        }
    }
}

function addEmployeeRecord() {
    console.log("\n===========Create/Add Employee Information===========\n");

    let ID = parseInt(readline.question("Enter Employee ID: "));
    let name = readline.question("Enter Employee Name: ");
    let department = readline.question("Enter Employee Department: ");

    let status;
    while (true) {
        console.log("\nChoose Employee Status:");
        console.log("1. Probational");
        console.log("2. Permanent");
        console.log("3. Contractual");
        status = readline.question("Enter choice [1-3]: ");
        if (["1", "2", "3"].includes(status)) break;
        console.log("Invalid input! Choose between 1-3.");
    }

    let rate = parseFloat(readline.question("Enter Employee Rate/Hr (PHP): "));
    let hoursWorked = parseFloat(readline.question("Enter Hours Worked: "));
    let dateHired = readline.question("Enter Date Hired (MM/DD/YYYY): ");

    let newEmployee = new Employee(ID, name, department, status, rate, hoursWorked, dateHired);
    manager.addEmployee(newEmployee);
    console.log("\nEmployee has been added successfully!\n");
}

function editEmployeeRecord() {
    let ID = parseInt(readline.question("\nEnter Employee ID: "));

    let emp = manager.findEmployee(ID);
    if (!emp) {
        console.log("\nEmployee Not Found!\n");
        return;
    }

    console.log("\nEditing Employee Record");
    console.log("1. Name");
    console.log("2. Department");
    console.log("3. Status");
    console.log("4. Rate per Hour");
    console.log("5. Hours Worked");

    let option = readline.question("\nEnter field number: ").trim();

    switch (option) {
        case "1":
            emp.employeeName = readline.question("Enter New Name: ");
            break;
        case "2":
            emp.department = readline.question("Enter New Department: ");
            break;
        case "3":
            while (true) {
                console.log("\nChoose New Employee Status:");
                console.log("1. Probational");
                console.log("2. Permanent");
                console.log("3. Contractual");
                let status = readline.question("Enter choice [1-3]: ");
                if (["1", "2", "3"].includes(status)) {
                    emp.employeeStatus = emp.getStatusFromNumber(status);
                    emp.Salary();
                    break;
                }
                console.log("Invalid input! Choose between 1-3.");
            }
            break;
        case "4":
            emp.ratePerHr = parseFloat(readline.question("Enter New Rate Per Hour (PHP): "));
            emp.Salary();
            break;
        case "5":
            emp.hoursWorked = parseFloat(readline.question("Enter New Hours Worked: "));
            emp.Salary();
            break;
        default:
            console.log("Please insert a Valid Input!");
            return;
    }

    console.log("\nEmployee Record Updated!\n");
}

function deleteEmployeeRecord() {
    let ID = parseInt(readline.question("\nEnter Employee ID to Delete: "));

    if (manager.deleteEmployee(ID)) {
        console.log("\nEmployee Deleted Successfully!\n");
    } else {
        console.log("\nEmployee Not Found!\n");
    }
}

function searchEmployee() {
    let ID = parseInt(readline.question("\nEnter Employee ID: "));

    let emp = manager.findEmployee(ID);
    if (!emp) {
        console.log("\nEmployee Not Found!\n");
        return;
    }

    console.log("\n===== Employee Details =====");
    console.log(`ID: ${emp.employeeID}`);
    console.log(`Name: ${emp.employeeName}`);
    console.log(`Department: ${emp.department}`);
    console.log(`Status: ${emp.employeeStatus}`);
    console.log(`Rate Per Hour: PHP ${emp.ratePerHr}`);
    console.log(`Hours Worked: ${emp.hoursWorked}`);
    console.log(`Date Hired: ${emp.dateHired}`);
    console.log(`Gross Pay: PHP ${emp.grossPay.toFixed(2)}`);
    console.log(`Overtime Pay: PHP ${emp.overtimePay.toFixed(2)}`);
    console.log(`Total Pay: PHP ${emp.totalPay.toFixed(2)}\n`);
}

handleUserInput();
