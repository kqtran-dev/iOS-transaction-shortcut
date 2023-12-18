# iOS-transaction-shortcut

## Premise
Guide on using the iOS shortcut automation feature to capture transactions

iOS 17.2 introduced the capability to attach automation events to a Transaction. Relevant info about a Transaction can be captured, including:
1. Transaction
2. Card or Pass (e.g. `Apple Card`)
3. Merchant (e.g. `Whole Foods Market`)
5. Amount (e.g. `$32.04`)
6. Name

You can also include identifying metadata such as:
1. Current Date
2. Device Details
Device Detail
OS
Device Type
Device hostname
Name

When used in concert, this information can be captured and used to generate a running transaction log. This information can supplement a budgeting application with "manual" entry for applications that may not support a direct integration, such as the Apple Card.

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
