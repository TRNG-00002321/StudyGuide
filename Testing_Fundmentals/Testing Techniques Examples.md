## Equivalence partitioning
**Example:**
A form accepts age input from users, with valid ages between 18 and 60 inclusive.  
**Step 1:** Identify input domain: Age field (integer).  
**Step 2:** Define equivalence classes:  
| Class | Range | Type    |
| ----- | ----- | ------- |
| EC1   | 18–60 | Valid   |
| EC2   | <18   | Invalid |
| EC3   | >60   | Invalid |


## Boundary Value Analysis (BVA)
**Example:**
A form accepts age input from users, valid between 18 and 60 inclusive.  
**Step 1:** Identify boundaries:
Minimum = 18
Maximum = 60  
**Step 2:** Determine test values:
- Just below minimum = 17
- Minimum = 18
- Just above minimum = 19
- Just below maximum = 59
- Maximum = 60
- Just above maximum = 61

| Test Case | Input | Expected Result  |
| --------- | ----- | ---------------- |
| TC1       | 17    | Reject (invalid) |
| TC2       | 18    | Accept (valid)   |
| TC3       | 19    | Accept (valid)   |
| TC4       | 59    | Accept (valid)   |
| TC5       | 60    | Accept (valid)   |
| TC6       | 61    | Reject (invalid) |


## State Transition Diagram (STD)
**Example: Vending Machine**
A vending machine that dispenses drinks costing $1.

**States:**
- Idle : waiting for coins
- Has 50¢ : 50 cents inserted
- Has $1 : enough money inserted
- Dispensed : drink has been given

**Events/Inputs:**
- Insert 50¢  
- Insert $1
- Press "Dispense"

| Current State | Event/Input    | Next State | Output/Action        |
| ------------- | -------------- | ---------- | -------------------- |
| Idle          | Insert 50¢     | Has 50¢    | Display 50¢ inserted |
| Idle          | Insert $1      | Has $1     | Display $1 inserted  |
| Has 50¢       | Insert 50¢     | Has $1     | Display $1 inserted  |
| Has 50¢       | Press Dispense | Has 50¢    | Not enough money     |
| Has $1        | Press Dispense | Dispensed  | Dispense drink       |
| Dispensed     | -              | Idle       | Reset machine        |

## Decision Table
**Example:** A loan approval system with two conditions:
- Credit Score ≥ 700 → Good / Bad
- Income ≥ $50,000 → High / Low

**Action:** Approve or Reject the loan.

| Rule | Credit Score ≥ 700? | Income ≥ 50,000? | Action  |
| ---- | ------------------- | ---------------- | ------- |
| 1    | Yes                 | Yes              | Approve |
| 2    | Yes                 | No               | Approve |
| 3    | No                  | Yes              | Reject  |
| 4    | No                  | No               | Reject  |


## Use Cases
**Example:**  Online Shopping – Placing an Order

- **Use Case:** “Place an Order”
- **Actor:** Customer
- **Precondition:** Customer is logged in and has items in the cart.
- **Flow of Events:**
    - Customer views cart.
    - Customer clicks “Checkout.”
    - Customer enters shipping and payment details.
    - System validates payment.
    - System confirms order and sends confirmation email.
- **Postcondition:** Order is placed, and inventory is updated.

| Test Case ID | Scenario/Step            | Test Data           | Expected Result                       |
| ------------ | ------------------------ | ------------------- | ------------------------------------- |
| TC1          | View cart                | Items in cart       | Cart displays all items               |
| TC2          | Click Checkout           | -                   | Checkout page opens                   |
| TC3          | Enter shipping details   | Valid address       | System accepts details                |
| TC4          | Enter payment details    | Valid credit card   | Payment succeeds                      |
| TC5          | Payment validation fails | Expired credit card | Payment rejected, error message shown |
| TC6          | Confirm order            | -                   | Order confirmation email sent         |
