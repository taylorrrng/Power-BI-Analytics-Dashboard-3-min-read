# Data Preparation & Modeling

This project tracks HR analytics for Atlas Labs using Power BI. The workflow includes data loading, modeling, measure creation, and building four interactive dashboards: Overview, Demographics, Performance Tracker, and Attrition.

**Steps:**

1. Import the following CSVs from the Datasets folder:
EducationLevel.csv, Employee.csv, PerformanceRating.csv, RatingLevel.csv, SatisfiedLevel.csv.

2. Prefix each table with Dim or Fact (e.g., DimEmployee, FactPerformanceRating).

3. Review and correct column data types (text, number, date) as per the metadata sheet.

4. Create a calculated table DimDate using DAX from DimDate.txt.

5. Build model relationships:

DimDate → FactPerformanceRating (active)

DimDate → DimEmployee (inactive)

DimEducationLevel → DimEmployee

DimSatisfiedLevel → FactPerformanceRating (active: EnvironmentSatisfaction)

DimRatingLevel → FactPerformanceRating (active: SelfRating)

6. Rename relationships and verify active/inactive links via Manage Relationships.

# Overview Dashboard

<img width="2000" height="1161" alt="Power BI - Cute 1" src="https://github.com/user-attachments/assets/d9fd452a-24dd-4d52-9e0e-dc86cafff2fe" />

**Steps:**

1. Rename Page 1 → Overview.

2. Create an empty table _Measures for KPIs.

3. Add measures:

TotalEmployees = Count of all employees.

ActiveEmployees / InactiveEmployees = Count by Attrition (“Yes” = inactive).

% Attrition Rate = (InactiveEmployees ÷ TotalEmployees), format as percentage (1 decimal).

4. Create card visuals for each KPI (Total, Active, Inactive, % Attrition Rate).

5. Add a stacked column chart for TotalEmployees by Date.

If blank, create TotalEmployeesDate using CALCULATE() + USERELATIONSHIP() to activate DimDate.

Replace the chart field with TotalEmployeesDate.

Add Attrition as a legend to split active vs inactive employees.

Set X-axis to Categorical and rename chart Employee Hiring Trends.

6. Create a clustered bar chart:

ActiveEmployees by Department → rename Active Employees by Department.

7. Create another visual:

ActiveEmployees by Department and JobRole → rename Active Employees by Department and Job Role.

# Demographics Dashboard

<img width="2000" height="1150" alt="Power BI - Cute 2" src="https://github.com/user-attachments/assets/6993b8a2-9994-431e-ad37-16816ef99c90" />

**Steps:**

1. Create new page → Demographics.

2. Add card visuals:

Minimum and maximum Age → rename to Youngest Employee and Oldest Employee (remove labels).

3. In Power Query, create a conditional column AgeBins with groups: <20, 20–29, 30–39, 40–49, 50+.

4. Add chart:

TotalEmployees by AgeBins, sort ascending → rename Employees by Age.

5. Duplicate and modify chart to show distribution by AgeBins and Gender → rename Employees by Age and Gender.

6. Add page-level filter for Attrition (active vs inactive).

7. Add new visuals:

Employees by MaritalStatus → rename Employees by Marital Status.

Create measure AverageSalary (average of salaries, 0 decimal, currency).

Visualize count and AverageSalary by Ethnicity → rename Employees by Ethnicity and Average Salary.

# Performance Tracker Dashboard

<img width="2000" height="1166" alt="Power BI - Cute 3" src="https://github.com/user-attachments/assets/2aadc434-354f-42f3-8ca6-25fbbefe2118" />

**Steps:**

1. Create new page → Performance Tracker.

2. Add calculated column FullName in DimEmployee combining FirstName & LastName.

3. Add slicer using FullName → rename to Select Employee, enable Single Select and Search.

4. Add card visuals:

Employee HireDate → rename Start Date.

5. Create measure LastReviewDate:

Displays last performance review for selected employee.

If blank, show “No review yet” (format mm/dd/yyyy).

Display as card Last Review.

6. Create measure NextReviewDate:

Adds 365 days to LastReviewDate (or HireDate if none).

Format mm/dd/yyyy, show as card Next Review.

7. In _Measures, add:

JobSatisfaction = MAX(FactPerformanceRating[JobSatisfaction])

EnvironmentSatisfaction, RelationshipSatisfaction, WorkLifeBalance → use USERELATIONSHIP() to activate connections to DimSatisfiedLevel.

8. Add visual(s) for EnvironmentSatisfaction, JobSatisfaction, WorkLifeBalance, and RelationshipSatisfaction by year.

9. Add measures: SelfRating, ManagerRating (using USERELATIONSHIP()).

10. Create chart(s) to show SelfRating and ManagerRating by year.

# Attrition Dashboard

<img width="2000" height="1130" alt="Power BI - Cute 4" src="https://github.com/user-attachments/assets/af8168e6-4bad-4c72-8972-b49561a9fa3a" />
