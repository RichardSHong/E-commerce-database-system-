INFO 605 - GUFS DBMS

**INFO 605: Fall 2020**

**Online Clothing Store**

Members: _Mariachiara Acconcia, Brian Kong, Janam Patel, and Richard Hong_

1. **Summary**

The purpose of this project is to provide a relational database solution to keep track of e-commerce entities. The database is intended for Give Us Five Stars (GUFS), an online clothing store. This document outlines the process that was taken to create the database system. This includes the goals, scope, requirements, ERD, relational schema, and the SQL implementation. In this project we tried to create a simplified database for a real world E-commerce system. The main aspects that are usually visible to E-commerce system users were included in our scope, while we left out all the system&#39;s internal aspects and calculations.

2. **PROJECT STATEMENT**
  - Overall Goals of the System
 This project is an E-commerce database system for a new E-commerce clothing website named Give Us Five Stars (GUFS) that will store information about products, such as apparel, footwear, sportswear, etc. and customers, and orders. This system aims to create a single database that combines all of the data for a new E-commerce clothing website, GUFS. Unified data in the E-commerce website enables a single application that supports all aspects of the company&#39;s needs or multiple applications without redundant data. For this project, the authors have decided to use a fictional organization, Give Us Five Stars (GUFS), that reflects the actual data needs and challenges of many E-commerce systems.

  - Context and Importance of the System
 Currently, GUFS stores data in separate databases. This makes it difficult to track data between accounts, orders, and items. GUFS must secure transaction reliability when customers make their purchases. The number of items in the warehouse should be updated in real-time. Also, when customers search for products they want, GUFS must provide search results quickly. An integrated database would provide transaction reliability, real-time update, and better-searching performance. Users would be able to track their order history, saved for later items, billing, and shipping information, and possible discounts applied to items they order.

  - Scope of the Project
    - IN-Scope
 This database will store data for all customers, all transactions made by customers, and all products. The product may be any cloth type, such as apparel, footwear, sportswear, formal wear, accessories, etc. This database&#39;s scope will also include data about the estimated delivery date, shipping information, payment options, products&#39; reviews, and save for later/favorite list. This E-commerce database system will also track records of customers and products such as cancelation rate, and return rate.

    - Out-Scope
 The database does not store employees&#39; information and information of warehouses that may affect delivery costs. Nor will it track the entire GUFS budget, including payroll and benefits, operating costs, building costs, and maintenance costs.
3. **REQUIREMENTS SPECIFICATION**

- Analysis of Current system

Currently, GUFS stores data in separate databases. This makes it difficult to track data between accounts, orders, and items. GUFS must secure transaction reliability when customers make their purchases. The number of items in the warehouse should be updated in real-time. Also, when customers search for products they want, GUFS must provide search results quickly. An integrated database would provide transaction reliability, real-time update, and better-searching performance. Users would be able to track their order history, saved for later items, billing, and shipping information, and possible discounts applied to items they order.

- Data Requirements
  - GUFS needs to track information for each new user, including name, phone number, email address. GUFS also generates a unique registration number for each new user.
  - Each user is tied to an account that contains a unique account ID, a unique user logonID and password, and creation date.
  - Each account can be either personal or a business account.
  - Each account can write reviews about any product. Each review has its own ID, date, number of stars, comment, useful flag, and number of total words.
  - GUFS records information about orders. Each order has an order ID, an order date, an order status, a shipping address, a receiver name, a delivery date, a dispatch date and a billing address.
  - Each order can contain one or many items, and about every item the system keeps track of the item ID, sku, item name, category, price, description, stock, review stars, size,color.
  - Each order has an order status that changes overtime and is recorded with a timestamp.
  - Every order also contains order items, for which the system keeps track of the order item ID, discounted price, and quantity.
  - One account can have many Save For Later items.
  - Each order can have multiple transactions, either payment or return, since customers may add items, change the number of items, or even return items after purchase if they so desire.
  - For each payment and for each return GUFS keeps track of the unique ID, total amount and date.
  - GUFS also keeps information about return line items and the quantity of items returned.
  - Each user can pay the total amount with credit cards. GUFS records card number, PIN, account&#39;s holder name and billing address for credit cards.

- Business Rules and Logic
  - Each account can make multiple orders, each containing many items.
  - Each account can add many items to the &quot;Save for later&quot; list.
  - Each payment can only belong to one account, while each account can make many payments.
  - Each return only belongs to one order, while each order can have zero or many returns.
  - Every order can have a payment or a return.
  - Each account can also write many reviews about items, and each item can have more than one review.
  - Each customer may or may not place orders at any one time.
  - Each return contains many return line items, and each return line item belongs to one and only one order line item.
  - Each order has an order status, which is constantly updated and recorded with a timestamp.
  - Each order can contain many order items, and each order item has exactly one item, while every item can be found in different order items.

**Solution**

To solve the problem, a relational database is being implemented. Utilizing a relational database, GUFS will be able to better keep track of its data. This will provide the ability for the business to track important metrics such as the order and return rate for various items. The schema is designed to handle the business rules and logic outlined in the section above. This solution consolidates the data from multiple sources and allows for easy querying.

**Data**

All data used in this implementation is dummy data created by each of our team members. The data is intended to simulate real world entries into the system. After the production deployment of our database, live data will be inserted from multiple sources. Daily business operations will produce data to be inserted into the database.

**Hardware and Software**

Lucidchart was used to develop the ERD. Oracle database was used to implement the database.

-

4. **Conceptual Design**
  - ![ERD_GUFS](https://github.com/RichardSHong/E-commerce-database-system-/blob/main/images/ERD_GUFS.jpeg?raw=true)


- Documentation of the ERD
  - Address is not stored for User because it is stored as a billing address and shipping address in the Order and Transaction tables.
  - User and Account can be merged into one entity since they have 1..1 relationship
  - Each account can make zero or multiple payments but each payment belongs to one and only one account.
  - Each account can make zero or multiple orders but each order belongs to one and only one account.
  - Each account can have zero or many Save\_for\_Later items, and each Save\_for\_Later item can belong to one and only one account.
  - Each Save\_For\_Later item refers to only one item specifically.
  - Each account can write as many reviews as they desire and each review is about one specific item and is written by one account only .
  - Each account can be either a business or personal account.
  - Each transaction can be either a Return or a Payment.
  - Each return and each payment is related to one credit card.
  - Each order contains one or more order items and each order item can belong to one and only one order.
  - Each order has one and only one order\_status, and each order\_status belongs to one and only one order.
  - Order Item is separate from the Item table as it does not contain item details such as category, color, desc, etc.
  - The purpose of Order Item is to link the Item and Order tables. It is essentially the line item of the order.
  - Each item can have zero or many reviews, but each review can only belong to one and one item.

-
5. **Relational Schema**
- Account( **account\_ID** , registration\_ID, fName, lName, email, cell\_Num, logon\_ID, password, create\_Date, account\_Type)

- Save\_For\_Later( **sfl\_account\_ID, sfl\_ID,** sfl\_item\_ID)
 Foreign key sfl\_account\_ID references Account(account\_ID);
 Foreign key sfl\_item\_ID references Item(item\_ID);

- Customer\_Order( **order\_ID,** account\_ID, s\_street, s\_City, s\_State, s\_Zip, order\_date, receiver\_name, delivery\_date, dispatch\_date)
 Foreign key account\_ID references Account(account\_ID);

- Order\_Status( **status\_Order\_ID, status\_Timestamp,** status)
 Foreign key status\_order\_ID references Customer\_Order(order\_ID);

- Order\_Item( **order\_ID, order\_item\_ID** , item\_ID, discounted\_price, quantity)
 Foreign key order\_ID references Customer\_Order(order\_ID);
 Foreign key item\_ID references Item(item\_ID);

- Item( **item\_ID** , sku, name, price, item\_desc, category, stock, item\_Star, item\_size, color)


- Payment( **payment\_id** , order\_id, payment\_date, total\_amount, card\_n)
 Foreign Key card\_n references Card(card\_number);
 Foreign Key order\_id references Customer\_Order(order\_id);

- Return( **return\_ID,** return\_date, refund\_amount, order\_id, card\_n)
 Foreign Key order\_id references Customer\_Order(order\_ID);
 Foreign Key card\_n references Card(card\_number);

- Card( **card\_Number** , cc\_Name, pin, b\_street, b\_city, b\_state, b\_zip)

- Return\_line\_item( **return\_ID** , **return\_item\_ID** , quantity, order\_item)
Foreign Key return\_ID references Return(return\_ID); Foreign Key order\_item references Order\_item(order\_item\_ID);

- Review( **review\_ID** , r\_star, comments, reviewDate, useful\_flag, num\_of\_words, review\_account, review\_item)
Foreign Key review\_account references Account(account\_ID); Foreign Key review\_item references Item(item\_ID);




6. **Data Dictionary**

Account

| account\_ID | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| registration\_ID | NOT NULL | VARCHAR2(10) | User Registration ID |
| fName | NOT NULL | VARCHAR2(20) | First Name |
| lName | NOT NULL | VARCHAR2(40) | Last Name |
| email | NOT NULL | VARCHAR2(320) | Email |
| cell\_Num | | CHAR (12) | Phone Number |
| logon\_ID | NOT NULL | VARCHAR2(20) | UserName |
| password | NOT NULL | VARCHAR2(20) | Password |
| create\_Date | NOT NULL | DATE | Account created on date |
| account\_Type | NOT NULL | CHAR(1) | Account Type |

Save\_For\_Later

| sfl\_account\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| --- | --- | --- | --- |
| sfl\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| sfl\_item\_ID | NOT NULL | VARCHAR2(10) | Item&#39;s ID |
| save\_Date | NOT NULL | DATE | Item saved on date |


Customer\_Order

| order\_ID | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| account\_ID | NOT NULL | VARCHAR2(10) | Account&#39;s ID |
| s\_Street | | VARCHAR2(40) | Shipping Street |
| s\_City | | VARCHAR2(20) | Shipping City |
| s\_State | | CHAR(2) | Shipping State |
| s\_Zip | | CHAR(10) | Shipping Zip Code |
| order\_date | | DATE | Order Date |
| receiver\_name | | VARCHAR2(40) | Receiver&#39;s Name |
| delivery\_date | | DATE | Delivery Date |
| dispatch\_date | | DATE | Dispatch Date |

Order\_Status

| status\_Order\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| --- | --- | --- | --- |
| status\_Timestamp | NOT NULL | DATE | Partial Primary Key |
| status | NOT NULL | VARCHAR2(40) | Order&#39;s status |

Order\_Item

| order\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| --- | --- | --- | --- |
| order\_item\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| item\_ID | NOT NULL | VARCHAR2(10) | Item&#39;s ID |
| discounted\_price | NOT NULL | NUMBER(12,2) | Discounted Price |
| quantity | NOT NULL | NUMBER(20) | Quantity of ordered items |

Item

| item\_ID | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| sku | NOT NULL | CHAR(8) | Stock keeping unit |
| name | NOT NULL | VARCHAR2(40) | Product Name |
| price | NOT NULL | NUMBER(12,2) | Product Price |
| item\_desc | | VARCHAR2(100) | Product Description |
| category | | VARCHAR2(10) | Product Category |
| stock | NOT NULL | NUMBER(5) | Product stock |
| item\_Star | | NUMBER(1) | Product Review |
| item\_size | | VARCHAR2(5) | Product Size |
| color | | VARCHAR2(10) | Product color |


Payment

| payment\_Id | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| order\_Id | NOT NULL | VARCHAR2(10) | Order&#39;s ID |
| payment\_Date | | DATE | Date of Payment |
| total\_Amount | | NUMBER(12,2) | Total Payment Amount |
| card\_N | | VARCHAR2(16) | Card Number |

Card

| card\_Number | NOT NULL | VARCHAR2(16) | Primary Key |
| --- | --- | --- | --- |
| cc\_Name | NOT NULL | VARCHAR2(40) | Account holder name |
| pin | NOT NULL | NUMBER(5) | Credit Card&#39;s pin |
| b\_Street | | VARCHAR2(40) | Address street |
| b\_City | | VARCHAR2(20) | City |
| b\_State | | CHAR(2) | State |
| b\_Zip | | CHAR(10) | Zip code (Postal code) |

Return\_line\_item

| return\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| --- | --- | --- | --- |
| return\_item\_ID | NOT NULL | VARCHAR2(10) | Partial Primary Key |
| quantity | NOT NULL | Number(20) | Quantity |
| order\_item\_ID | NOT NULL | VARCHAR2(10) | Order\_Item&#39;s ID |

Review

| review\_ID | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| r\_star | NOT NULL | NUMBER(1) | Review&#39;s number of stars |
| comments | | VARCHAR2(255) | Review comment |
| reviewDate | NOT NULL | DATE | Date of review |
| useful\_flag | | NUMBER(1) | 0 being Useful, 1 being Not Useful |
| num\_of\_words | | NUMBER(3) | Review&#39;s number of words |
| review\_account | NOT NULL | VARCHAR2(10) | Account&#39;s ID |
| review\_item | NOT NULL | VARCHAR2(10) | Item&#39;s ID |


Return

| return\_ID | NOT NULL | VARCHAR2(10) | Primary Key |
| --- | --- | --- | --- |
| refund\_amount | NOT NULL | NUMBER(12,2) | Amount Refunded |
| return\_date | NOT NULL | DATE | Return date |
| order\_ID | NOT NULL | VARCHAR2(10) | Customer order&#39;s ID |
| card\_n | NOT NULL | VARCHAR2(16) | Card&#39;s number |





7. Sample Data
- **Select \* from all Tables**

##


## select \* from Account;


| **ACCOUNT\_ID** | **REGISTRATION\_ID** | **FNAME** | **LNAME** | **EMAIL** | **CELL\_NUM** | **LOGON\_ID** | **PASSWORD** | **CREATE\_DATE** | **ACCOUNT\_TYPE** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **1234567890** | **1234567899** | **Brian** | **Kong** | **Bk555@drexel.edu** | **023-123-1234** | **bk555** | **bk123** | **20-NOV-20** | **B** |
| **2298387651** | **4500078457** | **Mariachiara** | **Acconcia** | **ma3768@drexel.edu** | **393456890098** | **mariachiara3768accon** | **678545fggfkty566bvgg** | **05-DEC-20** | **P** |
| **7184545773** | **7186729830** | **Tony** | **Stark** | **tony.stark@avenger.com** | **232-534-8732** | **tstark15** | **lkjhgfdsa** | **26-APR-19** | **P** |
| **1000** | **2000** | **Super** | **Man** | **superman@gmail.com** | **212-683-2039** | **superbro** | **super1234** | **01-JAN-19** | **P** |

**4 rows selected.**

## select \* from Save\_for\_later;

| **SFL\_ACCOUNT\_ID** | **SFL\_ID** | **SFL\_ITEM\_ID** | **SAVE\_DATE** |
| --- | --- | --- | --- |
| **7184545773** | **987345623** | **4983783429** | **10-MAY-20** |
| **2298387651** | **9936475125** | **2123987345** | **23-MAY-20** |
| **1000** | **202020** | **4983783429** | **30-MAY-20** |

**3 rows selected.**









## select \* from Customer\_Order;

| **ORDER\_ID** | **ACCOUNT\_ID** | **S\_STREET** | **S\_CITY** | **S\_STATE** | **S\_ZIP** | **ORDER\_DATE** | **RECEIVER\_NAME** | **DELIVERY\_DATE** | **DISPATCH\_DATE** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **0000000002** | **1234567890** | **2100 Walnut St** | **Philadelphia** | **PA** | **19103** | **21-NOV-20** | **Brian** | **22-NOV-20** | **21-NOV-20** |
| **6141876715** | **2298387651** | **Pompeo Neri street** | **Philadelphia** | **PA** | **19104** | **05-DEC-20** | **Mary Acconcia** | **12-DEC-20** | **05-DEC-20** |
| **342354465** | **7184545773** | **6111 5th avenue** | **New York City** | **NY** | **10001** | **21-JUN-19** | **Tony Stark** | **26-JUN-19** | **23-JUN-19** |
| **001** | **1000** | **Super street** | **Philadelphia** | **PA** | **19099** | **16-JAN-20** | **Clark** | **25-JAN-20** | **18-JAN-20** |

**4 rows selected.**

## select \* from Order\_Status;

| **STATUS\_ORDER\_ID** | **STATUS** | **STATUS\_TIMESTAMP** |
| --- | --- | --- |
| **342354465** | **Delivered** | **26-June-2019 11:02** |
| **0000000002** | **Delivered** | **25-NOV-2020 12:14:07** |
| **6141876715** | **Shipped** | **06-MAY-2020** |
| **001** | **Delivered** | **25-JAN-2020 10:53:21** |

**4 rows selected.**









## select \* from Order\_Item;

| **ORDER\_ID** | **ORDER\_ITEM\_ID** | **ITEM\_ID** | **DISCOUNTED\_PRICE** | **QUANTITY** |
| --- | --- | --- | --- | --- |
| **342354465** | **9297426093** | **4983783429** | **80** | **3** |
| **0000000002** | **0000012345** | **0000000321** | **0** | **1** |
| **6141876715** | **9835472111** | **2123987345** | **89.99** | **2** |
| **001** | **333** | **1000** | **499.99** | **1** |

**4 rows selected.**

## select \* from Item;

| **ITEM\_ID** | **SKU** | **NAME** | **PRICE** | **ITEM\_DESC** | **CATEGORY** | **STOCK** | **ITEM\_STAR** | **ITME\_SIZES** | **COLOR** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **4983783429** | **72290323** | **T-shirt** | **100** | **Plain T-Shirt with Supreme Logo on it.** | **Tshirts** | **30** | **5** | **M** | **Black** |
| **0000000321** | **12121212** | **Best Socks** | **30.5** | **Low Quality Socks. Made with cheap materials.** | **Socks** | **300** | **5** | **M** | **Blue** |
| **2123987345** | **00017465** | **Womens Jeans** | **99.99** | **Women&#39;s blue high-waist skinny jeans** | **Jeans** | **23** | **4** | **M** | **Blue** |
| **1000** | **00000012** | **Superman pants** | **599.99** | **Superman&#39;s blue pants** | **Costume** | **10** | **5** | **M** | **Blue** |

**4 rows selected.**



## select \* from Return;

| **RETURN\_ID** | **REFUND\_AMOUNT** | **RETURN\_DATE** | **ORDER\_ID** | **CARD\_N** |
| --- | --- | --- | --- | --- |
| **9028394029** | **30** | **30-JUN-19** | **342354465** | **9034029487348930** |
| **0928723615** | **30.5** | **03-DEC-20** | **0000000002** | **1234432198766789** |
| **1111983344** | **80** | **09-MAY-20** | **6141876715** | **0091002341** |
| **8888** | **399.99** | **10-FEB-20** | **001** | **1234123412341234** |

**4 rows selected.**

## select \* from Payment;

| **PAYMENT\_ID** | **ORDER\_ID** | **PAYMENT\_DATE** | **TOTAL\_AMOUNT** | **CARD\_N** |
| --- | --- | --- | --- | --- |
| **9308648390** | **342354465** | **22-JUN-19** | **240** | **9034029487348930** |
| **1000000398** | **0000000002** | **22-NOV-20** | **30.5** | **1234432198766789** |
| **9827333344** | **6141876715** | **05-MAY-20** | **179.98** | **0091002341** |
| **3333** | **001** | **16-JAN-20** | **499.99** | **1234123412341234** |

**4 rows selected.**


## select \* from Card;

| **CARD\_NUMBER** | **CC\_NAME** | **PIN** | **B\_STREET** | **B\_SITY** | **B\_STATE** | **B\_ZIP** |
| --- | --- | --- | --- | --- | --- | --- |
| **9034029487348930** | **Tony Stark** | **782** | **6111 5th avenue** | **New York City** | **NY** | **10001** |
| **1234432198766789** | **Visa** | **4321** | **2100 Walnut St** | **Philadelphia** | **PA** | **19103** |
| **0091002341** | **Mariachiara Acconcia** | **1299** | **Pompeo Neri street** | **Philadelphia** | **PA** | **19104** |
| **1234123412341234** | **Richard Hong** | **1234** | **Super street** | **Philadelphia** | **PA** | **19099** |

**4 rows selected.**
## select \* from Return\_line\_item;

| **RETURN\_ID** | **RETURN\_ITEM\_ID** | **QUANTITY** | **ORDER\_ITEM** | **ORDER\_ID** |
| --- | --- | --- | --- | --- |
| **9028394029** | **6384729375** | **1** | **9297426093** | **342354465** |
| **0928723615** | **0890236511** | **1** | **0000012345** | **0000000002** |
| **1111983344** | **0027286993** | **1** | **9835472111** | **6141876715** |
| **8888** | **1234** | **1** | **333** | **001** |

**4 rows selected.**

## select \* from Review;

| **REVIEW\_ID** | **R\_STAR** | **COMMENTS** | **REVIEWDATE** | **USEFUL\_FLAG** | **NUM\_OF\_WORDS** | **REVIEW\_ACCOUNT** | **REVIEW\_ITEM** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **8930290349** | **4** | **T-shirt is amazing, shrinked a little bit but it still fits perfectly. Just going to resell** | **27-JUN-19** | **0** | **16** | **7184545773** | **4983783429** |
| **0000000023** | **3** | **Not Bad** | **02-SEP-20** | **0** | **2** | **1234567890** | **0000000321** |
| **7799262181** | **4** | **Good product for the given price** | **07-MAY-20** | **0** | **6** | **2298387651** | **2123987345** |
| **123123** | **5** | **Super superman pants** | **07-FEB-20** | **0** | **3** | **1000** | **1000** |

**4 rows selected.**



