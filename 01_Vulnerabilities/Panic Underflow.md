**Definition:** In Solidity versions **0.8.0 and above**, the compiler includes built-in checks for arithmetic operations. A **Panic: Underflow** occurs when a subtraction results in a value less than zero for an unsigned integer type (like `uint256`).

**Technical Behavior:**

- **Revert:** The EVM (Ethereum Virtual Machine) automatically reverts the entire transaction.
- **State:** No state changes are saved, and the gas used up to that point is consumed.
- **Panic Code:** The specific error code for arithmetic overflows/underflows is `0x11`.

**Example:**

```
uint256 balance = 80;
uint256 debt = 100;
uint256 result = balance - debt; // ❌ This will trigger a Panic Underflow
```