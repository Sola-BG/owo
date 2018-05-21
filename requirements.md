# PayNow

## Functional Requirements

User Management

- Already registered User can login by entering email and password.
- Already registered User can login using their Google or Facebook login
- Unregistered can register by clicking on the register link and they are presented with registration form, where they can enter their details. This is stored in the database.
- Unregistered can register with their social media (Google or Facebook) login.
- Users who cannot remember their login can click on a password recovery link and get an email sent to them with a link containing a token they can click on for password recovery.

Transactions

- A logged in user is able to see a list of transactions showing (Recipient&#39;s name, transaction date, amount, status) it should also have dropdown links to (View Details, Resend)
- Clicking View Details on a transaction should take user to the _View Details Screen_
- Clicking Resend on a transaction should go to the _Transaction Journey Screen_ with _Recipient Details_ and _Sender Details_ steps pre-populated and the  _Amount_  step active.

Recipients

- A logged in user is able to see a list of previous recipients (Recipient&#39;s name, last 4 digits of account number) and dropdown links (Send, Edit, Delete).
- Clicking on Send on a recipient should go to the _Transaction Journey Screen_ with _Recipient Details_ and _Sender Details_ steps pre-populated and the  _Amount_  step active.
- Clicking on  Edit on a recipient should go to the _Transaction Journey Screen_ with _Recipient Details_  step active.
- Clicking on  Delete on a recipient should go open up a popup modal asking user to confirm deletion. If confirmed recipient is deleted otherwise, the modal simply closes.
- The Recipients list should also have an _Add_  button. Clicking on which should take user to the _Transaction Journey Screen_ with _Recipient Details_  step active.

Transaction Journey Screen

- _Step one (Sender Details);_ allows user select Country of recipient, Currency and Delivery method)
- _Step two (Recipient Details)_;  allows user enter recipients details.
- _Step three (Amount);_ allows user enter amount being sent and payment details.
- _Step four;_  allows confirm transaction by clicking Send.
- _Step five_; confirmation page

User Details

Shows details of logged in user; name, email, phone, address, allows user to change password.

Database Design

The application will utilise MongoDB for the data layer. The collections required are as follows:-

User

| Field | DataType | Remarks |
| --- | --- | --- |
| UserID | ObjectId |   |
| CreatedDate | date |   |
| UpdatedDate | date |   |
| LoginFails | Int32 |   |
| Firstname | string |   |
| Lastname | string |   |
| Email | string |   |
| Telephone | string |   |
| password | string |   |
| facebook\_id | string |   |
| google\_id | string |   |
| Date\_of\_birth | date |   |
| Addresses | Array | This hold an array of ObjectIds which will link it to the Address collection |
| Recipients | Array | This hold an array of Recipient which will link it to the Address collection |
| Transactions | Array | This hold an array of ObjectIds which will link it to the Transaction collection |
| Settings | Array | This hold an array of ObjectIds which will link it to the Setting collection |
| Authentication\_method | string | This will have 1 of 3 possible values (local, facebook, google) |
| UserTypeID | ObjectId |   |

UserType

| **Field** | **DataType** | **Remarks** |
| --- | --- | --- |
| UserTypeID | ObjectId |   |
| Description | string | (e.g. customer, admin, back-office-staff) |
|   |   |   |

Address

| Field | DataType | Remarks |
| --- | --- | --- |
| AddressID | ObjectId |   |
| AddressLine1 | string |   |
| AddressLine2 | string |   |
| City | string |   |
| County | string |   |
| PostCode | string |   |
| Country | string |   |
| AddressTypeID | ObjectId |   |

AddressType

| **Field** | **DataType** | **Remarks** |
| --- | --- | --- |
| AddressTypeID | ObjectId |   |
| Description | string |   |



Transaction

| **Field** | **DataType** | **Remarks** |
| --- | --- | --- |
| TransactionID | ObjectId |   |
| TransactionDateTime | DateTime |   |
| RecipientID | ObjectId |   |
| Amount | ObjectId |   |
| SenderCountry | string |   |
| SenderCurrency | string |   |
| RecipientCurrency | string |   |
| RecipientCountry | string |   |
| Exchange rate | string |   |
| Payment\_Method | string | This will have one of  3 values (bank-transfer, cash-collection, swift) |
| TransactionStatus | string |   |
| BankDetailsID | ObjectId |   |
| SwiftDetailsID | ObjectId |   |
| CashCollectionDetailsID | ObjectId |   |



Recipient

| Field | DataType | Remarks |
| --- | --- | --- |
| RecipientID | ObjectId |   |
| Firstname | string |   |
| Lastname | string |   |
| UserID | ObjectId |   |



BankDetails

| **Field** | **DataType** | **Remarks** |
| --- | --- | --- |
| BankDetailsID | ObjectId |   |
| BankName | string |   |
| AccountName | string |   |
| AccountNumber | string |   |
| SortCode | string |   |



SwiftDetails

| Field | DataType | Remarks |
| --- | --- | --- |
| SwiftDetailsID | string |   |
| AccountNumber | string |   |
| SwiftBIC | string |   |
| Reference | string |   |
| AddressID | ObjectId |   |



CashCollectionDetails

| Field | DataType | Remarks |
| --- | --- | --- |
| CashCollectionDetailsID | ObjectId |   |
| AddressID | ObjectId |   |
| IndentificationID | string |   |
| IdentificationType | string |   |
| Passcode | string |   |
