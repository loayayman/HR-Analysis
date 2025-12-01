# 📊 HR Analysis

## 🌟 Introduction
The goal of this project is to analyze key Human Resources (HR) metrics for **Atlas Labs**.  
By exploring a dataset containing employee information, attrition rates, demographics, and performance data, this analysis aims to provide actionable insights.  
The dashboard visualizes trends in hiring, employee distribution, demographic breakdowns, and performance tracking to support **data-driven decision-making**.

---

## 🔗 Dataset
The dataset used in this analysis includes comprehensive HR information for employees at Atlas Labs.  

Key data points include:
* Total, Active, and Inactive employee counts  
* Employee hiring trends over time  
* Departmental breakdowns (Technology, Sales, HR, etc.)  
* Demographic details — age, gender, marital status, and education  
* Performance metrics — job satisfaction, relationship satisfaction, and manager ratings  
* Attrition data — overall rate, attrition by tenure, hire date, and travel frequency  

The dataset consists of several related tables:
| Table Name | Description |
|-------------|-------------|
| **DimDate** | Custom date table used for time-based calculations |
| **Employee** | Main employee information (ID, gender, department, job role, etc.) |
| **Education Level** | Mapping of education categories for employees |
| **Performance Rating** | Historical employee performance scores |
| **Rating Level** | Reference table defining performance categories |
| **Satisfaction Level** | Reference table for job and relationship satisfaction metrics |

---

## 🛠️ Requirements
This dashboard was created using **Microsoft Power BI Desktop**.  
To view, edit, or interact with the project file, you will need:

* [Microsoft Power BI Desktop](https://www.microsoft.com/en-us/download/details.aspx?id=58492)
* Power Query (for data cleaning and transformation)
* Basic knowledge of DAX (Data Analysis Expressions)

---

## 📸 Screenshots
Place your screenshots inside a folder named `/images` in the repo, then link them like this:

#### Dashboard Overview
<img width="1330" height="747" alt="1 Overview" src="https://github.com/user-attachments/assets/714726d9-905a-481e-8d78-ba741d382015" />

#### Demographics
<img width="1327" height="740" alt="2 Demographics" src="https://github.com/user-attachments/assets/d2907b1e-853d-4b0a-b58e-4076ca6eb704" />

#### Performance Tracker
<img width="1326" height="745" alt="3 Performance Tracker" src="https://github.com/user-attachments/assets/e726cbbf-663d-49ac-802b-04e67c2d9f55" />



#### Attrition 

<img width="1317" height="745" alt="4 Attrition" src="https://github.com/user-attachments/assets/1a0f5509-b529-4a66-84aa-4ebe82bc0d4a" />


---

## 📈 Key Insights
- High attrition among entry-level employees.  
- Employees with less than 3 years tenure show the highest turnover rate.  
- Technical departments have the largest headcount but lowest retention.  
- Strong positive correlation between performance rating and salary.  

---

Data Model
<img width="1133" height="726" alt="Data Model" src="https://github.com/user-attachments/assets/ed672224-ced9-4844-b2b4-1a0f30d89b9c" />


Star schema implementation with fact and dimension tables

---

## 📅 Custom Date Table (DimDate)
A custom date table was built in Power BI using DAX to enable advanced time intelligence calculations:

```DAX
DimDate = 
VAR _minYear = YEAR(MIN(DimEmployee[HireDate]))
VAR _maxYear = YEAR(MAX(DimEmployee[HireDate]))
VAR _fiscalStart = 4 

RETURN
ADDCOLUMNS(

    CALENDAR(

                DATE(_minYear,1,1),

                DATE(_maxYear,12,31)

),

"Year",YEAR([Date]),
"Year Start",DATE( YEAR([Date]),1,1),
"YearEnd",DATE( YEAR([Date]),12,31),
"MonthNumber",MONTH([Date]),
"MonthStart",DATE( YEAR([Date]), MONTH([Date]), 1),
"MonthEnd",EOMONTH([Date],0),
"DaysInMonth",DATEDIFF(DATE( YEAR([Date]), MONTH([Date]), 1),EOMONTH([Date],0),DAY)+1,
"YearMonthNumber",INT(FORMAT([Date],"YYYYMM")),
"YearMonthName",FORMAT([Date],"YYYY-MMM"),
"DayNumber",DAY([Date]),
"DayName",FORMAT([Date],"DDDD"),
"DayNameShort",FORMAT([Date],"DDD"),
"DayOfWeek",WEEKDAY([Date]),
"MonthName",FORMAT([Date],"MMMM"),
"MonthNameShort",FORMAT([Date],"MMM"),
"Quarter",QUARTER([Date]),
"QuarterName","Q"&FORMAT([Date],"Q"),
"YearQuarterNumber",INT(FORMAT([Date],"YYYYQ")),
"YearQuarterName",FORMAT([Date],"YYYY")&" Q"&FORMAT([Date],"Q"),
"QuarterStart",DATE( YEAR([Date]), (QUARTER([Date])*3)-2, 1),
"QuarterEnd",EOMONTH(DATE( YEAR([Date]), QUARTER([Date])*3, 1),0),
"WeekNumber",WEEKNUM([Date]),
"WeekStart", [Date]-WEEKDAY([Date])+1,
"WeekEnd",[Date]+7-WEEKDAY([Date]),
"FiscalYear",if(_fiscalStart=1,YEAR([Date]),YEAR([Date])+ QUOTIENT(MONTH([Date])+ (13-_fiscalStart),13)),
"FiscalQuarter",QUARTER( DATE( YEAR([Date]),MOD( MONTH([Date])+ (13-_fiscalStart) -1 ,12) +1,1) ),
"FiscalMonth",MOD( MONTH([Date])+ (13-_fiscalStart) -1 ,12) +1
)
```
👨‍💻 Author

Loay Ayman

GitHub: [Loay Ayman](https://github.com/loayayman)

LinkedIn: [Loay Ayman](https://www.linkedin.com/in/loayaymaan/)



