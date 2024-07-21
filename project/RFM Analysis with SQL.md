# RFM Analysis with SQL

## what is RFM Analysis ?

RFM Analysis is a marketing technique for ranking and grouping customers from their recent transactions to identify the best customers and perform targeted marketing campaigns.

RFM analysis ranks each customer based on 3 factors:
- Recency. How recent was the customer's last purchase?
- Frequency. How often did this customer make a purchase in a given period?
- Monetary. How much money did the customer spend in a given period?
-------------------------------------------------------------------------------
**Dataset** : [online_retail](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
# Clean data

First of all, data set need to clean data for proper format
 

```sql

-- cleaning data


-- find missing value
select 
	count(*) - count(invoiceno) m_invoiceno,
	count(*) - count(stockcode) m_stockcode,
	count(*) - count(description) m_description, -- 1454,
	count(*) - count(quantity) m_quantity,
	count(*) - count(invoicedate) m_invoicedate,
	count(*) - count(unitprice) m_unitprice,
	count(*) - count(customerid) m_customerid, -- 135080,
	count(*) - count(country) m_country
from Online_retail;

-- drop missing value

delete from Online_retail
where customerid is null;

-- clean text string

-- count character
select 
	distinct length(invoiceno) char_invoiceno -- should have a 6-digit 
from Online_retail;

select 
 distinct length(stockcode) char_stockcode -- should have a 5-digit 
from Online_retail;

-- drop Canceled invoiceno

delete from Online_retail
where invoiceno like 'C%'

-- change pattern and data type 

select 
	case when length(stockcode) = 6 then left(stockcode,5)
		 when length(stockcode) = 5 then stockcode
		 else 'No Code'
	end as stockcode_new
from Online_retail;

update Online_retail
set stockcode = case when length(stockcode) = 6 then left(stockcode,5)
		 when length(stockcode) = 5 then stockcode
		 else 'No Code'
	end ;

alter table Online_retail
alter column invoiceno type integer USING invoiceno::integer;


-- cleannig numeric

-- chang type data
alter table Online_retail
alter column quantity type numeric USING quantity::integer;

-- explore numeric

select
	-- quantity
	avg(quantity) avg_quantity,
	min(quantity)  min_quantity, -- has nagative number
	max(quantity) max_quantity,
	stddev(quantity) stddev_quantity,
	-- unitprice
	avg(unitprice) avg_unitprice,
	min(unitprice) min_unitprice, -- has 0 
	max(unitprice)  max_unitprice, 
	stddev(unitprice) stddev_unitprice
from Online_retail


-- replacing 0 value with mean 

select
	avg(unitprice) -- 3.4 
from Online_retail;

update Online_retail
set unitprice = 3.4 
where unitprice = 0;

```
# RFM Analysis

```sql

-- Creating View to store data for later visualisations



-- Customer Segmentation using RFM 
create view RFM_Analysis as
with rfm as (
	select
		customerid,
		(select max(invoicedate)::date from Online_retail) - max(invoicedate)::date as recency,
		count(*) as frequency,
		sum(unitprice * quantity) as monetary
	from Online_retail
	group by customerid),
	
score as (
	select 
		customerid,
		monetary,
		frequency,
		recency,
		NTILE(5) over(order by recency asc) as r_score,
		NTILE(5) over(order by frequency) as f_score,
		NTILE(5) over(order by monetary) as m_score
	from rfm),
	
total_score as (
	select
		customerid,
		monetary,
		frequency,
		recency,
		concat(r_score, f_score, m_score)::numeric as rfm_score
	from score),

rfm_table as (
	select 
		customerid,
		monetary,
		frequency,
		recency,
		case 
			when rfm_score in (555, 554, 544, 545, 454, 455, 445) then 'Champion'
			when rfm_score in (543, 444, 435, 355, 354, 345, 344, 335) then 'Loyal Customers'
			when rfm_score in (553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323) then 'Potential Loyalist '
			when rfm_score in (512, 511, 422, 421, 412, 411, 311.) then 'New Customers'
			when rfm_score in (525, 524, 523, 522, 521, 515, 514, 513, 425,424, 413,414,415, 315, 314, 313) then 'Promising'
			when rfm_score in (535, 534, 443, 434, 343, 334, 325, 324) then 'Need Attention'
			when rfm_score in (155, 154, 144, 214,215,115, 114, 113) 	then 'Cannot Lose Them'
			when rfm_score in (331, 321, 312, 221, 213) then 'About To Sleep'
			when rfm_score in (255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124) then 'At Risk'
			when rfm_score in (332, 322, 231, 241, 251, 233, 232, 223, 222, 132, 123, 122, 212, 211) then 'Hibernating'
			else 'lost'
			end as segmentation
		from total_score)
		
select
	segmentation,
	round(avg(frequency),2) as avg_frequency,
	round(avg(recency),2) as avg_recency,
	count(*) as total_customer,
	round(sum(monetary),2) as total_monetary,
	round(avg(monetary),2) as avg_monetary
from rfm_table
group by segmentation
order by total_monetary desc

```
# Conclusion
Based on the analysis, we can categorize the segments into the following 5 groups:

1.High Potential Customers:
- Segments: Champions, Potential Loyalists, and Loyal customers.
- Marketing Strategy: Focus on retaining and engaging with these segments due to their significant contribution to total sales and profit.

2.Engagement Opportunities:
- Segments: New Customers and Promising.
- Marketing Strategy: Offer products or services that are more personalized for customers, and Implement strategies to increase engagement and order frequency to maximize their long-term value by referencing items they have previously purchased.

3.At-Risk Customers:
- Segment: At Risk.
- Marketing Strategy: Consider offering exclusive promotions for this group.
  
4.Reactivation Strategies:
- Segment: Hibernating Customers and Lost Customers.
- Marketing Strategy: Develop targeted reactivation strategies to re-engage with these customers and win back their business.
  
5.Small but Valuable:
- Segment: Cannot Lose Them.
- Marketing Strategy: Despite a small customer base, this segment contributes significantly. Strengthen loyalty through personalized strategies, such as offering a variety of promotion formats to users.
