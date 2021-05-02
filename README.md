INFO 605 - GUFS DBMS

**INFO 605: Fall 2020**

**Online Clothing Store**

Members: _Mariachiara Acconcia, Brian Kong, Janam Patel, and Richard Hong_

1. **Summary**

The purpose of this project is to provide a relational database solution to keep track of e-commerce entities. The database is intended for Give Us Five Stars (GUFS), an online clothing store. This document outlines the process that was taken to create the database system. This includes the goals, scope, requirements, ERD, relational schema, and the SQL implementation. In this project we tried to create a simplified database for a real world E-commerce system. The main aspects that are usually visible to E-commerce system users were included in our scope, while we left out all the system&#39;s internal aspects and calculations.

1. **PROJECT STATEMENT**
  - Overall Goals of the System
 This project is an E-commerce database system for a new E-commerce clothing website named Give Us Five Stars (GUFS) that will store information about products, such as apparel, footwear, sportswear, etc. and customers, and orders. This system aims to create a single database that combines all of the data for a new E-commerce clothing website, GUFS. Unified data in the E-commerce website enables a single application that supports all aspects of the company&#39;s needs or multiple applications without redundant data. For this project, the authors have decided to use a fictional organization, Give Us Five Stars (GUFS), that reflects the actual data needs and challenges of many E-commerce systems.

  - Context and Importance of the System
 Currently, GUFS stores data in separate databases. This makes it difficult to track data between accounts, orders, and items. GUFS must secure transaction reliability when customers make their purchases. The number of items in the warehouse should be updated in real-time. Also, when customers search for products they want, GUFS must provide search results quickly. An integrated database would provide transaction reliability, real-time update, and better-searching performance. Users would be able to track their order history, saved for later items, billing, and shipping information, and possible discounts applied to items they order.

  - Scope of the Project
    - IN-Scope
 This database will store data for all customers, all transactions made by customers, and all products. The product may be any cloth type, such as apparel, footwear, sportswear, formal wear, accessories, etc. This database&#39;s scope will also include data about the estimated delivery date, shipping information, payment options, products&#39; reviews, and save for later/favorite list. This E-commerce database system will also track records of customers and products such as cancelation rate, and return rate.

    - Out-Scope
 The database does not store employees&#39; information and information of warehouses that may affect delivery costs. Nor will it track the entire GUFS budget, including payroll and benefits, operating costs, building costs, and maintenance costs.
2. **REQUIREMENTS SPECIFICATION**

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

1. **Conceptual Design**
  - ![](RackMultipart20210502-4-1c6ocnf_html_a75383f0231fedd7.png)


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
- **Relational Schema**
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




1. **Data Dictionary**

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




1. **Schema and Data**
  - **Create Tables and Inserts**


**-- Account 1**** drop table Account cascade constraints; ****create table Account**** (account\_ID varchar2(10) NOT NULL,****registration\_ID varchar2(10) NOT NULL,****fName varchar2(20) NOT NULL,****lName varchar2(40) NOT NULL,****email varchar2(320) NOT NULL,****cell\_Num char(12) NULL,****logon\_ID varchar2(20) NOT NULL,****password varchar2(20) NOT NULL,****create\_Date DATE NOT NULL,****account\_Type char(1) NOT NULL,****constraint account\_Type check(account\_Type IN (&#39;P&#39;,&#39;B&#39;)),****constraint account\_pk primary key (account\_ID));**

**-- Item 2**** drop table item cascade constraints; ****create table item**** (item\_ID varchar2(10) not null,****sku char(8) not null,****name varchar2(40) not null,****price number(12,2) not null,****item\_desc varchar2(100) null,****category varchar2(10) null,****stock number(5) not null,****item\_star number(1) null,****itme\_sizes varchar2(5) null,****color varchar2(10) null,****constraint item\_pk primary key (item\_id));**

**-- CARD 3**** drop table CARD cascade constraints; ****create table CARD**** (card\_number VARCHAR2(16) not null,****cc\_name VARCHAR2(40) not null,****pin CHAR(4) not null,****b\_street VARCHAR2(40),****b\_sity VARCHAR2(20),****b\_state CHAR(2),****b\_zip CHAR(10),****constraint Card\_PK primary Key (Card\_Number));**


**-- Customer\_Order 4**** drop table Customer\_Order cascade constraints; ****create table Customer\_Order**** (order\_ID varchar2(10) NOT NULL,****account\_ID varchar2(10) NOT NULL,****s\_street varchar2(40) NULL,****s\_City varchar2(20) NULL,****s\_State CHAR(2) NOT NULL,****s\_Zip CHAR(10) NULL,****order\_date DATE NULL,****receiver\_name varchar2(40) NOT NULL,****delivery\_date DATE NULL, ****dispatch\_date DATE NULL,**** constraint Customer\_Order\_pk primary key (order\_ID),****constraint account\_order foreign key (account\_ID) references Account);**

**-- Order\_Item 5**** drop table Order\_Item cascade constraints; ****create table Order\_Item**** (order\_ID varchar2(10) NOT NULL,****order\_item\_ID varchar2(10) NOT NULL,****item\_ID varchar2(10) NOT NULL,****discounted\_price number(12,2) NOT NULL,****quantity number(20) NOT NULL,****constraint order\_item\_pk primary key (order\_ID, order\_item\_ID),****constraint order\_id foreign key (order\_ID) references Customer\_Order,****constraint item\_id foreign key (item\_ID) references Item);**

**-- ORDER\_STATUS 6**** drop table ORDER\_STATUS cascade constraints; ****create table ORDER\_STATUS**** (status\_Order\_ID VARCHAR2(10) not null,****status varchar2(40) null,****status\_Timestamp varchar2(20) null,****constraint Status\_PK primary key (Status\_Order\_ID, Status\_Timestamp),****constraint STATUS\_fk\_Order foreign key (status\_order\_ID) references Customer\_Order(order\_ID)****);**


**-- Payment 7**** drop table Payment cascade constraints; ****create table Payment**** (payment\_id varchar2(10) NOT NULL,****order\_id varchar2(10) NOT NULL,****payment\_date DATE NULL,****total\_amount NUMBER(12,2) NULL,****card\_n varchar2(16) NULL,****constraint Payment\_pk primary key (payment\_id),****constraint Payment\_fk\_CARDNUM foreign key (card\_n) references Card(card\_number),****constraint Payment\_fk\_Customer\_Order foreign key (order\_id) references Customer\_Order(order\_id));**

**-- Return 8**** drop table Return cascade constraints; ****create table Return**** (return\_ID varchar2(10) NOT NULL,****refund\_amount number(12,2) NOT NULL,****return\_date date NOT NULL,****order\_ID varchar2(10) NOT NULL,****card\_n varchar2(16) NOT NULL,****constraint return\_pk primary key (return\_ID),****constraint return\_order foreign key (order\_ID) references Customer\_Order,****constraint c\_card foreign key (card\_n) references Card);**


**-- Return\_line\_item 9**** drop table Return\_line\_item cascade constraints; ****create table Return\_line\_item**** (return\_ID varchar2(10) NOT NULL,****return\_item\_ID varchar2(10) NOT NULL,****quantity NUMBER(20) NOT NULL,****order\_item varchar2(10) NOT NULL,****order\_ID varchar2(10) NOT NULL,****constraint Return\_line\_item\_pk primary key (return\_ID, return\_item\_ID),****constraint Return\_line\_item\_fk\_RETURN foreign key (return\_ID) references Return(return\_ID),****constraint Return\_line\_fk\_id\_ITEM foreign key (order\_ID,order\_item) references Order\_Item(order\_ID, order\_item\_ID)****);**


**-- Review 10**** drop table Review cascade constraints; ****create table Review**** (review\_ID varchar2(10) NOT NULL,****r\_star number(1) NOT NULL,****comments varchar2(255), ****reviewDate date NOT NULL,**** useful\_flag number(1),****num\_of\_words number(3),****review\_account varchar(10) NOT NULL,****review\_item varchar(10) NOT NULL,****constraint useful\_flag check(useful\_flag IN (1,0)),****constraint review\_pk primary key (review\_ID),****constraint r\_account foreign key (review\_account) references Account,****constraint r\_item foreign key (review\_item) references Item);**

**-- Save\_For\_Later 11**** drop table Save\_For\_Later cascade constraints; ****create table Save\_For\_Later**** (sfl\_account\_ID varchar2(10) NOT NULL,****sfl\_ID varchar2(10) NOT NULL,****sfl\_item\_ID varchar2(10) NOT NULL, ****save\_Date DATE NOT NULL,**** constraint Save\_For\_Later\_pk primary key (sfl\_account\_ID, sfl\_ID),****constraint Save\_For\_Later\_fk\_ACCOUNT foreign key (sfl\_account\_ID) references Account(account\_ID),****constraint Save\_For\_Later\_fk\_ITEM foreign key (sfl\_item\_ID) references Item(item\_ID));**


**-- INSERTS**

**-- Account**** INSERT INTO ACCOUNT VALUES (&#39;1234567890&#39;, &#39;1234567899&#39;, &#39;Brian&#39;, &#39;Kong&#39;, &#39;Bk555@drexel.edu&#39;, &#39;023-123-1234&#39;, &#39;bk555&#39;, &#39;bk123&#39;, &#39;20-NOV-2020&#39;, &#39;B&#39;);**
**INSERT INTO ACCOUNT VALUES (&#39;2298387651&#39;, &#39;4500078457&#39;, &#39;Mariachiara&#39;, &#39;Acconcia&#39;, &#39;ma3768@drexel.edu&#39;, &#39;393456890098&#39;, &#39;mariachiara3768accon&#39;, &#39;678545fggfkty566bvgg&#39;, &#39;05-DEC-2020&#39;, &#39;P&#39;);**
**INSERT INTO ACCOUNT VALUES (&#39;7184545773&#39;, &#39;7186729830&#39;, &#39;Tony&#39;, &#39;Stark&#39;, &#39;tony.stark@avenger.com&#39;, &#39;232-534-8732&#39;, &#39;tstark15&#39;, &#39;lkjhgfdsa&#39;, &#39;26-APRIL-2019&#39;, &#39;P&#39;);**
**INSERT INTO ACCOUNT VALUES (&#39;1000&#39;, &#39;2000&#39;, &#39;Super&#39;, &#39;Man&#39;, &#39;superman@gmail.com&#39;, &#39;212-683-2039&#39;, &#39;superbro&#39;, &#39;super1234&#39;, &#39;1-Jan-2019&#39;, &#39;P&#39;);**

**-- Item**
**INSERT INTO item VALUES (&#39;4983783429&#39;, &#39;72290323&#39;, &#39;T-shirt&#39;, &#39;100&#39;, &#39;Plain T-Shirt with Supreme Logo on it.&#39;, &#39;Tshirts&#39;, &#39;30&#39;, &#39;4.8&#39;, &#39;M&#39;, &#39;Black&#39;);**
**INSERT INTO ITEM VALUES (&#39;0000000321&#39;, &#39;12121212&#39;, &#39;Best Socks&#39;, &#39;30.50&#39;, &#39;Low Quality Socks. Made with cheap materials.&#39;, &#39;Socks&#39;, &#39;300&#39;, &#39;5&#39;, &#39;M&#39;, &#39;Blue&#39;);**

**INSERT INTO Item VALUES (&#39;2123987345&#39;, &#39;00017465&#39;, &#39;Womens Jeans&#39;, &#39;99.99&#39;, &#39;Women&#39;&#39;s blue high-waist skinny jeans&#39;, &#39;Jeans&#39;, &#39;23&#39;, &#39;4&#39;, &#39;M&#39;, &#39;Blue&#39;);**
**INSERT INTO ITEM VALUES (&#39;1000&#39;, &#39;00000012&#39;, &#39;Superman pants&#39;, 599.99, &#39;Superman&#39;&#39;s blue pants&#39;, &#39;Costume&#39;, 10, 5, &#39;M&#39;, &#39;Blue&#39;);**


**-- Card**

**INSERT INTO card VALUES (&#39;9034029487348930&#39;, &#39;Tony Stark&#39;, &#39;782&#39;, &#39;6111 5th avenue&#39;, &#39;New York City&#39;, &#39;NY&#39;, &#39;10001&#39;);**
**INSERT INTO CARD VALUES (&#39;1234432198766789&#39;, &#39;Visa&#39;, &#39;4321&#39;, &#39;2100 Walnut St&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19103&#39;);**
**INSERT INTO Card VALUES (&#39;0091002341&#39;, &#39;Mariachiara Acconcia&#39;, &#39;1299&#39;, &#39;Pompeo Neri street&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19104&#39;);**
**INSERT INTO Card VALUES (&#39;1234123412341234&#39;, &#39;Richard Hong&#39;, &#39;1234&#39;, &#39;Super street&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19099&#39;);**


**-- Customer\_Order**
**INSERT INTO CUSTOMER\_ORDER VALUES (&#39;0000000002&#39;, &#39;1234567890&#39;, &#39;2100 Walnut St&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19103&#39;, &#39;21-NOV-2020&#39;, &#39;Brian&#39;, &#39;22-NOV-2020&#39;, &#39;21-NOV-2020&#39;);**
**INSERT INTO CUSTOMER\_ORDER VALUES (&#39;6141876715&#39;, &#39;2298387651&#39;, &#39;Pompeo Neri street&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19104&#39;, &#39;05-DEC-2020&#39;, &#39;Mary Acconcia&#39;, &#39;12-DEC-2020&#39;, &#39;05-DEC-2020&#39;);**
**INSERT INTO customer\_order VALUES (&#39;342354465&#39;, &#39;7184545773&#39;, &#39;6111 5th avenue&#39;, &#39;New York City&#39;, &#39;NY&#39;, &#39;10001&#39;, &#39;21-June-2019&#39;, &#39;Tony Stark&#39;, &#39;26-June-2019&#39;, &#39;23-June-2019&#39;);**
**INSERT INTO customer\_order VALUES (&#39;001&#39;, &#39;1000&#39;, &#39;Super street&#39;, &#39;Philadelphia&#39;, &#39;PA&#39;, &#39;19099&#39;, &#39;16-JAN-2020&#39;, &#39;Clark&#39;, &#39;25-JAN-2020&#39;, &#39;18-JAN-2020&#39;);**


**-- Order\_Item**
**INSERT INTO Order\_Item VALUES (&#39;342354465&#39;, &#39;9297426093&#39;, &#39;4983783429&#39;, &#39;80&#39;, &#39;3&#39;);**
**INSERT INTO ORDER\_ITEM VALUES (&#39;0000000002&#39;, &#39;0000012345&#39;, &#39;0000000321&#39;, &#39;0&#39;, &#39;1&#39;);**
**INSERT INTO Order\_Item VALUES (&#39;6141876715&#39;, &#39;9835472111&#39;, &#39;2123987345&#39;, &#39;89.99&#39;, &#39;2&#39;);**
**INSERT INTO Order\_Item VALUES (&#39;001&#39;, &#39;333&#39;, &#39;1000&#39;, &#39;499.99&#39;, &#39;1&#39;);****-- Order\_Status**
**INSERT INTO ORDER\_STATUS VALUES (&#39;342354465&#39;, &#39;Delivered&#39;, &#39;26-June-2019 11:02&#39;);**
**INSERT INTO ORDER\_STATUS VALUES (&#39;0000000002&#39;, &#39;Delivered&#39;, &#39;25-NOV-2020 12:14:07&#39;);**
**INSERT INTO Order\_Status VALUES (&#39;6141876715&#39;, &#39;Shipped&#39;, &#39;06-MAY-2020&#39;);**
**INSERT INTO Order\_Status VALUES (&#39;001&#39;, &#39;Delivered&#39;, &#39;25-JAN-2020 10:53:21&#39;);**

**-- Payment**
**INSERT INTO Payment VALUES (&#39;9308648390&#39;, &#39;342354465&#39;, &#39;22-June-2019&#39;, &#39;240.00&#39;, &#39;9034029487348930&#39;);**
**INSERT INTO PAYMENT VALUES (&#39;1000000398&#39;, &#39;0000000002&#39;, &#39;22-NOV-2020&#39;, &#39;30.50&#39;, &#39;1234432198766789&#39;);**
**INSERT INTO Payment VALUES (&#39;9827333344&#39;, &#39;6141876715&#39;, &#39;05-MAY-2020&#39;, &#39;179.98&#39;, &#39;0091002341&#39;);**
**INSERT INTO Payment VALUES (&#39;3333&#39;, &#39;001&#39;, &#39;16-JAN-2020&#39;, &#39;499.99&#39;, &#39;1234123412341234&#39;);**


**-- Return**
**INSERT INTO Return VALUES (&#39;9028394029&#39;, &#39;30&#39;, &#39;30-June-2019&#39;, &#39;342354465&#39;, &#39;9034029487348930&#39;);**
**INSERT INTO Return VALUES (&#39;0928723615&#39;, &#39;30.50&#39;, &#39;03-DEC-2020&#39;, &#39;0000000002&#39;, &#39;1234432198766789&#39;);**
**INSERT INTO Return VALUES (&#39;1111983344&#39;, &#39;80&#39;, &#39;09-MAY-2020&#39;, &#39;6141876715&#39;, &#39;0091002341&#39;);**
**INSERT INTO Return VALUES (&#39;8888&#39;, &#39;399.99&#39;, &#39;10-FEB-2020&#39;, &#39;001&#39;, &#39;1234123412341234&#39;);**


**-- Return\_Line\_Item**
**INSERT INTO Return\_line\_item VALUES (&#39;9028394029&#39;,&#39;6384729375&#39;, &#39;1&#39;, &#39;9297426093&#39;,&#39;342354465&#39;);**
**INSERT INTO RETURN\_LINE\_ITEM VALUES (&#39;0928723615&#39;,&#39;0890236511&#39;, &#39;1&#39;, &#39;0000012345&#39;,&#39;0000000002&#39;);**
**INSERT INTO Return\_line\_item VALUES (&#39;1111983344&#39;, &#39;0027286993&#39;, &#39;1&#39;, &#39;9835472111&#39;, &#39;6141876715&#39;);**
**INSERT INTO Return\_line\_item VALUES (&#39;8888&#39;, &#39;1234&#39;, &#39;1&#39;, &#39;333&#39;, &#39;001&#39;);**


**-- Review**
**INSERT INTO Review VALUES (&#39;8930290349&#39;, &#39;4&#39;, &#39;T-shirt is amazing, shrinked a little bit but it still fits perfectly. Just going to resell&#39;, &#39;27-June-2019&#39;, &#39;0&#39;, &#39;16&#39;, &#39;7184545773&#39;, &#39;4983783429&#39;);**
**INSERT INTO REVIEW VALUES (&#39;0000000023&#39;, &#39;3&#39;, &#39;Not Bad&#39;, &#39;02-SEP-2020&#39;, &#39;0&#39;, &#39;2&#39;, &#39;1234567890&#39;, &#39;0000000321&#39;);**
**INSERT INTO Review VALUES (&#39;7799262181&#39;, &#39;4&#39;, &#39;Good product for the given price&#39;, &#39;07-MAY-2020&#39;, &#39;0&#39;, &#39;6&#39;, &#39;2298387651&#39;, &#39;2123987345&#39;);**
**INSERT INTO Review VALUES (&#39;123123&#39;, &#39;5&#39;, &#39;Super superman pants&#39;, &#39;07-feb-2020&#39;, &#39;0&#39;, &#39;3&#39;, &#39;1000&#39;, &#39;1000&#39;);**


**-- Save\_For\_Later 11**** drop table Save\_For\_Later cascade constraints; ****create table Save\_For\_Later**** (sfl\_account\_ID varchar2(10) NOT NULL,****sfl\_ID varchar2(10) NOT NULL,****sfl\_item\_ID varchar2(10) NOT NULL, ****save\_Date DATE NOT NULL,**** constraint Save\_For\_Later\_pk primary key (sfl\_account\_ID, sfl\_ID),****constraint Save\_For\_Later\_fk\_ACCOUNT foreign key (sfl\_account\_ID) references Account(account\_ID),****constraint Save\_For\_Later\_fk\_ITEM foreign key (sfl\_item\_ID) references Item(item\_ID));**

**-- Save\_For\_Later**** INSERT INTO save\_for\_later VALUES (&#39;7184545773&#39;, &#39;987345623&#39;, &#39;4983783429&#39;, &#39;10-MAY-2020&#39;);**
**INSERT INTO Save\_For\_Later VALUES (&#39;2298387651&#39;, &#39;9936475125&#39;, &#39;2123987345&#39;,&#39;23-MAY-2020&#39;);**
**INSERT INTO Save\_For\_Later VALUES (&#39;1000&#39;, &#39;202020&#39;, &#39;4983783429&#39;, &#39;30-MAY-2020&#39;);**



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



**DATA QUERIES**
**3 per person (Use joins and aggregation)**


1. **Queries by Mariachiara Acconcia**
  1. **Query 1 (English meaning, SQL, output, #rows)**

For each account ID, select the Item name, item price, and discounted price of each item ordered where the discount on the price is at least 20%.
SELECT A.account\_ID, I.name, I.price, OI.discounted\_PriceFROM Account A, Customer\_Order O, Order\_Item OI, Item IWHERE A.account\_ID=O.account\_IDAND O.order\_ID=OI.order\_IDAND OI.item\_ID=I.item\_IDAND OI.discounted\_price\&lt;=0.8\*I.price;
 ![](RackMultipart20210502-4-1c6ocnf_html_1fefa4253174e50.png)
Rows: 2

  1. **Query 2 (English meaning, SQL, output, #rows)**

Find the names of users that wrote reviews in 2020 and the average number of stars they gave.

SELECT A.fName, A.lName, AVG(R.r\_star) AS average\_starsFROM Account A, Review RWHERE A.account\_ID=R.review\_accountAND reviewDate\&gt;&#39;01-JAN-2020&#39;GROUP BY A.fname, A.lname;
 ![](RackMultipart20210502-4-1c6ocnf_html_ea55369ffc08ae72.png)
Rows: 3

  1. **Query 3 (EngDMLlish meaning, SQL, output, #rows)**
Find all users names that made expensive orders for other people (with expensive orders being anything greater than $200.00), count the number of those orders for each user and the total amount they spent on those orders. Find also the average number of days that it took for those orders to be delivered.

COLUMN full\_Name FORMAT A30;COLUMN receiver\_Name FORMAT A20;COLUMN total FORMAT $9999.99;

SELECT (A.fName || &#39; &#39; || A.lName) AS full\_Name, O.receiver\_Name, SUM(P.total\_Amount) AS total, COUNT(O.order\_Id) AS orders#, AVG(O.delivery\_Date-O.order\_Date) AS DaysFROM Account A, Customer\_Order O, Payment PWHERE O.account\_ID=A.account\_ID AND O.order\_ID=P.order\_id AND P.total\_Amount\&gt;200.00 AND (A.fName || &#39; &#39; || A.lName)!=O.receiver\_NameGROUP BY A.fname, A.lName, O.receiver\_Name;
 ![](RackMultipart20210502-4-1c6ocnf_html_f8009850a8649e33.png)
Rows; 1


1. **Queries Brian Kong**
  1. **Query 1 (English meaning, SQL, output, #rows)**

Find the most expensive item that a user has ordered with a first name beginning with &quot;Bri&quot;:
Select A.Fname, A.LNAME, MAX(I.Price) FROM ACCOUNT A, CUSTOMER\_ORDER C, ORDER\_ITEM O, ITEM I WHERE A.Account\_ID = C.Account\_ID AND C.order\_ID = O.order\_ID AND O.Item\_ID = I.Item\_ID AND A.Fname like &#39;Bri%&#39; GROUP BY A.Fname, A.Lname;
 ![](RackMultipart20210502-4-1c6ocnf_html_3ec8307f87272399.png)Rows: 1

  1. **Query 2 (English meaning, SQL, output, #rows)**

Select the cardholder name and billing street for any payments made on the 22nd of November, 2020:
Select C.cc\_name, C.B\_street FROM CARD C, PAYMENT P WHERE C.Card\_Number = P.Card\_n AND P.payment\_date = &#39;22-NOV-2020&#39;;
 ![](RackMultipart20210502-4-1c6ocnf_html_96f9d496b8552af.png)Rows:1

  1. **Query 3 (EngDMLlish meaning, SQL, output, #rows)**

Return the average review star rating for all items.
SELECT AVG(R.R\_STAR) FROM REVIEW R, ACCOUNT A WHERE R.USEFUL\_FLAG IN (0) AND A.account\_Type = &#39;P&#39;;
 ![](RackMultipart20210502-4-1c6ocnf_html_21dcb7698a07bb7.png)Rows: 1

1. **Queries by Janam Patel**
  1. **Query 1 (English meaning, SQL, output, #rows)**
 Display all account&#39;s fname,lname,emails, phone# and date when account created on, that are from NY

 select account.fname, account.lname, account.email, account.cell\_num, account.create\_date, customer\_order.S\_State
from ((customer\_orderinner join account on account.account\_id = customer\_order.account\_id))where customer\_order.S\_State = &#39;NY&#39;group by account.fname,account.lname, account.email, account.cell\_num, account.create\_date, customer\_order.S\_State; ![](RackMultipart20210502-4-1c6ocnf_html_f4a7b4fea028a5de.png)Rows: 1

  1. **Query 2 (English meaning, SQL, output, #rows)**
 Display total amount that was refunded for customer\_order from city of Philadelphia

 select sum(return.refund\_amount) as Philadelphia\_returnsfrom (( returninner join customer\_order on customer\_order.order\_ID = return.order\_ID))where customer\_order.S\_city = &#39;Philadelphia&#39;;
 ![](RackMultipart20210502-4-1c6ocnf_html_f1e9d4b9a7f1a763.png)Rows: 1

  1. **Query 3 (EngDMLlish meaning, SQL, output, #rows)**
 Display order\_id,payment date, return date, total amount, refund amount and difference of refund from total amount.

select payment.order\_id, payment.payment\_date, return.return\_date, payment.total\_amount, return.refund\_amount, (payment.total\_amount-return.refund\_amount) as Differencefrom (( paymentinner join return on return.card\_n = payment.card\_n));

 ![](RackMultipart20210502-4-1c6ocnf_html_5f5c93f711aaf968.png) **Rows: 4**

1. **Queries by Richard Hong**
  1. Display the First Name, Last Name, Phone, City of the shipping address, State of the shipping address, and the name of items for customers who bought Tshirts or Jeans.

COLUMN State FORMAT A5COLUMN &quot;Last Name&quot; FORMAT A15COLUMN &quot;Item Name&quot; FORMAT A30
SELECT A.fname AS &quot;First Name&quot;, A.lname as &quot;Last Name&quot;, A.cell\_num as PHONE, CO.s\_City AS City, CO.s\_State AS State, I.name AS &quot;Item Name&quot;FROM Account A, Customer\_Order CO, Order\_Item OI, Item IWHERE A.account\_ID = CO.account\_IDAND CO.order\_ID = OI.order\_IDAND OI.item\_ID = I.item\_IDAND I.category in (&#39;Tshirts&#39;, &#39;Jeans&#39;); ![](RackMultipart20210502-4-1c6ocnf_html_3d4c4907e9e3bdc5.png) **Rows:2**

  1. Display the First Name, Last Name, name of the item, description of the item, the item&#39;s selling price(discounted price), and the item&#39;s original price for customers who bought the most expensive item.

COLUMN Description FORMAT A30COLUMN &quot;Item Name&quot; FORMAT A30COLUMN &quot;Sell Price&quot; FORMAT $9999.99COLUMN &quot;Original Price&quot; FORMAT $9999.99
SELECT A.fname AS &quot;First Name&quot;, A.lname as &quot;Last Name&quot;, I.name AS &quot;Item Name&quot;, I.item\_desc AS Description, OI.discounted\_price AS &quot;Sell Price&quot;, I.price AS &quot;Original Price&quot;FROM Account A, Customer\_Order CO, Order\_Item OI, Item I WHERE A.account\_ID = CO.account\_IDAND CO.order\_ID = OI.order\_IDAND OI.item\_ID = I.item\_IDAND I.price = (SELECT MAX(price)FROM Item); ![](RackMultipart20210502-4-1c6ocnf_html_9631bcc1adc472bf.png) **Rows:1**

  1. Display the statistics for each category of items that were reviewed after December 31, 2019. The statistics include the highest price, the lowest price, and the average price of items for each category. Order the results in the ascending order of category.

COLUMN &quot;Maximum Price&quot; FORMAT $9999.99COLUMN &quot;Minimum Price&quot; FORMAT $9999.99COLUMN &quot;Average Price&quot; FORMAT $9999.99
SELECT I.category, MAX(I.price) AS &quot;Maximum Price&quot;, MIN(I.price) AS &quot;Minimum Price&quot;, AVG(I.price) AS &quot;Average Price&quot;FROM Item I, Review RWHERE I.item\_ID = R.review\_itemAND R.reviewDate \&gt; &#39;31-DEC-2019&#39;GROUP BY I.categoryORDER BY I.category;
 ![](RackMultipart20210502-4-1c6ocnf_html_c363baafdfa7b072.png) **Rows:3**








**DATA MANIPULATION (Each member must include at least one example of UPDATE and DELETE to any table in your database in the context of your requirements. For DML commands, use SET AUTOCOMMIT OFF so that you can rollback. For each deletion and update command, you must display the data before and after the command to confirm the correctness of the command. That is, I want you to practice insertion/deletion/update in your projects. For example,**
1. **DML by Mariachiara Acconcia**
  1.
SELECT \* from Review; ![](RackMultipart20210502-4-1c6ocnf_html_96f9fc049acc149c.png)

  1.
UPDATE ReviewSET r\_Star=&#39;5&#39;WHERE useful\_flag=&#39;0&#39;;

  1.
 ![](RackMultipart20210502-4-1c6ocnf_html_f3310fbb69497d9a.png)

  1. ROLLBACK;



  1.
SELECT \* from Order\_Status; ![](RackMultipart20210502-4-1c6ocnf_html_a8e2875ce298a864.png)


  1.
DELETE FROM Order\_StatusWHERE status=&#39;Delivered&#39;;


  1.
 ![](RackMultipart20210502-4-1c6ocnf_html_586e7ce2c2eed305.png)

  1. ROLLBACK;

1. **DML Brian Kong**
  1. ![](RackMultipart20210502-4-1c6ocnf_html_e66ce6123d222bec.png)
UPDATE Customer\_OrderSET delivery\_date = &#39;25-NOV-2020&#39;WHERE order\_ID = &#39;0000000002&#39;; ![](RackMultipart20210502-4-1c6ocnf_html_1f94a627fc172dc0.png)ROLLBACK;

 ![](RackMultipart20210502-4-1c6ocnf_html_67900c9c5dca6ab4.png)DELETE FROM save\_for\_laterWHERE SFL\_ACCOUNT\_ID like &#39;1234567890&#39;; ![](RackMultipart20210502-4-1c6ocnf_html_85e0c9dcd5215407.png)ROLLBACK;

1. **DML by Janam Patel**
  1. Select \* from customer\_order;
 ![](RackMultipart20210502-4-1c6ocnf_html_b5f3cb02a6737dac.png)
  2. Update customer\_order set s\_street = &#39;4283 42st Timesquare&#39; where receiver\_name = &#39;Tony Stark&#39;;

  3.
 ![](RackMultipart20210502-4-1c6ocnf_html_ba5f63a469f994a.png)
  4. Rollback;
  5. **select \* from review;**
 ![](RackMultipart20210502-4-1c6ocnf_html_b5283565fdba795f.png)
  6. delete from review where R\_star \&lt; 4;

  7.
 ![](RackMultipart20210502-4-1c6ocnf_html_747a11d0755940b5.png)
  8. Rollback;

2. **DML by Richard Hong**
  1. **Show data before the UPDATE command**
 ![](RackMultipart20210502-4-1c6ocnf_html_4cd2b48586c4401.png)

  1. **Perform UPDATE command**
UPDATE AccountSET cell\_num = &#39;123-456-7890&#39;WHERE Account\_ID = &#39;1000&#39;;

  1. **Show data after the UPDATE command**
 ![](RackMultipart20210502-4-1c6ocnf_html_56646f617d0bb608.png)

  1. **Perform ROLLBACK**
ROLLBACK;






  1. **Show data before the DELETE command**
 ![](RackMultipart20210502-4-1c6ocnf_html_fa9086d5966b69fc.png)

  1. **Perform DELETE command**
DELETE FROM save\_for\_laterWHERE save\_date \&lt; &#39;15-MAY-20&#39;;

  1. **Show data after the DELETE command**
 ![](RackMultipart20210502-4-1c6ocnf_html_e3a3e36c208aed4d.png)

  1. **Perform ROLLBACK**
ROLLBACK;









**Personal Summaries**


1. **Summary by Mariachiara Acconcia**
I believe that the hardest part of this project was to make every single part consistent with the others. Some things that worked and made perfectly sense in ERD were then sometimes hard to translate in the relational schema or to implement with SQL. That&#39;s why we had to change and cut some things from our original ERD, once we realised that it would be too complex to keep going with the implementation for the given time. If we had more time we could have definitely included more concepts in our scope, but our final project still reached a good complexity level. I feel like writing SQL queries for something that I have a better understanding of, since we developed every single phase, from the conceptual idea to the implementation, helped me to improve my understanding of SQL language and commands.
1. **Summary Brian Kong**
I feel that our database was relatively complex for a term project. Due to this we decided to omit some of the originally planned features. The current version of the database can support an e-commerce site. I believe the scope could have been reduced since as we progressed in the project we found that the complexity increased. My biggest takeaway from this experience is to be conservative when planning the project and identifying the scope.
2. **Summary by Janam Patel**
I believe when we first started our database had more details and was closer to the actual ecommerce database, which was good and easy until we were just writing the explanation for it, and drawing ERD for it. But when it comes to creating the actual database in oracle, it proved to be much more harder than expected. Although hard, it&#39;s not impossible, so if we had more time I believe we would&#39;ve been able to design that complex database. I think I learned a lot on how to write good relational schema, because good relational schema will make it easier when creating the table.
3. **Summary by Richard Hong**
Throughout this project, I could have practical experience in database modeling, design, and implementation. Web-based e-commerce systems have quite complex business requirements. Developing the ERD was beneficial to me to understand the domain, which I had never experienced. In this project, we had to deal with the scope many times to simplify the domain. It was repetitive and tedious, but we needed to iterate those steps. I could learn how important it is to build a proper conceptual schema - a map and a blueprint. Because that indicates how much I clearly understand the business needs and scope.

**Appendix**** We split up the work equally, outlined throughout the document.**

37
