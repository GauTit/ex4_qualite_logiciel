# Analyse SonarQube - Résumé

## Issues Identifiées

### Issue 1: Try-with-resources
- **Fichier:** Bank.java:144
- **Problème:** Fermeture manuelle des ressources (FileOutputStream, OutputStreamWriter)
- **Risque:** Ressources non fermées en cas d'exception
- **Sévérité:** Major

### Issue 2: Strings dupliquées
- **Fichier:** BankAccountApp.java:95, 159
- **Problème:** Littéraux "DEPOSIT", "WITHDRAW", "BALANCE" répétés 3+ fois
- **Risque:** Maintenance difficile, incohérences
- **Sévérité:** Major

### Issue 3: Champs statiques modifiés
- **Fichier:** PersonTest.java:24
- **Problème:** Méthode non-static modifie variables static
- **Risque:** Problèmes de concurrence dans les tests
- **Sévérité:** Major

## Corrections Appliquées

### Fix 1: Try-with-resources
- Avant: ~25 lignes (try-catch-finally manuel)
- Après: ~10 lignes (fermeture automatique)

### Fix 2: Constantes (partiel)
- Création: `OPERATION_DEPOSIT`
- Remplacements: 2 occurrences
- Reste à faire: WITHDRAW, BALANCE, QUIT, etc.

### Fix 3: Suppression 'static'
- Champs de test maintenant isolés par instance
- Élimination des risques de tests parallèles

## Corrélation Complexité/Issues

**Haute complexité = Plus d'issues:**
- Bank & BankAccountApp: WMC/CBO élevés → nombreux problèmes
- Person & PersonTest: WMC faible → moins de problèmes

**Conclusion:** La complexité élevée corrèle avec plus de problèmes de qualité