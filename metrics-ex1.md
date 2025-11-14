# Exercise 1: Discover the Code & Rough Size

## Metrics Summary

| Class | LOC (approx.) | NOM | Short description of responsibility |
|-------|---------------|-----|-------------------------------------|
| Bank | 395 | 14 | Manages collection of bank accounts, provides CRUD operations and statistics (average, min, max balance). Handles persistence. |
| BankAccount | 462 | 20 | Represents individual bank account. Manages balance, deposits, withdrawals, limits. Handles serialization. |
| Person | 325 | 23 | Represents account holder with personal attributes (name, gender, age, physical characteristics, email). Provides validation and serialization. |
| BankAccountApp | 492 | 2 | Main application with console UI. Single large main() method handles all user interactions and menu navigation. |

## Size vs Responsibility Analysis

**Bank:** ✅ Size matches responsibility. 395 LOC and 14 methods are appropriate for managing multiple accounts and operations.

**BankAccount:** ⚠️ Slightly oversized (462 LOC, 20 methods). Handles both business logic AND persistence, suggesting potential separation needed.

**Person:** ⚠️ Too many methods (23) for a data class. Over-engineered with complex validation logic that could be simplified.

**BankAccountApp:** ❌ **Critical problem.** 492 LOC in single main() method with cyclomatic complexity of 40. Severe violation of Single Responsibility Principle. Needs urgent refactoring.

## Conclusion

Most classes have reasonable sizes except **BankAccountApp**, which is a "God Method" anti-pattern requiring immediate refactoring into separate methods/classes.