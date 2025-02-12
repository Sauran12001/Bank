import json
import os

# Data file paths
USER_DATA_FILE = "users.json"
EMPLOYEE_DATA_FILE = "employees.json"

# Ensure user data file exists
if not os.path.exists(USER_DATA_FILE):
    with open(USER_DATA_FILE, "w") as f:
        json.dump({}, f)

# Ensure employee data file exists with a default employee account (username: "1234", password: "1234")
if not os.path.exists(EMPLOYEE_DATA_FILE):
    default_employee = {
        "1234": {"password": "1234", "fees_collected": 0}
    }
    with open(EMPLOYEE_DATA_FILE, "w") as f:
        json.dump(default_employee, f, indent=4)

# ---------------------- User Management Functions ----------------------

def register_user():
    """
    Register a new user.
    The user is asked to input their first name, last name, phone number, username, and card password.
    """
    print("\n--- User Registration ---")
    first_name = input("First Name: ")
    last_name = input("Last Name: ")
    username = input("Username: ")
    phone_number = input("Phone Number: ")
    card_password = input("Card Password: ")

    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if username in users:
        print("❌ This username is already taken!")
        return

    users[username] = {
        "first_name": first_name,
        "last_name": last_name,
        "phone_number": phone_number,
        "card_password": card_password,
        "balance": 0.0,
        "saved_money": 0.0
    }

    with open(USER_DATA_FILE, "w") as f:
        json.dump(users, f, indent=4)

    print("Registration successful!")

def login_user():
    """
    User login using username and card password.
    """
    print("\n--- User Login ---")
    username = input("Username: ")
    card_password = input("Card Password: ")

    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if username in users and users[username]["card_password"] == card_password:
        print(f"Login successful! Welcome, {users[username]['first_name']}!")
        return username
    else:
        print("❌ Incorrect username or password!")
        return None

def deposit_money(username):
    """
    Deposit money into the user's main balance.
    """
    try:
        amount = float(input("Enter deposit amount: "))
        if amount <= 0:
            print("❌ Amount must be positive.")
            return
    except ValueError:
        print("❌ Invalid amount.")
        return
    
    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    users[username]["balance"] += amount

    with open(USER_DATA_FILE, "w") as f:
        json.dump(users, f, indent=4)

    print(f"${amount:.2f} has been deposited. New balance: ${users[username]['balance']:.2f}")

def spend_money(username):
    """
    Spend money from the user's main balance.
    """
    try:
        amount = float(input("Enter spending amount: "))
        if amount <= 0:
            print("❌ Amount must be positive.")
            return
    except ValueError:
        print("❌ Invalid amount.")
        return

    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if users[username]["balance"] >= amount:
        users[username]["balance"] -= amount

        with open(USER_DATA_FILE, "w") as f:
            json.dump(users, f, indent=4)

        print(f"${amount:.2f} has been spent. New balance: ${users[username]['balance']:.2f}")
    else:
        print("❌ Insufficient balance!")

def save_money(username):
    """
    Transfer money from the user's main balance to their savings.
    """
    try:
        amount = float(input("Enter amount to save: "))
        if amount <= 0:
            print("❌ Amount must be positive.")
            return
    except ValueError:
        print("❌ Invalid amount.")
        return

    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if users[username]["balance"] >= amount:
        users[username]["balance"] -= amount
        users[username]["saved_money"] += amount

        with open(USER_DATA_FILE, "w") as f:
            json.dump(users, f, indent=4)

        print(f"${amount:.2f} has been moved to savings.")
        print(f"New balance: ${users[username]['balance']:.2f}")
        print(f"Savings: ${users[username]['saved_money']:.2f}")
    else:
        print("❌ Insufficient balance!")

def check_balance(username):
    """
    Display the user's main balance and savings.
    """
    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    print("\n--- Account Details ---")
    print(f"Main Balance: ${users[username]['balance']:.2f}")
    print(f"Savings: ${users[username]['saved_money']:.2f}")

def withdraw_from_savings(username):
    """
    Withdraw money from the user's savings back to their main balance.
    """
    try:
        amount = float(input("Enter withdrawal amount from savings: "))
        if amount <= 0:
            print("❌ Amount must be positive.")
            return
    except ValueError:
        print("❌ Invalid amount.")
        return

    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if users[username]["saved_money"] >= amount:
        users[username]["saved_money"] -= amount
        users[username]["balance"] += amount

        with open(USER_DATA_FILE, "w") as f:
            json.dump(users, f, indent=4)

        print(f"${amount:.2f} has been withdrawn from savings.")
        print(f"New balance: ${users[username]['balance']:.2f}")
        print(f"Remaining Savings: ${users[username]['saved_money']:.2f}")
    else:
        print("❌ Insufficient savings!")

def user_menu(username):
    """
    Display the user menu with the following ordered options:
      1. Deposit Money
      2. Spend Money
      3. Save Money
      4. Check Balance
      5. Withdraw from Savings
      6. Logout
    """
    while True:
        print("\n--- User Menu ---")
        print("1. Deposit Money")
        print("2. Spend Money")
        print("3. Save Money")
        print("4. Check Balance")
        print("5. Withdraw from Savings")
        print("6. Logout")

        choice = input("Enter your choice: ")

        if choice == "1":
            deposit_money(username)
        elif choice == "2":
            spend_money(username)
        elif choice == "3":
            save_money(username)
        elif choice == "4":
            check_balance(username)
        elif choice == "5":
            withdraw_from_savings(username)
        elif choice == "6":
            print("Logging out...")
            break
        else:
            print("❌ Invalid choice. Please try again.")

# ---------------------- Employee Management Functions ----------------------

def login_employee():
    """
    Employee login using predefined credentials.
    Default employee account:
      Username: "1234"
      Password: "1234"
    """
    print("\n--- Employee Login ---")
    username = input("Employee Username: ")
    password = input("Password: ")

    with open(EMPLOYEE_DATA_FILE, "r") as f:
        employees = json.load(f)

    if username in employees and employees[username]["password"] == password:
        print(f"Employee login successful! Welcome, {username}!")
        return username
    else:
        print("❌ Incorrect employee username or password!")
        return None

def view_users():
    """
    Display a list of all registered users with details:
      - Username
      - First Name
      - Last Name
      - Phone Number
      - Main Balance
      - Savings
    """
    with open(USER_DATA_FILE, "r") as f:
        users = json.load(f)

    if not users:
        print("❌ No users registered.")
        return

    print("\n--- Registered Users ---")
    for username, details in users.items():
        print(f"Username: {username}")
        print(f"  First Name: {details['first_name']}")
        print(f"  Last Name: {details['last_name']}")
        print(f"  Phone Number: {details['phone_number']}")
        print(f"  Main Balance: ${details['balance']:.2f}")
        print(f"  Savings: ${details['saved_money']:.2f}\n")

def employee_menu(username):
    """
    Display the employee menu.
    """
    while True:
        print("\n--- Employee Menu ---")
        print("1. View Users")
        print("2. Logout")

        choice = input("Enter your choice: ")

        if choice == "1":
            view_users()
        elif choice == "2":
            print("Logging out of employee menu...")
            break
        else:
            print("❌ Invalid choice. Please try again.")

# ---------------------- Main System ----------------------

def main():
    while True:
        print("\n=== Banking System ===")
        print("1. User Login")
        print("2. Employee Login")
        print("3. Register New User")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            user = login_user()
            if user:
                user_menu(user)
        elif choice == "2":
            emp = login_employee()
            if emp:
                employee_menu(emp)
        elif choice == "3":
            register_user()
        elif choice == "4":
            print("Exiting the system. Goodbye!")
            break
        else:
            print("❌ Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
