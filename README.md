class Expense:
    def __init__(self, amount, category, description, date):
        self.amount = amount
        self.category = category
        self.description = description
        self.date = date

class ExpenseTracker:
    def __init__(self):
        self.expenses = []

    def add_expense(self, expense):
        self.expenses.append(expense)

    def get_total_expenses(self):
        total = sum(expense.amount for expense in self.expenses)
        return total

    def get_monthly_summary(self, month, year):
        monthly_expenses = [expense for expense in self.expenses if expense.date.month == month and expense.date.year == year]
        total_monthly_expenses = sum(expense.amount for expense in monthly_expenses)
        return total_monthly_expenses

    def get_category_summary(self):
        category_summary = {}
        for expense in self.expenses:
            category = expense.category
            if category in category_summary:
                category_summary[category] += expense.amount
            else:
                category_summary[category] = expense.amount
        return category_summary

    def save_expenses_to_file(self, filename):
        with open(filename, 'w') as file:
            for expense in self.expenses:
                file.write(f"{expense.amount},{expense.category},{expense.description},{expense.date}\n")

    def load_expenses_from_file(self, filename):
        self.expenses = []
        with open(filename, 'r') as file:
            for line in file:
                amount, category, description, date = line.strip().split(',')
                self.add_expense(Expense(float(amount), category, description, date))
