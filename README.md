# Expense-Tracker-CLI
Uses argparse library handling users command .Adding arguments and working with queries.

import argparse

expenses = []

def add_expense(amount, category):
    expenses.append({"amount": amount, "category": category})
    print(f"Added: ₹{amount} ({category})")

def show_expenses():
    if not expenses:
        print("No expenses found.")
        return

    total = 0
    for exp in expenses:
        print(f"₹{exp['amount']} - {exp['category']}")
        total += exp['amount']

    print(f"\nTotal Expense: ₹{total}")

parser = argparse.ArgumentParser(
    description="Simple Expense Tracker CLI"
)

parser.add_argument(
    "--action",
    choices=["add", "show"],
    required=True,
    help="Action to perform"
)

parser.add_argument(
    "--amount",
    type=float,
    help="Expense amount"
)

parser.add_argument(
    "--category",
    type=str,
    help="Expense category"
)

args = parser.parse_args()

if args.action == "add":
    if args.amount is None or args.category is None:
        print("Error: --amount and --category required")
    else:
        add_expense(args.amount, args.category)

elif args.action == "show":
    show_expenses()
