# Payment

Stores payment transaction information for a person.  A payment can be made using credit card, check, bank transfer, cash or purchase order.  All payments are grouped which means a registrant can pay for themselves and their guests with a single transaction.

## Properties

Field | Type | Description
------| ---- | -----------
Amount | decimal | Settled amount
AuthNum | string | Authorization code from the credit card issuer for an approved transaction
CCType | string | Type of credit card (i.e. Visa, Master Card, American Express, Discover)
CheckNumber | string | Check number if paid by check
DateChequeReceived | string | Date when the check was received
DateOnCheque | string | Date written on the check
DateTimeStamp | string | Time stamp of when the transaction was recorded
Last4 | string | Last 4 digits of a credit card
Message | string | Administrative notes
Name | string | Name on credit card
OrderID | string | Group payment id, the transaction's unique identifier
PaymentId | integer | Individual payment id
PaymentType | `PaymentType` | The type of payment (credit card, check, transfer, cash, purchase order etc ..)
PPIDCommittedBy | guid | PPID of the person who committed the transaction (can be the actual registrant or administrator)
PPIDFrom | guid | PPID of the person's account in which the payment was made from
PPIDTo | guid | PPID of the person's account to which the payment was made towards
Status | string | Payment status (Approved, Declined, Pending)