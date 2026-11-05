[README.md](https://github.com/user-attachments/files/34412472/README.md)
# PAPGroupA_Project# Municipal Financial Management System (MFMS)

## Group Information
- **Group Name:** MFMS
- **Group Number:** Group 5
- **Course:** PAP521S – Programming in Practice
- **Institution:** Namibia University of Science and Technology

| Name | Student Number | Responsibility |
|---|---|---|
| Alfeus Rosalia | 224009893 | Employee Management |
| Nangolo Drothea | 223039985 | Supplier Management |
| Siyanda Ndhlovu | 223127981 | Asset Management |
| Andreas Niipare | 223118958 | Budget Management |
| Allan Lunga | 225061333 | Report Management |

## Project Description
A menu-driven system to manage municipal employees, budgets, suppliers, assets, and generate reports — developed as the Project A foundation system.

## System Features
- **Employee Management** — add, display and search employees (by name); calculates each employee's total salary
- **Budget Management** — enter departmental budgets, record expenditure, calculate the remaining budget, check status and list departments over budget
- **Supplier Management** — register, list and search suppliers (by name or service, ignoring capital letters)
- **Asset Management** — add assets, display the asset register, search by ID, department or type, and show a value summary
- **Reports** — Employee, Budget, Supplier and Asset reports
- **Input validation** in every menu and form

## Compilation Instructions
Open a terminal in the project folder, then:
```bash
cd "C codes"
gcc -std=c99 -Wall -Wextra main.c employees.c budget_management.c suppliers.c assets.c reports.c -o mfms
```

## How to Run
```bash
.\mfms.exe
```
(On Linux or macOS: `./mfms`)

## Functions, Integration and Validation

### Functions
The system has **five core management modules**:

- **Employee Management** (`employees.c`)
  - Adds, displays and searches employees; calculates salaries
  - Stores: employee ID, name, department, basic salary, housing allowance, transport allowance
  - Key functions: `employeeMenu()`, `addEmployee()`, `displayEmployees()`, `searchEmployee()`, `calculateSalary()`

- **Budget Management** (`budget_management.c`)
  - Sets department budgets; records expenditure; checks budget status
  - Tracks: allocated budget, amount spent, remaining balance
  - Key functions: `budgetMenu()`, `calculateRemaining()`, `displayAll()`, `displayExceeded()`

- **Supplier Management** (`suppliers.c`)
  - Registers new suppliers; displays all; searches by name or service
  - Stores: supplier name, contact person / phone, service or goods provided
  - Key functions: `handleSupplierMenu()`, `addSupplier()`, `displayAllSuppliers()`, `searchSupplier()`

- **Asset Management** (`assets.c`)
  - Adds assets; displays the register; searches by ID, department or type; value summary
  - Stores: asset ID, name, type, purchase value, department, condition
  - Key functions: `assetMenu()`, `addAsset()`, `displayAssets()`, `searchAssetById()`, `searchAssetsByDepartment()`, `searchAssetsByType()`, `assetSummary()`

- **Report Generation** (`reports.c`)
  - Generates individual reports for all modules
  - Summarises totals and status across the system
  - Key functions: `displayReports()`, `employeeReport()`, `budgetReport()`, `supplierReport()`, `assetReport()`

### Integration
- All modules connect through **`main.c`** — one central main menu
- Each module has its own `.h` header file that declares its public functions
- `main.c` includes all headers → calls each module's menu function → returns to the main menu when finished
- The Reports module reads the other modules' data through their header files

### Validation Applied Across All Modules
- **Menu choices** — letters, empty input and numbers outside the menu are rejected with a message, and the menu asks again
- **Empty input** — names, departments and other required fields cannot be left blank
- **Length limits** — text that is too long for its field is rejected
- **Numbers** — salaries, budgets, expenditure and asset values must be valid numbers; negative values are rejected
- **Duplicates** — the same employee ID or asset ID cannot be added twice
- **Full lists** — a message is shown when a module's storage limit is reached

## Testing, Documentation and Git Coordination

### Testing
- **Unit Testing**
  - Supplier Management
    - Created `test_suppliers.c` to run independently without other modules
    - Verified: add supplier, display list, search, empty list, full list, invalid input
  - Employee Management
    - Tested: add employee, search, calculate salary, display all
  - Budget Management
    - Tested: set budget, record spending, check remaining balance
  - Asset Management
    - Tested: add asset, display register, search by ID, department and type, value summary, invalid input

- **Integration Testing**
  - Compiled the full system:
    ```bash
    gcc -std=c99 -Wall -Wextra main.c employees.c budget_management.c suppliers.c assets.c reports.c -o mfms
    ```
  - Ran end-to-end: main menu → enter each module → return to main → exit
  - Verified all modules work together without conflicts

- **Test Cases Run — All Modules:**
  - Supplier — Add new supplier → saves & displays correctly
  - Supplier — Empty list → shows "No suppliers registered"
  - Supplier — Search existing → finds & shows details
  - Supplier — Search non-existent → shows "No supplier matching"
  - Supplier — Empty name → rejected
  - Employee — Add employee → displays; search by name → finds match
  - Employee — Letters or negative number as ID → rejected
  - Budget — Set budget → record expense → updates remaining; over budget → warning
  - Asset — Add asset → search by ID → returns correct record
  - System-wide — Invalid menu choice (letters or wrong number) → shows error & asks again
  - All modules → return to main menu correctly

### Documentation
- Every `.c` and `.h` file includes:
  - Module description at the top
  - Author name & student number
  - Function purpose comments
- **README.md** contains: project overview, group members, responsibilities, compile/run instructions, and this report
- Consistent naming, indentation and formatting applied across all files

### Git Coordination
- All code stored in a shared GitHub repository
- Workflow followed for every update:
  ```bash
  git add .
  git commit -m "Description of changes"
  git push
  ```
