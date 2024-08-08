# Develop a console-based budget tracker that allows users to manage their expenses and income.
import json
import os
from datetime import datetime

# File name for storing transactions
DATA_FILE = 'budget_tracker.json'

# Load transactions from file
def load_transactions():
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, 'r') as file:
            return json.load(file)
    return {'incomes': [], 'expenses': [], 'pending': []}

# Save transactions to file
def save_transactions(transactions):
    with open(DATA_FILE, 'w') as file:
        json.dump(transactions, file, indent=4)

# Record a new transaction (income or expense)
def record_transaction(transactions):
    transaction_type = input("Enter transaction type (income/expense): ").lower()
    if transaction_type not in ['income', 'expense']:
        print("Invalid transaction type.")
        return
    
    category = input("Enter transaction category: ")
    amount = input("Enter transaction amount: ")
    
    # Check if amount is valid
    try:
        amount = float(amount)
    except ValueError:
        print("Invalid amount. Please enter a valid number.")
        return
    
    timestamp = datetime.now().isoformat()
    
    transaction = {
        'category': category,
        'amount': amount,
        'timestamp': timestamp
    }
    
    transactions[transaction_type + 's'].append(transaction)
    save_transactions(transactions)
    print("Transaction recorded successfully.")

# Calculate remaining budget
def calculate_budget(transactions):
    total_income = sum(transaction['amount'] for transaction in transactions['incomes'])
    total_expense = sum(transaction['amount'] for transaction in transactions['expenses'])
    remaining_budget = total_income - total_expense
    print(f"Total Income: {total_income:.2f}")
    print(f"Total Expense: {total_expense:.2f}")
    print(f"Remaining Budget: {remaining_budget:.2f}")

# Analyze expenses by category
def analyze_expenses(transactions):
    expenses_by_category = {}
    for expense in transactions['expenses']:
        category = expense['category']
        amount = expense['amount']
        if category in expenses_by_category:
            expenses_by_category[category] += amount
        else:
            expenses_by_category[category] = amount
    
    print("Expense Analysis:")
    for category, amount in expenses_by_category.items():
        print(f"{category}: {amount:.2f}")

# Main function to run the budget tracker
def main():
    transactions = load_transactions()
    
    while True:
        print("\nBudget Tracker")
        print("1. Record Transaction")
        print("2. Calculate Budget")
        print("3. Analyze Expenses")
        print("4. Exit")
        
        choice = input("Enter your choice: ")
        
        if choice == '1':
            record_transaction(transactions)
        elif choice == '2':
            calculate_budget(transactions)
        elif choice == '3':
            analyze_expenses(transactions)
        elif choice == '4':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == '__main__':
    main()
