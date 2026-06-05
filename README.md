# Healthcare Appointments No-Show Analysis

## Overview
This project analyzes 110,000+ medical appointment records to identify patterns in patient no-show behavior and provide actionable recommendations to reduce missed appointments.

## Data Quality Issues Identified
1. **Inconsistent date formatting**: Scheduled and appointment dates were stored as text
2. **Invalid age entries**: 2% of records had ages <0 or >100 (removed during cleaning)
3. **Missing clinic names**: 0.3% of records had null clinic values (marked as "Unknown")
4. **Duplicate appointment IDs**: 15 duplicate records removed
5. **Negative wait times**: Some appointments were scheduled after the appointment date (data entry errors)

## Key Findings
- **Overall no-show rate**: 20.2% (22,319 missed appointments)
- **Average wait time**: 10.2 days between scheduling and appointment
- **High-risk clinics**: 5 clinics have no-show rates >25%
- **Gender pattern**: Female patients have slightly higher attendance (78.8% vs 77.4%)

## Assumptions
- "No-show" = 1 means patient did not attend; 0 means they attended
- Appointments scheduled on the same day as the appointment date (wait_days = 0) are considered valid
- Pediatric appointments (age <18) are included in the analysis
- All date/times are in local Brazilian timezone

## Recommendations to Reduce No-Shows
1. **SMS/Email Reminders**: Implement automated reminders 48 hours and 24 hours before appointments
2. **Target High-Risk Clinics**: Prioritize intervention programs in the top 5 clinics with >25% no-show rates
3. **Reduce Wait Times**: Appointments scheduled >14 days out have 8% higher no-show rates; aim for <7-day scheduling
4. **Morning Slots**: Early morning appointments (before 10 AM) show 15% better attendance
5. **Overbooking Strategy**: Consider 5-10% overbooking in high-risk time slots to compensate for expected no-shows

## Tools Used
- **Power BI Desktop**: Dashboard development and DAX measures. Build an interactive dashboard that highlights key patterns and trends, enabling stakeholders to make data-driven decisions.
- **SQL**: Data querying and KPI calculations
- **Power Query**: Data cleaning and transformation
- **Data Preparation,Modeling & Exploratory Data Analysis Python (pandas)**: Alternative data cleaning pipeline and transform the raw dataset for analysis.

## Files Included
- `appointments_cleaned.csv`: Cleaned dataset
- `Project overview and Recommendation`: Project insight
- `sql_scripts.sql`: Table creation and KPI queries
- `healthcare_dashboard.pbix`: Power BI report file
- `README.md`: This documentation
