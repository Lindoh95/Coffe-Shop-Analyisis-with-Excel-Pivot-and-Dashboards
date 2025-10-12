# Retail-sales
Retail Analysis. Comparing Revenues over months, Time bucket and most selling product.

<br>I used snowfakles to  store and process my data. </br>
<br>i used snowfleakes to store my data in my create database,schema and tables.</br>
<br>within the snowflakes i used SQL Querries to extract, modelled and manipulate data.</br>
<br>after i convert my data into suitable format of EXCEL</br>

<br>Revenue per transaction 
SELECT transaction_id,
       transaction_qty*unit_price AS revenue  <br></br>
FROM sales.retail.bright_coffee</br>

<br> SELECT COUNT(DISTINCT store_id) AS number_of_shops
FROM sales.retail.bright_coffee;
</br>
<br>  calculate the revenue by store location 
SELECT store_location,
       SUM(transaction_qty*unit_price) AS revenue
FROM sales.retail.bright_coffee
GROUP BY store_location;
</br>
<br>
What time does the shop opens
SELECT MIN(transaction_time) openig_time
FROM sales.retail.bright_coffee;

-- What time does the shop close
SELECT MAX(transaction_time) closing_time
FROM sales.retail.bright_coffee</br>
<b>Populate time bucket of revenues across all store locations</b>
<br> SELECT product_category,
       SUM(transaction_qty*unit_price) AS revenue,
       store_location,
       transaction_date,
       transaction_time,
       CASE
            WHEN transaction_time BETWEEN '06:00:00' AND '11:59:59' THEN '01. Morning'
            WHEN transaction_time BETWEEN '12:00:00' AND '15:59:59' THEN '02. Aftenoon'
            WHEN transaction_time BETWEEN '16:00:00' AND '19:59:59' THEN '03. Evening'
            WHEN transaction_time >= '20:00:00'  THEN '04. Night'
        END AS time_bucket
FROM sales.retail.bright_coffee
WHERE transaction_date>'2023-05-01'
GROUP BY product_category,
         store_location,
         transaction_date,
         time_bucket,
         transaction_time
ORDER BY revenue DESC;</br>
<b> I built insights dashboars on excel </b>
<a href="https://github.com/Lindoh95/Retail-sales/blob/main/RETAIL1.PNG"> SCREEN 1</a>
<a href="https://github.com/Lindoh95/Retail-sales/blob/main/RETAIL2.PNG">SCREEN 2</a>


