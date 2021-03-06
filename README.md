# text-messaging-to-gnucash
##### Create transactions via short text-messagging to a gnucash sqlite3 database file.

## Parameters: 

At minimum, 3 parameters are required (in this order):

    1 - the dollar amount
    2 - a description
    3 - the expense account name must be specified. 
    
The transaction will default as an expense. The withdrawal account will default to 'Liabilities:Credit Card' when not specified.

A positive dollar amount will be added into the Expense:{Name} account.
A negative dollar amount will be added into the Liabilities/Account.

Two more paramters exist to change the Account and switch Expense to Income

    4 - the account (liabilities, checking, savings, etc)
    5 - income

This allows you to expense or add income to another account. 

## Examples: 

Note: The command 'transaction' (transaction.bat) is synonymous with 'python2 parser.py'

### Defaulting as Credit Card Expense:
```transaction '$9.00,The Martian,Books'```

Success:  ($9.00) "The Martian" Expenses:Books from Liabilities:Credit Card

### Changing Expense to come out of Checking and nested Expense Account:
```transaction '$16.00,The Martian,Entertainment:Movie,Checking'```

Success:  ($16.00) "The Martian" Expenses:Entertainment:Movies from Account:Checking

### Changing to Income to add into Checking:
```transaction '1000000,Making Bank,Salary,Checking,Income'```

Success:  ($1,000,000) "Making Bank" Income:Salary into Assets:Current Assets:Checking Account

### Add Expense to new Expense Account:
```transaction '5.00,Climbing Gym Day Pass,Sports'```

Success:  ($5.00) "Climbing Gym Day Pass:, Expenses:Sports from Liabilities:Credit Card

Note: The account Expenses:Sports did not exist and was automatically created.

## Shorthand:

    CC as 'Liabilities:Credit Card'
    Checking as 'Assets:Current Assets:Checking Account'
    Savings as 'Assets:Current Assets:Savings Account'

## Notes on Missing/Imbalance Account:

When an expense comes in referenece a non-existant expense account, that expense account will be automatically created.
All other missing accounts will redirect to Imbalance.
I decided to only automatically create expense accounts, this seemed safe. Should the "from" account (like CC or checking) not exist, it will redirect to Imbalance.
If income comes in and either the TO (where to deposit) or FROM (what type of income was this, like Salary) accounts do not exist, both can redirect to Imbalance.

Imbalance allows the user to recognize an error in gnucash and correct transactions. Imbalance will highlight RED.

Unless there is a problem connecting to the file, this should allow all transactions to process into the database.

## settings.yaml sample

    location: './'
    gnucash: sample.gnucash
    log: sms-transaction.log
