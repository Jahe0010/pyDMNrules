# pyDMNrules
An implementation DMN (Decision Model Notation) in Python, using the pySFeel and openxlrd modules.

DMN rules are read from an Excel workbook.
Then data, matching the input variables in the DMN rules is passed to the decide() function.
The returned data contains the decion.


The passed Excel workbook must contain the two tabs 'Glossary' and 'Decision'.
Other tabs contain as many DMN rules tables as necessary.

The 'Glossary' tab must contain a table headed 'Glossary'.
This table must contain three columns with the headings 'Variable', 'Business Concept' and 'Attribute'.
The data in these three columns describe the inputs and outputs associated with the 'Decision'.
'Variable' can be any text and is used to pass data to and from pyDMNrules.
'Business Concept' and 'Attribute' must be valid S-FEEL names, but may **not** contain the dot, or period character.

| Glossary |                  |           |
|----------|------------------|-----------|
| Variable | Business Concept | Sector    |
| Customer | Customer         | sector    |
| OderSize | Order            | orderSize |
| Delivery |                  | delivery  |
| Discount | Discount         | discount  |

The 'Decision' tab must contain a table headed 'Decision' with the headings 'Decisions' and 'Execute Decision Table'.
The row contain a description and the name of a DMN rules table. pyDMNrules will execute each decision table in this order.

| Decision           |                        |
|--------------------|------------------------|
| Decisions          | Execute Decision Table |
| Determine Discount | Discount               |
| Discount           | Discount               |

USAGE:

    import pySFeel
    dmnRules = pyDMNrules()
    data = {}
    data['Customer'] = 'Business'
    data['OrderSize'] = 9
    data['Delivery'] = 'sameday'
    (status, newData) = dmnRules.decide(data)

newData will contain all the items listed in the Glossary, with their final assigned value. Items in the Glossary can be outputs of one decision table and inputs in the next decision table, which makes it easy to support complex business models.
