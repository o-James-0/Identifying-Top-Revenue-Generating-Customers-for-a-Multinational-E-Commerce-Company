# Identifying-Top-Revenue-Generating-Customers-for-a-Multinational-E-Commerce-Company
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe



# project overview
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe. 


The objective of the study is to analyze and identify the **Top 10 highest revenue-generating customers**, offering critical business insights into customer value, regional sales dynamics, and strategic growth opportunities.


Leveraging advanced data analytics techniques, including data preprocessing, aggregation, and visualization, this project uncovers key patterns in customer spending behavior across diverse markets. 


By ranking customers based on total revenue contribution, the analysis empowers business stakeholders with actionable intelligence to optimize customer relationship management, tailor marketing strategies, and enhance profitability in a globally competitive landscape.

This project serves as a practical application of data science principles in the domain of e-commerce, showcasing the impact of data-driven decision-making on strategic business outcomes.

### Problem Statement  
**Who are Top 10 Customers of the Company interms of Total Revenue generated since the company started ?**


### Project Objectives 

1. **To Identify Top Revenue-Generating Customers**

   * By Analyzing sales data to determine the top 10 customers contributing the highest total revenue across all regions.


2. **To Understand Revenue Concentration**

   * By Analyzing how much of the company's total revenue is concentrated among top customers.


3. **To Uncover Geographic Patterns**

   * By Assessing the global distribution of high-value customers across the Countries to identify key markets and regional revenue   clusters.


4. **To Support Strategic Decision-Making**

   * By Providing actionable insights to the company’s sales and marketing teams for developing targeted retention, loyalty, and upselling strategies.



5. **To Demonstrate Real-World Data Science Application**

   * By Showcasing the use of data science tools and techniques (data preprocessing, aggregation, visualization) in solving a real-world business problem.


6. **To Enable Stakeholder Communication**

   * By Creating intuitive visualizations and summaries that allow non-technical stakeholders to understand key findings and insights.


7. **To Lay the Groundwork for Predictive Modeling**

   * By Establishing a foundational dataset and insights that could be extended into customer lifetime value prediction or churn modeling in future phases.


### Data Source

**The Company's central transaction database**


### Project Methodology

- **Data Collection**: Data was collected from the Company's Central Transaction Database

- **Data Pre-processing**: Loaded the data from a CSV file into a Pandas Dataframe

- **Data Inspection and Cleaning**: Checked for Missing values, Checked for Duplicates.

- - Handled missing values
  - Handled duplicate values

- **Data Modification**: generated some  core metrics which were NOT provided from the dataset, and would be required for the purpose of the data   analysis

- **Data Aggregation**: To Compute the major metric : Total Revenue by Customer**

- **Data Sorting/ Data Ranking**: To Determine the Most Importat Metric:  **Top 10 highest revenue-generating customers**

- **Data Visualization**: To uncover the **Top 10 highest revenue-generating customers** in a pictorial form.

- **Data Interpretation**:

- **Key Findings**

- **Conclusions**

- **Reconmendation**



### Data Collection

Sales data was obtained from a central transaction database of the company representing orders placed by customers across multiple countries. Each record included attributes such as:

* `Customer ID`
* `OrderNo`
* `OrderQuantity`
* `CostPrice_usd`
* `SellingPrice_usd`
* `OrderDate`
* `CustomerName`
* `CustomerCity`
* `CustomerState`
* `CustomerCountry`
* `ProductCategory`
* `ProductColor`
* `Model`


### Data Pre-processing

**Data Loading**: 
Reading the Raw Dataset which originally existed as a CSV file into a Pandas Dataframe



__Task:__ Follow the appropriate steps in reading a CSV file into a pandas Dataframe, 


and  Read the data stored  in the csv file named:  `bikes` From your computer.


The resulting Dataframe should be named : `bikes_df`


~~~python
# solution
# solution 
import pandas as pd

bikes_df = pd.read_csv("C:/Users/James/Downloads/bikes.csv")
bikes_df
~~~


<img width="1108" height="467" alt="data pre processing" src="https://github.com/user-attachments/assets/056d1874-7654-41d6-ade4-82d9824a74b7" />


### Data Inspection and Cleaning

- **1. Check for Missing values**:

~~~python
# solution 
bikes_df.isna().any()

~~~


~~~python
# counting the number of missing values
Number_of_missing_values_per_column = bikes_df.isna().sum()
Number_of_missing_values_per_column
~~~


~~~python
# counting the number of rows

len(bikes_df)
~~~


~~~python
  # visualising the total number of the missing values

import matplotlib.pyplot as plt

Number_of_missing_values_per_column.plot(kind = "bar")
plt.plot()
~~~


- **2.Handling Missing values**:

~~~python
  # solution 
bikes_df_filled = bikes_df.fillna("Black")

bikes_df_filled
~~~



###  Check if any  columns is still containing  missing values from the:  bikes_df_filled

~~~python
# solution 

bikes_df_filled.isna().any()
~~~


- **3. Check for  Duplicates**:

~~~python
  # solution

# counting the total number of our datapoint
len(bikes_df)
~~~



- **4. Handling Duplicates**:

~~~python
  # solution
# dropping any duplicate if any exists

bikes_df.drop_duplicates(inplace = True)
~~~


~~~python
# recounting our data point again

len(bikes_df)

# this shows there was no duplicate in our data point
~~~



### Data Modification


~~~python
# generating some core metrics which were NOT provided from the dataset, which would be required for the purpose of the data analysis

# solution 

# (1) TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# (2) SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 


# (3) Profit : To be obtained by (SalesRevenue - TotalCostPrice)


bikes_df["Profit"] = bikes_df["SalesRevenue"]  - bikes_df["TotalCostPrice"]


# Displaying the result

bikes_df.head()
~~~



### Data Aggregation


~~~python
# Computing/ Aggregating the sales data to show Total Revenue by Customer , including their City, State and Country. 

# solution 
"CustomerName", "CustomerCity", "CustomerState", "CustomerCountry"	

bikes_df.groupby(["CustomerName", "CustomerCity", "CustomerState", "CustomerCountry"])["SalesRevenue"].sum()
~~~


~~~python
# adding their index number

Total_revenue_by_customer = bikes_df.groupby(["CustomerName", "CustomerCity", "CustomerState", "CustomerCountry"])["SalesRevenue"].sum().reset_index()
Total_revenue_by_customer
~~~



### Data Sorting/ Data Ranking

~~~python
# To Determine the Most Importat Metric: Top 10 highest revenue-generating customers 

# solution 

The_Top_10_customers = Total_revenue_by_customer.sort_values("SalesRevenue", ascending = False).head(10)
The_Top_10_customers
