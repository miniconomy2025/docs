# Miniconomy Docs

This repository serves as a central location for all teams to manage their:
- high-level assumptions + design (`spec/<group-name>.md`)
- individual roles + responsibilities (`spec/<group-name>.md`)
- API documentation (`apis/<group-name>/api.{md,yaml}`)

By managing things in one central location it should be easier to resolve inconsistencies and to ensure that all groups are working by the same assumptions.

> **NOTE**: The `master` branch should only contain **definitive** and **finalized** specifications, which other groups can confidently assume to be true, and base their respective implementations off of.
> Groups should make their own `<group-name>` branches (E.g. `commercial-bank`) to incrementally work on in-progress specifications, and should only things into `master` once they are certain & consistent with the assumptions of other groups.


---

# Spec
Groups will be simulating the cellphone supply chain and economy
These are the groups:

- Suppliers (3)
    - Electronics Supplier - take copper and silicon and make into electronics
    - Screen Supplier - take copper and sand and make into screens
    - Case supplier - take plastic or aluminum and make into cases

- Logistics (2)
    - Bulk Logistics - transfer goods from suppliers to phone companies
    - Consumer Logistics - transfer goods from phone companies to consumers

- Phone Companies (2)
    - Pear - builds the Pear ePhone series - 3 models
    - SumSang - builds the Cosmos Z25 series  - 3 models

- Bank (commercial)
    - Loans to companies
    - Payments between companies

- Bank (retail)
    - Loans to peeps
    - Payments from peeps to companies (so the retail bank has to pay money over to the commercial bank)

- Hand of Hḗphaistos (THoH)
    - Manages randomness (price and availability of raw materials)
    - 'Sells' raw materials and distributes that money to people
    - Manages when the simulation starts etc.
    - Manages people, their salaries and the like
    - Sells manufacturing equipment and delivery vehicles to companies
    - Basically the start and end of the cycle, basically keeps the entire value chain flowing
        - Sell the raw materials so the suppliers can manufacture
        - … all the other stuff happens
        - Decides when people 'buy' the phones.

- Recycler
    - Receives phones from consumers and recycles them into raw materials (copper, silicone, sand, plastic and aluminium) to re-sell to suppliers.``