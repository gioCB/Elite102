# Elite102
mport mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="root",
  password="@GankeMiles12"
)

print(mydb)

mycursor = mydb.cursor()

mycursor.execute("SHOW DATABASES")

for x in mycursor:
  print(x)
# Define a list to store account information
accounts = {'123456': {'name': 'Gio', 'pin': '22222', 'balance': 0}}

# Define functions for banking operations
def check_balance(account):
    balance = accounts[account]['balance']
    print(f'Your balance is ${balance:.2f}')

def deposit(account, amount):
    accounts[account]['balance'] += amount
    print(f'Deposited ${amount:.2f} into your account')

def withdraw(account, amount):
    if accounts[account]['balance'] < amount:
        print('Insufficient funds')
    else:
        accounts[account]['balance'] -= amount
        print(f'Withdrawn ${amount:.2f} from your account')

def create_account():
    account = input('Enter a new account number: ')
    name = input('Enter your name: ')
    pin = input('Enter a PIN: ')
    accounts[account] = {'name': name, 'pin': pin, 'balance': 0}
    print(f'Account {account} created')

def close_account(account):
    del accounts[account]
    print(f'Account {account} closed')

def modify_account(account):
    print('What would you like to modify?')
    print('1. Name')
    print('2. PIN')
    choice = input('Enter your choice: ')
    if choice == '1':
        name = input('Enter your new name: ')
        accounts[account]['name'] = name
        print('Name updated')
    elif choice == '2':
        pin = input('Enter your new PIN: ')
        accounts[account]['pin'] = pin
        print('PIN updated')
    else:
        print('Invalid choice')

# Define a function to authenticate users
def authenticate():
    account = input('Enter your account number: ')
    pin = input('Enter your PIN: ')
    if account in accounts and pin == accounts[account]['pin']:
        print(f'Welcome, {accounts[account]["name"]}')
        return account
    else:
        print('Invalid account number or PIN')
        return None

# Main program loop
while True:
    print('What would you like to do?')
    print('1. Check balance')
    print('2. Deposit')
    print('3. Withdraw')
    print('4. Create account')
    print('5. Close account')
    print('6. Modify account')
    print('7. Quit')
    choice = input('Enter your choice: ')

    if choice == '1':
        account = authenticate()
        if account:
            check_balance(account)

    elif choice == '2':
        account = authenticate()
        if account:
            amount = float(input('Enter the amount to deposit: '))
            deposit(account, amount)

    elif choice == '3':
        account = authenticate()
        if account:
            amount = float(input('Enter the amount to withdraw: '))
            withdraw(account, amount)

    elif choice == '4':
        create_account()

    elif choice == '5':
        account = authenticate()
        if account:
            close_account(account)

    elif choice == '6':
        account = authenticate()
        if account:
            modify_account(account)

    elif choice == '7':
        print('Goodbye, Thanks for banking with us!')
        break

    else:
        print('Invalid choice')
