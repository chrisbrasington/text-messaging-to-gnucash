# asterisk-sms-to-gnucash
Create transactions via text-messagging to a listening asterisk server and gnucash.

At minimum, 3 parameters are required:

    1 - the dollar amount
    2 - a description
    3 - the expense account name must be specified. 
The transaction will default as an expense with the withdrawal account will default to 'Liabilities:Credit Card' when not specified.

A positive dollar amount will be added into the Expense:{Name} account.

A negative dollar amount will be added into the Liabilities/Account.

Two more paramters exist to change the Account and switch Expense to Income

    4 - the account (liabilities, checking, savings, etc)
    5 - income

This allows you to expense or add income to another account. 

## Examples: 
### Defaulting as Credit Card Expense:
```"Books,The Martian,$9.00"```

Success:  ($9.00) "The Martian" Expenses:Books from Liabilities:Credit Card

### Changing Expense to come out of Checking:
```"Movies,The Martian,$16.00,Checking"```

Success:  ($16.00) "The Martian" Expenses:Movies from Account:Checking

### Changing to Income to add into Checking:
```"Salary,Making Bank,$1,000,000,Checking, Income"```

Success:  ($1,000,000) "Making Bank" Income:Salary into Account:Checking
