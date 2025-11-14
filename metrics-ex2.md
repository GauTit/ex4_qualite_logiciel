# Exercise 2: Cyclomatic Complexity on a Key Method

## Selected Method: `withdrawMoney(double withdrawAmount)`

**Metrics:** CC = 5 | Class: BankAccount | Line: 128-137

### Decision Points Marked
```java
public boolean withdrawMoney(double withdrawAmount) {
    // DECISION POINT 1: withdrawAmount >= 0
    // DECISION POINT 2: AND balance >= withdrawAmount
    // DECISION POINT 3: AND withdrawAmount < withdrawLimit
    // DECISION POINT 4: AND withdrawAmount + amountWithdrawn <= withdrawLimit
    if (withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount < withdrawLimit
            && withdrawAmount + amountWithdrawn <= withdrawLimit) {
        balance = balance - withdrawAmount;
        success = true;
        amountWithdrawn += withdrawAmount;
    } else { // DECISION POINT 5
        success = false;
    }
    return success;
}
```

### Refactoring Proposal

Extract the complex validation logic into a helper method `canWithdraw(double amount)` that encapsulates all four validation checks. This reduces the main method's complexity from CC=5 to CC=2 and improves readability by giving meaningful names to each validation rule. The helper method would check: valid amount, sufficient balance, and withdrawal limits.

### Bonus: Refactored Code
```java
private boolean canWithdraw(double amount) {
    return amount >= 0 
        && balance >= amount 
        && amount < withdrawLimit 
        && (amount + amountWithdrawn) <= withdrawLimit;
}

public boolean withdrawMoney(double withdrawAmount) {
    if (canWithdraw(withdrawAmount)) {
        balance -= withdrawAmount;
        amountWithdrawn += withdrawAmount;
        return true;
    }
    return false;
}
```

**Result:** `withdrawMoney()` CC reduced from 5 to 2. Code is cleaner and more testable.