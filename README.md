# iOS-transaction-shortcut

## Premise
Guide on using the iOS shortcut automation feature to capture transactions

iOS 17.2 introduced the capability to attach automation events to a Transaction.

This can be used to supplement a budgeting application and keep a running transaction log, which can be useful for applications that don't directly support integration.

## Configure the iOS transaction automation
Open *Shortcuts* > Automation > *+* to add new
Scroll down to *Transaction* 
Select the card(s) that you want to monitor
Select *Run Immediately*
Select *Next*

Select **New Blank Automation**
Select **+ Add Action**
Search for the option to **Run Script Over SSH**

### Format the script
This requires a lot of messing around with the nuances of the iOS keyboard and interface. What you're looking to accomplish is like this screenshot:

You can choose to add or remove parameters as needed, but I would recommend to add as many as possible so that it's easier to uniquely identify a transaction.

The important thing here is to add single quotes surrounding each item. This will avoid a few issues:
1. We are using a bash script to parse the input, which accepts spaces as an argument separator. `'`s will join the arguments together so that `Whole Foods Market` will show up as one argument instead of 3: `Whole`, `Foods`, and `Market`.
2. The `Amount` variable is sent with a dollar sign, which is a variable identifier in bash. It needs to be captured and escaped for database interactions.
