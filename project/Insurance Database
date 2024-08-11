# Create Insurance Database 

**Table of Content**
- ER Diagram
- Create Table
- Insert Data
- Query Data



## ER Diagram

## SQL Code

```sql

-- Create Table

CREATE TABLE "Policy" (
  "PolicyID" integer PRIMARY KEY,
  "Insured" varchar,
  "Beneficiary" varchar,
  "Location" varchar,
  "Type" varchar,
  "Sum_insured" integer,
  "Premium" integer,
  "Start_date" date,
  "End_date" date,
  "EndorsementID" integer, -- Changed to integer
  "Agent_code" varchar
);

CREATE TABLE "Agent" (
  "Agent_code" varchar PRIMARY KEY,
  "Agent_name" varchar,
  "Agent_phone" varchar -- Changed to varchar to accommodate phone numbers with special characters
);

CREATE TABLE "Invoice" (
  "InvoiceID" integer PRIMARY KEY,
  "Invoice_date" date,
  "Insured" varchar,
  "Address" varchar,
  "Insurance_premium" integer,
  "Net_premium" integer,
  "Duty" integer,
  "Vat" integer,
  "PolicyID" integer,
  "EndorsementID" integer
);

CREATE TABLE "Customers" (
  "CustomerID" integer PRIMARY KEY,
  "Customer_name" varchar,
  "Address" varchar,
  "Customer_phone" varchar,
  "Email" varchar,
  "Agent_code" varchar
);

CREATE TABLE "Endorsement" (
  "EndorsementID" integer PRIMARY KEY,
  "EndorsementDate" date,
  "EndorsementType" varchar,
  "Description" varchar,
  "PolicyID" integer -- Added PolicyID as foreign key
);

CREATE TABLE "Claim" (
  "ClaimID" varchar PRIMARY KEY,
  "ClaimDate" date,
  "ClaimAmount" int,
  "ClaimStatus" varchar,
  "PolicyID" integer
);

ALTER TABLE "Policy" ADD FOREIGN KEY ("Agent_code") REFERENCES "Agent" ("Agent_code");

ALTER TABLE "Claim" ADD FOREIGN KEY ("PolicyID") REFERENCES "Policy" ("PolicyID");

ALTER TABLE "Customers" ADD FOREIGN KEY ("Agent_code") REFERENCES "Agent" ("Agent_code");

ALTER TABLE "Endorsement" ADD FOREIGN KEY ("PolicyID") REFERENCES "Policy" ("PolicyID");

ALTER TABLE "Invoice" ADD FOREIGN KEY ("EndorsementID") REFERENCES "Endorsement" ("EndorsementID");

ALTER TABLE "Invoice" ADD FOREIGN KEY ("PolicyID") REFERENCES "Policy" ("PolicyID");

```
# RFM Analysis

```sql

-- Insert Data
-- Insert data into Agent table
INSERT INTO "Agent" ("Agent_code", "Agent_name", "Agent_phone") VALUES
('AO1000', 'Prachaniyom Broker', 1234567890),
('ABC000', 'Risk EN Broker', 2345678901),
('CHA000', 'Chartri Insurance', 3456789012),
('MBT000', 'Howden Smile Broker', 4567890123),
('SPY000', 'Sripria Broker', 1212344567),
('NID000', 'NidNoi Consultant', 3451235433),
('SUA000', 'Surawong Broker', 8967299590),
('TPO000', 'TPO PO Consultant', 8890294389),
('BUI000', 'BangBon Inurance', 9767356723),
('ALA000', 'Ala Ala Broker', 5678901234);


-- Insert data into Customers table
INSERT INTO "Customers" ("CustomerID", "Customer_name", "Address", "Customer_phone", "Email", "Agent_code") VALUES
(1, 'Michael Green', '123 Elm Street', '555-1234', 'michael.green@example.com', 'AO1000'),
(2, 'Valentino Company', '456 Oak Avenue', '555-5678', 'Valentino.Company@example.com', 'ABC000'),
(3, 'Namo Company', '789 Pine Road', '555-9012', 'Namo.Company@example.com', 'CHA000'),
(4, 'Sarah Lee', '101 Maple Lane', '555-3456', 'sarah.lee@example.com', 'MBT000'),
(5, 'Emily Clark', '202 Birch Street', '555-7890', 'emily.clark@example.com', 'SPY000'),
(6, 'SkyLift Cranes Ltd.', '44 Oak Avenue', '552-3056', 'SkyLift.Cranes@example.com', 'NID000'),
(7, 'Eagle Lift Cranes', '789 Pine Road', '552-3496', 'Eagle.Cranes@example.com', 'SUA000'),
(8, 'Atlas Industrial Cranes', '203 Birch Street', '589-2456', 'Atlas.Cranes@example.com', 'TPO000'),
(9, 'Ten Lee', '102 Maple Lane', '555-9956', 'Ten.lee@example.com', 'BUI000'),
(10, 'Kim Yeonjun', '77 Timmy Street', '555-7756', 'Yeonjun.Kim@example.com', 'ALA000'),
(11, 'John Doe', '123 Elm Street', '555-1134', 'john.doe@example.com', 'AO1000'),
(12, 'Jane Smith', '457 Oak Avenue', '555-5278', 'jane.smith@example.com', 'ABC000'),
(13, 'Sam Brown', '78 Mine Road', '555-8700', 'sam.brown@example.com', 'CHA000'),
(14, 'Lisa White', '321 Birch Lane', '555-4321', 'lisa.white@example.com', 'MBT000'),
(15, 'ABC Construction Co.', '77 Timmy Street', '555-7823', 'info@abcconstruction.com', 'SPY000'),
(16, 'BuildRight Contractors', '456 Oak Avenue', '555-9342', 'contact@buildright.com', 'NID000'),
(17, 'SafeBuild Inc.', '785 Pine Road', '555-1048', 'support@safebuild.com', 'SUA000'),
(18, 'Elite Contractors LLC', '321 Birch Lane', '555-6739', 'service@elitecontractors.com', 'TPO000'),
(19, 'Jennie Kim', '45 Oak Avenue', '555-1174', 'Lisa.kim@example.com', 'CHA000'),
(20, 'Lisa J', '78 Mine Road', '555-5978', 'Lisa.J@example.com', 'SPY000');


-- Insert data into Policy table
INSERT INTO "Policy" ("PolicyID", "Insured", "Beneficiary","Location","Type", "Sum_insured", "Premium", "Start_date", "End_date", "Agent_code") VALUES
(2408520001, 'Michael Green', NULL, 'Pancake Cafe 123 Elm Street', 'LB', 100000, 3500,'2024-08-01','2025-08-01','AO1000'),
(2408520002, 'Michael Green', NULL, 'Micheal Restaurant 124 Elm Street', 'LB', 100000, 3500,'2024-08-01','2025-08-01','AO1000'),
(2408700001, 'Valentino Company', NULL, 'ten town building 120 street', 'CW', 1000000, 10000,'2024-08-03','2024-10-03','ABC000'),
(2408700002, 'Namo Company', NULL, 'gang bridge lane rod', 'CW',20000000, 45000,'2024-08-11','2024-11-11','CHA000'),
(2408520003, 'Sarah Lee', NULL, 'Sarah baber titi road', 'LB', 100000, 3500,'2024-08-12','2025-08-12','MBT000'),
(2408520004, 'Juice Company', 'Emily Clark', 'Juice Event 34 hall 12 street', 'LB', 1000000, 15000,'2024-08-14','2024-08-21','SPY000'),
(2408520005, 'SkyLift Cranes Ltd', NULL, 'THAILAND except dangerous zone', 'LB', 100000, 3500,'2024-08-20','2025-08-20','NID000'),
(2408740001, 'SkyLift Cranes Ltd', NULL, 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-08-20','2025-08-20','NID000'),
(2408740002, 'Eagle Lift Cranes', 'Michel kim', 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-08-22','2025-08-22','SUA000'),
(2408520006, 'Atlas Industrial Cranes', NULL, 'THAILAND except dangerous zone', 'LB', 100000, 3500,'2024-08-22','2025-08-22','TPO000'),
(2408740003, 'Atlas Industrial Cranes', NULL, 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-08-22','2025-08-22','TPO000'),
(2408520007, 'Ten Lee', NULL, 'Ten Bar 12 road', 'LB', 1000000, 10000,'2024-08-25','2025-08-25','BUI000'),
(2408520008, 'Ten Lee', NULL, 'Ten Reataurant 12 road', 'LB', 1000000, 10000,'2024-08-25','2025-08-25','BUI000'),
(2408520009, 'Ten Lee', NULL, 'Ten Bar 20 road', 'LB', 1000000, 10000,'2024-08-25','2025-08-25','BUI000'),
(2408740004, 'Kim Yeonjun', 'Crane leasing company', 'THAILAND except dangerous zone', 'CPM', 100000, 10000,'2024-08-25','2025-08-25','ALA000'),
(2408740005, 'Kim Yeonjun', 'Crane leasing company', 'THAILAND except dangerous zone', 'CPM', 100000, 10000,'2024-08-25','2025-08-25','ALA000'),
(2409520001, 'John Doe', NULL, 'JOHN APARTMENT 21 red lane', 'LB', 100000, 30000,'2024-09-03','2025-09-03','AO1000'),
(2409600001, 'John Doe', NULL, 'JOHN GAS 20 black lane', 'LO', 100000, 5000,'2024-09-03','2025-09-03','AO1000'),
(2409520002, 'Jane Smith', NULL, 'Smith Condo khao sarn road', 'LB', 1000000, 10000,'2024-09-05','2025-09-05','ABC000'),
(2409700001, 'Jane Smith', NULL, 'Smith Condo khao tom road', 'CW', 4500000, 85000,'2024-09-05','2025-09-05','ABC000'),
(2409520003, 'Jane Smith', NULL, 'Smith Cafe khao sarn road', 'LB', 1000000, 6000,'2024-09-05','2025-09-05','ABC000'),
(2409740001, 'Sam Brown', 'Nida leasing', 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-09-09','2025-09-09','CHA000'),
(2409740002, 'Sam Brown', 'Nida leasing', 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-09-09','2025-09-09','CHA000'),
(2409600002, 'Lisa White', NULL, 'White GAS Timmy Lane', 'LO', 100000, 5000,'2024-09-12','2025-09-12','MBT000'),
(2409700002, 'ABC Construction Co', NULL, 'The mall 2 zen road', 'CW',20000000, 75000,'2024-09-20','2026-07-20','SPY000'),
(2409700003, 'BuildRight Contractors', NULL, 'Sang Bridge long road', 'CW',20000000, 45000,'2024-09-20','2025-01-20','NID000'),
(2409700004, 'Elite Contractors LLC', NULL, 'Kong Town 25 road', 'CW', 1000000, 10000,'2024-09-21','2025-04-21','TPO000'),
(2409520004, 'SafeBuild Inc.', NULL, 'THAILAND except dangerous zone', 'LB', 100000, 3500,'2024-09-25','2025-09-25','SUA000'),
(2409740003, 'SafeBuild Inc.', NULL, 'THAILAND except dangerous zone', 'CPM', 1000000, 10000,'2024-09-25','2025-09-25','SUA000'),
(2409600003, 'Jennie Kim', NULL, 'Jennie Gas 45 Oak Avenue', 'LO', 100000, 5000,'2024-09-26','2025-09-26','CHA000'),
(2409520005, 'Jennie Kim', NULL, 'Jennie Reataurant 45 Oak Avenue', 'LB', 1000000, 10000,'2024-09-26','2025-09-26','CHA000'),
(2409520006, 'Lisa J', NULL, 'Lisa Reataurant 78 Mine Road', 'LB', 1000000, 10000,'2024-09-26','2025-09-26','SPY000');


-- Insert data into Endorsement table
INSERT INTO "Endorsement" ("EndorsementID", "EndorsementDate", "EndorsementType", "Description", "PolicyID") VALUES
(24001, '2024-08-05', 'D/V', 'Edit receipt address', 2408520002),
(24002, '2024-08-10', 'A/V', 'Increase sum insured 2000000', 2408740001),
(24003, '2024-08-20', 'A/B', 'Increase sum insured 1000000', 2408520006),
(24004, '2024-08-20', 'A/V', 'Extend the period 10 days', 2408520004),
(24005, '2024-08-23', 'D/V', 'Edit Beneficiary', 2408520005),
(24006, '2024-09-10', 'D/V', 'Edit Beneficiary', 2409600001),
(24007, '2024-09-11', 'D/V', 'Edit receipt address', 2409520002),
(24008, '2024-10-25', 'A/V', 'Extend the period 2 months', 2409700003);


-- Insert data into Invoice table
INSERT INTO "Invoice" ("InvoiceID", "Invoice_date", "Insured", "Address", "Insurance_premium", "Net_premium", "Duty", "Vat", "PolicyID", "EndorsementID") VALUES
(001, '2024-08-01', 'Michael Green', '123 Elm Street',3898, 3500 , 140, 258, 2408520001, NULL),
(002, '2024-08-01', 'Michael Green', '124 Elm Street',3898, 3500 , 140, 258, 2408520002, NULL),
(003, '2024-08-03', 'Valentino Company', '456 Oak Avenue', 10743,10000, 40, 703, 2408700001, NULL),
(004, '2024-08-05', 'Michael Green', '123 Elm Street', 0, 0, 0, 0,2408520002, 24001),
(005, '2024-08-05', 'Namo Company', '789 Pine Road',48342, 45000, 180, 3162, 2408700002, NULL),
(006, '2024-08-05', 'Sarah Lee', '101 Maple Lane',3898, 3500 , 140, 258, 2408520003, NULL),
(007, '2024-08-05', 'Emily Clark', '202 Birch Street',16114, 15000 , 60, 1054, 2408520004, NULL),
(008, '2024-08-06', 'SkyLift Cranes Ltd', '44 Oak Avenue',3898, 3500 , 140, 258, 2408520005, NULL),
(009, '2024-08-06', 'SkyLift Cranes Ltd', '44 Oak Avenue',10743,10000, 40, 703, 2408740001, NULL),
(010, '2024-08-07', 'Eagle Lift Cranes', '789 Pine Road',10743,10000, 40, 703, 2408740002, NULL),
(011, '2024-08-10', 'SkyLift Cranes Ltd', '44 Oak Avenue',16114, 15000 , 60, 1054, 2408740001, 24002),
(012, '2024-08-15', 'Atlas Industrial Cranes', '203 Birch Street',3898, 3500 , 140, 258, 2408520006, NULL),
(013, '2024-08-15', 'Atlas Industrial Cranes', '203 Birch Street',10743,10000, 40, 703, 2408740003, NULL),
(014, '2024-08-17', 'Ten Lee', '102 Maple Lane',10743,10000, 40, 703, 2408520007, NULL),
(015, '2024-08-17', 'Ten Lee', '102 Maple Lane',10743,10000, 40, 703, 2408520008, NULL),
(016, '2024-08-17', 'Ten Lee', '102 Maple Lane',10743,10000, 40, 703, 2408520009, NULL),
(017, '2024-08-20', 'Ten Lee', '102 Maple Lane',10743,10000, 40, 703, 2408520006, 24003),
(018, '2024-08-20', 'Emily Clark', '202 Birch Street',7520,7000, 28, 492, 2408520004, 24004),
(019, '2024-08-21', 'Kim Yeonjun', '77 Timmy Street',10743,10000, 40, 703, 2408740004, NULL),
(020, '2024-08-21', 'Kim Yeonjun', '77 Timmy Street',10743,10000, 40, 703, 2408740005, NULL),
(021, '2024-08-23', 'Kim Yeonjun', '77 Timmy Street',0,0, 0, 0, 2408740005, 24005),
(022, '2024-09-03', 'John Doe', '123 Elm Street',32228,30000, 120, 2108, 2409520001, NULL),
(023, '2024-09-03', 'John Doe', '123 Elm Street',5371,5000, 20, 351, 2409600001, NULL),
(024, '2024-09-05', 'Jane Smith', '457 Oak Avenue',10743,10000, 40, 703, 2409520002, NULL),
(025, '2024-09-05', 'Jane Smith', '457 Oak Avenue',91314,85000, 340, 5974, 2409700001, NULL),
(026, '2024-09-05', 'Jane Smith', '457 Oak Avenue',6446,6000, 24, 422, 2409520003, NULL),
(027, '2024-09-09', 'Sam Brown', '78 Mine Road',10743,10000, 40, 703, 2409740001, NULL),
(028, '2024-09-09', 'Sam Brown', '78 Mine Road',10743,10000, 40, 703, 2409740002, NULL),
(029, '2024-09-10', 'John Doe', '123 Elm Street',0,0, 0, 0, 2409600001, 24006),
(030, '2024-09-11', 'Jane Smith', 'Smith Condo khao sarn road',0,0, 0, 0, 2409520002, 24007),
(031, '2024-09-13', 'Lisa White', '321 Birch Lane',5371,5000, 20, 351, 2409600002, NULL),
(032, '2024-09-17', 'ABC Construction Co', '77 Timmy Street',80571,75000, 300, 5271, 2409700002, NULL),
(033, '2024-09-20', 'BuildRight Contractors', '456 Oak Avenue',48342, 45000, 180, 3162, 2409700003, NULL),
(034, '2024-09-20', 'Elite Contractors LLC', '321 Birch Lane', 10743,10000, 40, 703, 2409700004, NULL),
(035, '2024-09-20', 'BuildRight Contractors', '456 Oak Avenue',16114, 15000, 60, 1054, 2409700003, 24008),
(036, '2024-09-22', 'SafeBuild Inc.', '785 Pine Road',3898, 3500 , 140, 258, 2408520004, NULL),
(037, '2024-09-22', 'SafeBuild Inc.', '785 Pine Road',10743,10000, 40, 703, 2409740003, NULL),
(038, '2024-09-23', 'Jennie Kim', '45 Oak Avenue',5371,5000, 20, 351, 2409600003, NULL),
(039, '2024-09-23', 'Jennie Kim', '45 Oak Avenue',10743,10000, 40, 703, 2409520005, NULL),
(040, '2024-09-23', 'Lisa J', '78 Mine Road',10743,10000, 40, 703, 2409520006, NULL);

-- Insert data into Claim table
INSERT INTO "Claim" ("ClaimID", "ClaimDate", "ClaimAmount", "ClaimStatus", "PolicyID", "claim_reason") VALUES
('C001', '2024-08-19', 1500, 'Approved', 2408520004,'Third person hit by elevator'),
('C002', '2024-09-01', 3000, 'Approved', 2408740003,'Mechanical Failures'),
('C003', '2024-09-20', 500, 'Approved', 2408520002,'Third person hit by elevator'),
('C004', '2024-09-23', 600, 'Approved', 2409740002,'The Crane toppled over'),
('C005', '2024-10-05', 5000, 'Approved', 2409700002,'Mechanical Failures'),
('C006', '2024-10-11', 1500, 'Approved', 2408740003,'The Crane toppled over'),
('C007', '2024-11-24', 3000, 'Approved', 2408740004,'The Crane toppled over'),
('C008', '2024-11-25', 10000, 'Approved', 2409700001,'Flood');

```
```sql
--Query Data
-- Which insurance type sold the most in August?

SELECT 
    "Type",
    COUNT(*) AS count,
    SUM("Net_premium")
FROM public."Policy"
LEFT JOIN public."Invoice" ON public."Policy"."PolicyID" = public."Invoice"."PolicyID"
WHERE EXTRACT(MONTH FROM "Invoice_date") = 8
GROUP BY "Type"
ORDER BY count DESC
LIMIT 1;

-- Which insurance type sold the most in September?
SELECT 
    "Type",
    COUNT(*) AS count,
    SUM("Net_premium")
FROM public."Policy"
LEFT JOIN public."Invoice" ON public."Policy"."PolicyID" = public."Invoice"."PolicyID"
WHERE EXTRACT(MONTH FROM "Invoice_date") = 9
GROUP BY "Type"
ORDER BY count DESC
LIMIT 1;

-- Monthly income in August
select 
	sum("Net_premium") - sum("ClaimAmount") As Monthly
from public."Invoice"
inner join public."Claim" on public."Invoice"."PolicyID" = public."Claim"."PolicyID"
WHERE EXTRACT(MONTH FROM "Invoice_date") = 8


-- Monthly income in September
select 
	sum("Net_premium") - sum("ClaimAmount") As Monthly
from public."Invoice"
inner join public."Claim" on public."Invoice"."PolicyID" = public."Claim"."PolicyID"
WHERE EXTRACT(MONTH FROM "Invoice_date") = 9

-- Endorsement in August
select *
from public."Endorsement"
WHERE EXTRACT(MONTH FROM "EndorsementDate") = 8

-- Endorsement in September
select *
from public."Endorsement"
WHERE EXTRACT(MONTH FROM "EndorsementDate") = 9

-- Which broker has the highest sales
SELECT 
    A."Agent_code",
    A."Agent_name",
    SUM(I."Net_premium") AS total_sales
FROM public."Agent" A
JOIN public."Policy" P ON A."Agent_code" = P."Agent_code"
JOIN public."Invoice" I ON P."PolicyID" = I."PolicyID"
GROUP BY A."Agent_code", A."Agent_name"
ORDER BY total_sales DESC
LIMIT 1;
```
