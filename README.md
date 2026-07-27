# ZestyEats-End-to-End-Food-Delivery-Sales-Operational-Performance-Intelligence-Dashboard
An interactive Power BI analytics suite optimizing sales performance, delivery efficiency, and customer demographic insights.


# ZestyEats: Food Delivery Sales & Operational Performance Dashboard

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power_Query-M_Code-green?style=for-the-badge)

##  Executive Summary
**ZestyEats Analytics** is an end-to-end Power BI data solution built to evaluate food delivery operations, sales distribution, and delivery efficiency across multiple cities. The dashboard transforms raw relational order data into actionable operational insights for regional managers, driver managers, and restaurant partners.

---

##  Key Features & Pages

1. **KPI Overview Page (`KPIs`)**:
   * Executive summaries for **Total Sales**, **Average Order Value**, **Total Deliveries**, and **On-Time Delivery %**.
   * Category breakdowns for drinks, snacks, and order value segments.
2. **Sales & Customer Charts (`Charts`)**:
   * Order value distribution across food categories.
   * Customer demographic insights segmented by age group and gender.
   * Sales split by order type (*Meal*, *Snack*, *Drinks*, *Buffet*).
3. **Operations & Delivery Efficiency (`Performance`)**:
   * Analysis of traffic density vs. delivery driver rating.
   * Efficiency scatter plot evaluating driver age, vehicle condition, and delivery duration.
   * Restaurant performance treemap covering dine-in availability and cuisine types.
4. **Detailed Granular Matrix (`Matrix`)**:
   * Multilevel drill-down view by City, Age Group, and Gender.

---

##  Data Architecture & Modeling

The project employs a star schema model centered around the `Order_details` fact table, linked to normalized dimension tables:

* `Order_details` ↔ `User_details` (*Many-to-One via `Customer ID`*)
* `Order_details` ↔ `Restaurant_details` (*Many-to-One via `Restaurant ID`*)
* `Delivery_details` ↔ `Delivery_person_details` (*Many-to-One via `Delivery Person Id`*)
* `Order_details` ↔ `Delivery_details` (*One-to-One via `Order Id`*)

---

## 📊 Key DAX Measures Implemented

```dax
// Total Sales
Total Sales = SUM('Order_details'[Order Value])

// Average Order Value
Average Order Value = AVERAGE('Order_details'[Order Value])

// Total Deliveries
Total Deliveries = DISTINCTCOUNT('Order_details'[Order Id])

// On-time Delivery %
On-time Delivery % = 
DIVIDE(
    COUNTROWS(FILTER('Delivery_details', 'Delivery_details'[Time Taken (Min)] <= 30)),
    COUNTROWS('Delivery_details')
) * 100
