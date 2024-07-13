# Credit-Card-Financial-Report-2023
Credit Card Analysis for a year of 2023

Objective: 
To develop a comprehensive, real-time credit card weekly dashboard that provides stakeholders with detailed insights into key performance metrics and trends. This dashboard will enable stakeholders to monitor and analyze credit card operations effectively, identify emerging patterns, and make informed decisions. The objective includes integrating various data sources to ensure up-to-date information, offering customizable views to cater to user needs, and implementing advanced data visualization techniques to highlight critical data points and trends for proactive management.

Responsibilities: 
•	Designed and developed an interactive dashboard utilizing transaction and customer data extracted from an SQL database, ensuring real-time insights into credit card operations.
•	Optimized data processing and analysis workflows to monitor key performance metrics and trends, enhancing the efficiency and accuracy of data handling.
•	Integrated multiple data sources and implemented ETL processes to maintain up-to-date and reliable data within the dashboard.
•	Leveraged advanced data visualization techniques to present complex data in an easily understandable format, enabling quick identification of critical trends and patterns.
•	Conducted regular reviews and updates of the dashboard to incorporate new metrics and improve functionality based on stakeholder feedback.
•	Provided stakeholders with detailed, actionable insights derived from the dashboard, supporting strategic decision-making processes and operational improvements.
•	Collaborated with cross-functional teams to ensure the dashboard met business requirements and aligned with overall organizational goals.

Dax Queries Used: 

AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
 )


IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)


week_num2 = WEEKNUM('public cc_detail'[week_start_date])


Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]


Current_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]))) 


Previous_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))

