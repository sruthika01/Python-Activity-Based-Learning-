# Problem Statement
To develop a Python program using nested lists to compare product quantities across multiple warehouses. The program identifies stock shortages and surpluses, compares available quantities with specified stock targets, and calculates the transfers required to balance inventory between warehouses.
# Algorithm
1. Start the program.
2. Define warehouse names, product names, and stock targets.
3. Store product quantities in a nested list.
4. Calculate the total stock of each product across all warehouses.
5. Compare each warehouse's stock with its target.
6. Identify shortages and surpluses.
7. Calculate the required transfers from surplus warehouses to shortage warehouses.
8. Display stock details and transfer requirements.
9. Stop the program.
 # Mermaid Flowchart
 ```mermaid
flowchart TD
    A([Start]) --> B[Define warehouses, products and targets]
    B --> C[Store inventory in nested lists]
    C --> D[Compare stock with target]
    D --> E{Stock below target?}
    E -->|Yes| F[Identify shortage]
    E -->|No| G{Stock above target?}
    G -->|Yes| H[Identify surplus]
    G -->|No| I[Stock balanced]
    F --> J[Calculate transfers]
    H --> J
    I --> J
    J --> K[Display reconciliation report]
```
# Source code

# Inventory Matrix Reconciliation

warehouses = ["Warehouse A", "Warehouse B", "Warehouse C"]
products = ["Laptop", "Mouse", "Keyboard"]

# Rows represent warehouses; columns represent products
stock = [
    [50, 20, 40],
    [20, 60, 30],
    [40, 30, 50]
]

# Required stock targets for each warehouse and product
targets = [
    [40, 30, 40],
    [30, 40, 30],
    [40, 40, 50]
]

print("INVENTORY RECONCILIATION")

# Identify shortages and surpluses
for j, product in enumerate(products):
    print(f"\nProduct: {product}")

    shortages = []
    surpluses = []

    for i, warehouse in enumerate(warehouses):
        difference = stock[i][j] - targets[i][j]

        if difference < 0:
            shortage = -difference
            shortages.append([i, shortage])
            print(f"{warehouse}: Shortage = {shortage}")

        elif difference > 0:
            surpluses.append([i, difference])
            print(f"{warehouse}: Surplus = {difference}")

        else:
            print(f"{warehouse}: Stock balanced")

    # Match surplus stock with shortages
    print("Required Transfers:")

    s = 0
    d = 0

    while s < len(surpluses) and d < len(shortages):
        source = surpluses[s][0]
        available = surpluses[s][1]

        destination = shortages[d][0]
        needed = shortages[d][1]

        quantity = min(available, needed)

        print(
            f"Transfer {quantity} units from "
            f"{warehouses[source]} to "
            f"{warehouses[destination]}"
        )

        surpluses[s][1] -= quantity
        shortages[d][1] -= quantity

        if surpluses[s][1] == 0:
            s += 1

        if shortages[d][1] == 0:
            d += 1

    if d < len(shortages):
        print("Warning: Insufficient surplus stock.")

    if s < len(surpluses):
        print("Remaining surplus:", sum(x[1] for x in surpluses))
# Sample input
Warehouses: Warehouse A, Warehouse B, Warehouse C
Products: Laptop, Mouse, Keyboard

Current Stock:
Warehouse A: 50, 20, 40
Warehouse B: 20, 60, 30
Warehouse C: 40, 30, 50

Target Stock:
Warehouse A: 40, 30, 40
Warehouse B: 30, 40, 30
Warehouse C: 40, 40, 50
# Sample output
INVENTORY RECONCILIATION

Product: Laptop
Warehouse A: Surplus = 10
Warehouse B: Shortage = 10
Warehouse C: Stock balanced
Required Transfers:
Transfer 10 units from Warehouse A to Warehouse B

Product: Mouse
Warehouse A: Shortage = 10
Warehouse B: Surplus = 20
Warehouse C: Shortage = 10
Required Transfers:
Transfer 10 units from Warehouse B to Warehouse A
Transfer 10 units from Warehouse B to Warehouse C

Product: Keyboard
Warehouse A: Stock balanced
Warehouse B: Stock balanced
Warehouse C: Stock balanced
Required Transfers:
# Screen shot
<img width="1320" height="792" alt="image" src="https://github.com/user-attachments/assets/949bb1e7-9bde-448e-8613-c18b6582c452" />

    K --> L([Stop])


