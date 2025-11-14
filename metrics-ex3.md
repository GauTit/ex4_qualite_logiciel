# Exercise 3: CK Metrics Across Classes - Code Smells Analysis

## Metrics Table

| Class | LOC | WMC | CBO | LCOM | Quick notes |
|-------|-----|-----|-----|------|-------------|
| Bank | 395 | 14 | 3 | 0 | Account manager. Moderate complexity. |
| BankAccount | 462 | 20 | 2 | 44 | Most methods. Mixes business + persistence logic. |
| Person | 325 | 23 | 0 | 79 | Data class with too many methods. High LCOM = low cohesion. |
| BankAccountApp | 492 | 2 | 3 | 1 | Giant 492-line main() method (CC=40). God Method anti-pattern. |

## Analysis

**Highest WMC:** Person (23 methods) - too many getters/setters for a simple data class.

**Highest CBO:** Bank and BankAccountApp (both 3) - expected for orchestrator classes.

**Most worrisome:** **BankAccountApp**. Despite WMC=2, it has a single 492-line main() method with cyclomatic complexity of 40. This is a severe "God Method" anti-pattern that violates Single Responsibility Principle. Untestable and unmaintainable. Needs urgent refactoring.

**Secondary concerns:** Person (LCOM=79) suggests over-engineering; BankAccount (LCOM=44) mixes responsibilities.