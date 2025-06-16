```mermaid
erDiagram
CATEGORY {
int CATEGORY_ID PK
varchar CNAME
}
CUSTOMER {
int CUST_ID PK
varchar FIRST_NAME
varchar LAST_NAME
varchar PHONE_NUMBER
}
EMPLOYEE {
int EMPLOYEE_ID PK
varchar FIRST_NAME
varchar LAST_NAME
varchar GENDER
varchar EMAIL
varchar PHONE_NUMBER
int JOB_ID FK
varchar HIRED_DATE
int LOCATION_ID FK
}
JOB {
int JOB_ID PK
varchar JOB_TITLE
}
LOCATION {
int LOCATION_ID PK
varchar PROVINCE
varchar CITY
}
PRODUCT {
int PRODUCT_ID PK
varchar PRODUCT_CODE
varchar NAME
varchar DESCRIPTION
int QTY_STOCK
int ON_HAND
int PRICE
int CATEGORY_ID FK
int SUPPLIER_ID FK
varchar DATE_STOCK_IN
}
SUPPLIER {
int SUPPLIER_ID PK
varchar COMPANY_NAME
int LOCATION_ID FK
varchar PHONE_NUMBER
}
TRANSACTION {
int TRANS_ID PK
int CUST_ID FK
varchar NUMOFITEMS
varchar SUBTOTAL
varchar LESSVAT
varchar NETVAT
varchar ADDVAT
varchar GRANDTOTAL
varchar CASH
varchar DATE
varchar TRANS_D_ID "Note: Type mismatch with TRANSACTION_DETAILS.TRANS_D_ID"
}
TRANSACTION_DETAILS {
int ID PK
varchar TRANS_D_ID FK "Links to TRANSACTION.TRANS_ID (Type inconsistency: varchar vs int)"
varchar PRODUCTS
varchar QTY
varchar PRICE
varchar EMPLOYEE "Could be FK to EMPLOYEE_ID if stores ID, currently varchar"
varchar ROLE
}
TYPE {
int TYPE_ID PK
varchar TYPE
}
USERS {
int ID PK
int EMPLOYEE_ID FK
varchar USERNAME
varchar PASSWORD
int TYPE_ID FK
}

EMPLOYEE ||--o{ JOB : "has a"
EMPLOYEE ||--o{ LOCATION : "works in"
PRODUCT ||--o{ CATEGORY : "belongs to"
PRODUCT ||--o{ SUPPLIER : "supplied by"
SUPPLIER ||--o{ LOCATION : "located in"
TRANSACTION ||--o{ CUSTOMER : "made by"
TRANSACTION ||--o{ TRANSACTION_DETAILS : "has"
USERS ||--|| EMPLOYEE : "associated with"
USERS ||--o{ TYPE : "has a"
