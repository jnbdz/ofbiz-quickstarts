# Global General Ledger Settings
- Master template to help with setup a: 
    - Chart of accounts
    - Default transactions
    - Other settings that can be applied across many OFBiz modules
- Global settings are needed because OFBiz is an integrated system so certain areas like accounting are linked to many other modules

Global GL Settings: 
- **Chart of Accounts** - a comprehensive master template for a complete chart of accounts.
    - All general ledger accounts must exist in the global template before they can be assigned to be used at the organisation level (e.g. Company)
- **Custom Time Periods** - a master list to display or setup financial periods (key in accounting)
   - Company Financial Year
   - Fiscal / Tax Periods (weeks, months, quarters)
   - VAT / GST Periods
   - Sales Periods
- **Costs** - a master list of any cost calculations to be used for assets or tasks.
    - Track all the costs
    - Make sure you are not losing money
    - Costs examples to track: 
        - Raw Materials Costs
        - Labour Costs
        - Rental Costs
        - Electricity Costs
        - Quality Assurance or Regulatory Costs
    - Direct and Indirect Costs:
        - Direct: 
            - Easily identifiable
            - Related to what you do to produce
            - Sell to customers
        - Indirect: 
            - Not easily linked to what you are selling to customers
            - Included: rent, electricity, general administration costs
    - Fixed and variable Costs
        - Variable costs: Example: the number of products you sell or produce
        - Fixed: Example: How many products you sell or not will not change that cost
    - 
- **Payment Method Type** - a master list of the ways payments can be made (e.g. cash, credit card, etc) and the default accounts to be used for each
- **Invoice Item Type** - a master list of all the transaction line types that can occur on any invoice and the default account to be used for each
- **Rates** - a list of rates (e.g. pay rates, overtime rates etc) that can be used for billing work,tasks or as part of salary calculations
- **Foreign Exchange Rates** - a master list of exchange rates to be used and dates they are valid
- **GL Account Category** - currently this is set to be a list of cost centres
- **Cost Centers** - a way to specify how to process percentage allocations between cost centres for specific accounts


