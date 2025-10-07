 # 🛍️ E-commerce Data Analysis
 ## 📘 Project Overview

This project focuses on building and analyzing an E-commerce Database Model using MYSQL and Python.

The goal was to understand customer purchasing behavior, product trends, and department-level insights from a large e-commerce dataset.
## Objective

To design a relational database and perform data analysis to answer questions like:

* Which products are most frequently purchased or reordered?

* Which aisles and departments generate the most sales?
## Tools & Technologies
* Python
* Pandas, SQLAlchemy
* MySQL
* Jupyter Notebook
## Dataset Information
The dataset used in this project is taken from an open-source e-commerce data repository on Kaggle.

You can download it here:

-[Kaggle]  (https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)

## Working with Jupyter Notebook and SQL Connection

I used Jupyter Notebook for this entire project because it’s easy to run Python code, write SQL queries.
To connect my Python code with the SQL database 

I used two main libraries:

**mysql.connector** → to create the database and tables.

**SQLAlchemy** → to send large data files (CSV) directly to SQL tables using the .to_sql() function.

Here’s a example code of how I connected to my database and uploaded my CSV files
```md
python

import pandas as pd
import mysql.connector
from sqlalchemy import create_engine

# Step 1: Load the CSV files into Pandas DataFrames
orders_df = pd.read_csv("C://Users//username//Downloads//orders.csv").sample(10000)
products_df = pd.read_csv("C://Users//username//Downloads//products.csv")
aisles_df = pd.read_csv("C://Users//username//Downloads//aisles.csv")
departments_df = pd.read_csv("C://Users//username//Downloads//departments.csv")
order_products_df = pd.read_csv("C://Users//username//Downloads//order_products__prior.csv").sample(10000)

# Step 2: Connect to MySQL database
try:
    conn = mysql.connector.connect(
        host='localhost',
        user='root',
        password='root',
        database='ecommerce_data_analysis'
    )
    print(" Connection successful!")
except:
    print(" Connection failed!")

# Step 3: Create SQLAlchemy engine (for uploading data)
engine = create_engine("mysql+mysqlconnector://root:root@localhost:3306/ecommerce_data_analysis")

# Step 4: Upload DataFrames into MySQL tables
aisles_df.to_sql('aisles', con=engine, if_exists='replace', index=False)
departments_df.to_sql('departments', con=engine, if_exists='replace', index=False)
products_df.to_sql('products', con=engine, if_exists='replace', index=False)
orders_df.to_sql('orders', con=engine, if_exists='replace', index=False)
order_products_df.to_sql('order_products', con=engine, if_exists='replace', index=False)

print("All data uploaded successfully!")
```

Once the data was uploaded, I wrote SQL queries inside Jupyter Notebook to analyze the data, create temporary tables, and join the datasets.These queries helped me join different tables, summarize important data, and find patterns in customer behavior.

## 1️⃣ Order Information

I created a temporary table that joins the orders, order_products, and products tables to get complete information about each order — including product name, department, and aisle details.

```md
python
cursor.execute("""
 create temporary table product_info as 
 select 
 product_id, product_name,count(*) as total_orders, sum(reordered) as total_reorders,avg(add_to_cart_order) as avg_cart_order 
 from order_info 
 group by product_id,product_name ;
""")
```
This was the main query in my analysis — I used this table later to explore patterns like the most purchased products, reorder rates, and order timings.
It helped me understand how different datasets in the e-commerce system are connected and how SQL joins can be used to uncover business insights.
### Amrutha Nagothi
- 📧 amruthanagothi@gmail.com
- 🌐 [Linkedin](www.linkedin.com/in/amrutha-nagothi-3s)           [GitHub](https://github.com/ammu105)


<p align="center">
  Thank you for reviewing this project 💻❤️
</p>


