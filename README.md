# ECommerce

```mermaid

---
title: Ecommerce
---
erDiagram
Product
Product {
	int id PK
	string name
	float price
	blob image
	string status
	int category_id FK
	int brand_id FK
	int stock_id FK
	datetime created_at
	datetime modified_at
}

Category {
	int id PK
	string name
	string description
	datetime created_at
	datetime modified_at
}

Brand {
	int id PK
	string name
}

Discount {
	int id PK
	int product_id FK
	int percentage
	datetime created_at
	datetime modified_at
}


Admin {
	int id PK
	string name
	string email
	string password
}


Customer {
	int id PK
	string first_name
	string last_name
	string city
	string state
	string email
	string gender
	string password
	blob image
}

Cart {
	int id
	int total_quantity
	int total_price
}

"Cart Item" {
	int id PK
	int cart_id FK
	datetime created_at
	datetime modified_at
}

Transaction {
	int id PK
	datetime time
	int order_id
	int customer_id
	int account_id	
}

Account {
	int id PK
	int card_numbre
	string card_name
	string password
}


Order {
	int id PK
	double total_price
	double total_quantity
	datetime created_at
	datetime modified_at
}

"Order Item" {
	int id PK
	int product_id FK
	int order_id FK
	int quantity
datetime created_at
	datetime modified_at
}

Notification {
	int id PK
	int order_id FK
	int customer_id FK
	string customer_email
	string status
}

Coupon {
	int id PK
	string code
	datetime expiration_date
	int usage_limit
	string end_type
	double value
	double percentage
	string discount_type
}

"Coupon History" {
	int id PK
	int coupon_id FK
	int order_id FK
	int customer_id FK
	int remaining_coupons
	int usages
	datetime time
}


Stock {
	int id PK
	int product_id FK
	int quantity
}

"Stock History" {
	int id PK
	datetime time
	int oreder_id FK
	string operation
	int sold_quantity
	int remaining_quantity	
	int total_quantity
}



Category ||--|{ Product : ""
Brand ||--|{ Product : ""
Product ||--|| Discount : ""
Product ||--|| Stock : ""


Customer ||--|| Cart : ""
Customer ||--|{ Order : ""
Customer ||--|{ Transaction : ""

Transaction ||--|| Account : ""
Transaction |{--|| Order : ""

Cart ||--|{ "Cart Item" : ""
"Cart Item" |{--|| Product : ""

Order ||--|{ "Order Item" : ""
"Order Item" |{--|| Product : ""

Order ||--|| Notification : ""
Order |{--|| Customer : ""
Order ||--|| Coupon : ""

Coupon ||--|{ "Coupon History" : ""
"Coupon History" |{--|| Customer : ""
"Coupon History" ||--|| Order : ""


"Stock History" ||--|| Order : ""





```
