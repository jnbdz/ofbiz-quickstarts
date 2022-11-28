# Accounting | Applications | EN | OFBiz
It is the core application component and has most of the modern features you would expect in a general purpose double-entry accounting system.

Like many of the applications that come with OFBiz it seamlessly integrates with other OFBiz applications such as [Inventory](../inventory/README.md), [Purchasing](../purchasing/README.md) and [Manufacturing](../manufacturing/README.md). All this makes OFBiz a more valuable accounting system.

## About
It is org.: 
- [double-entry](https://en.wikipedia.org/wiki/Double-entry_bookkeeping) - 
- General Ledger with hierarchical accounts
- journals
- posting of transactions
- corresponding entries
- structure based on [OMG GL](https://www.omg.org/) standard - 
- Correlates well with: 
    - [AR/AP](https://www.zoho.com/books/articles/accounts-receivable-accounts-payable-guide.html) extension of the **OMG GL** standard
    - [ebXML](http://www.ebxml.org/) - 
    - [OAGIS](https://oagi.org/) - 
### Support
- Multiple orgs. can be managed (because of the way entities are structured)
    - Companies
    - Departments
    - Org. inside the company
- Orgs. can have various GL Accounts associated with it (op. with its own subset of the Master Chart of Accounts).
- Orgs. can have its own **Journals** for flexibility
- **Journals** should be as minimal as possible in favour of allowing the system to auto create and post transactions based on **business events** triggered by *standard procedures* and *documents*
- Documents types: 
    - purchase
    - sales orders
    - invoices
    - inventory transfer
    - payments
    - receipts
    - and so on
- Accounting Features
    - General Ledger
    - Accounts Receivable
    - Accounts Payable
    - Agreements
    - Multi-currency Support
    - Billing Accounts
    - Fixed Asset Accounting 


