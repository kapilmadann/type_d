SQL Time Dimension Table and Population Script 🗓️
-Kapil Madan
This T-SQL script creates a versatile time dimension table (dbo.TimeDimension) and a stored procedure (dbo.PopulateTimeDimension) to populate it. The table is designed for data warehousing and business intelligence, providing a rich set of calendar and fiscal date attributes. The script generates entries for an entire year based on a single input date.

Features
Creates a comprehensive time dimension table from scratch.

Includes both calendar and fiscal date attributes.

The fiscal year start month is easily configurable (defaults to April).

Uses a stored procedure for easy, repeatable population for any year.

Handles leap years automatically.

Prerequisites
Microsoft SQL Server

How to Use
Run the Script: Execute the entire SQL script in your SQL Server environment. This will:

Drop the TimeDimension table and PopulateTimeDimension procedure if they already exist.

Create the new TimeDimension table.

Create the PopulateTimeDimension stored procedure.

Populate the Table: Execute the stored procedure with any date from the year you wish to populate. The procedure will generate entries for the entire calendar year (January 1st to December 31st).

SQL

-- Example: Populate the table for the year 2020
EXEC dbo.PopulateTimeDimension '2020-07-14';

-- Example: Populate the table for the year 2025
EXEC dbo.PopulateTimeDimension '2025-01-01';
Verify the Data: Query the table to see the results.

SQL

-- View the first 10 records
SELECT TOP 10 * FROM dbo.TimeDimension ORDER BY [Date];
Script Components
Table: dbo.TimeDimension
This is the main dimension table where date attributes are stored. The primary key is the Date column.

Column	Data Type	Description
Date	DATE	The specific date (Primary Key).
KeyDate	DATE	A key for the date, same as Date.
CalendarDay	INT	The day of the month (1-31).
CalendarMonth	INT	The month number of the year (1-12).
CalendarMonthName	NVARCHAR(20)	The full name of the month (e.g., 'January').
CalendarQuarter	INT	The calendar quarter (1-4).
CalendarYear	INT	The calendar year (e.g., 2025).
DayName	NVARCHAR(20)	The full name of the weekday (e.g., 'Sunday').
DayNameShort	NVARCHAR(10)	The short name of the weekday (e.g., 'Sun').
DayNumberOfWeek	INT	The number of the day in the week (based on server settings).
DayNumberOfYear	INT	The day number of the year (1-366).
DaySuffix	NVARCHAR(5)	The day suffix (e.g., 'st', 'nd', 'rd', 'th').
WeekOfYear	INT	The week number of the year.
IsWeekend	BIT	A flag indicating if the day is a weekend (1 for True).
FiscalDay	INT	The day of the fiscal month.
FiscalMonth	INT	The fiscal month number (1-12).
FiscalMonthName	NVARCHAR(20)	The name of the month (calendar name).
FiscalQuarter	INT	The fiscal quarter (1-4).
FiscalYear	INT	The fiscal year.
FiscalYearPeriod	NVARCHAR(10)	A combined fiscal year and month period (YYYYMM).


Stored Procedure: dbo.PopulateTimeDimension
Purpose: To populate the dbo.TimeDimension table for a full year.

Parameter: @InputDate DATE - Any date within the target year. The procedure derives the start and end of the year from this date.

Logic: It uses a recursive Common Table Expression (CTE) to generate a list of all dates from January 1st to December 31st of the specified year. Then, it calculates and inserts all the calendar and fiscal attributes for each day into the TimeDimension table.

result :
<img width="1771" height="597" alt="Screenshot 2025-07-27 153941" src="https://github.com/user-attachments/assets/95bf3671-442e-418d-bd28-95119157b562" />
<img width="1438" height="547" alt="Screenshot 2025-07-27 153955" src="https://github.com/user-attachments/assets/17f0a684-d881-40e9-b854-76bdbb1b4fa4" />

