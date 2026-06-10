# Healthcare Appointments No-Show Analysis

## Project Overview
This project analyses 110,519 medical appointment records from a Brazilian public health system to identify what drives patient no-show behaviour and provide actionable, data-backed recommendations to reduce missed appointments.
The analysis moves through three stages: data cleaning in Python, KPI querying in SQL, and dashboard visualisation in Power BI.
Tools: Python (pandas), SQL (SQL Server), Power BI Desktop, Power Query, DAX

## Business Problem
Missed medical appointments are costly for healthcare providers and harmful to patients. Understanding which patients are most likely to miss their appointments, and why, allows clinics to act before the appointment is missed rather than after.
This project answers three core questions:

1. **What is the overall no-show rate and how does it vary across clinics?
2. **Which patient and scheduling factors predict no-show behaviour?
3. **What practical steps can reduce no-show rates?

## Dataset
**Source: Kaggle - Medical Appointment No Shows (Brazil, 2016)
**Raw records: 110,527 appointments across 81 clinics
**Columns used:
Patient_id: Unique patient identifier
Appointment_id: Unique appointment identifier
Gender: Patient gender (M/F)
Scheduled_date: Date the patient booked the appointment
Appointment_date: Date of the scheduled appointment
Age: Patient age
Clinic: Clinic name (neighbourhood)
Scholarship: Indicates if the patient receives welfare (1 = Yes)
Hipertension: Hypertension diagnosis flag
Diabetes: Diabetes diagnosis flag
Sms_received: Indicates if the patient received an SMS reminder (1 = Yes)
No_show: Target variable where 1 means the patient did not attend and 0 means the patient attended
Wait_days: Calculated days between booking and appointment.

## Data Cleaning Step
All cleaning was performed in Python using pandas. The notebook is included in this repository.

1. **Renamed all columns to snake_case for consistency with the SQL schema
2. **Converted scheduled_date and appointment_date from ISO string format to date objects
3. **Removed records where age was below 0 or above 100 (8 records removed)
4. **Filled null clinic values with "Unknown" (0 records affected in this dataset)
5. **Calculated wait_days as the difference between appointment_date and scheduled_date
6. **Converted the no_show column from text values ("Yes"/"No") to binary integers (1/0)
7. **Confirmed zero duplicate records in the dataset

Cleaned records: 110,519 rows saved to appointments_cleaned.csv

## Key Findings
1. **Overall No-Show Rate: 20.2%
More than 1 in 5 patients did not attend their scheduled appointment. That amounts to 22,319 missed appointments across the dataset.
2. **Wait Time is a Strong Predictor of No-Shows
Patients who attended their appointments waited an average of 8.8 days between booking and appointment. Patients who did not attend waited an average of 15.8 days. Appointments scheduled more than 14 days in advance carry a meaningfully higher risk of being missed.
3. **SMS Reminders Showed a Counterintuitive Pattern
Patients who received an SMS reminder had a no-show rate of 27.6%. Patients who received no reminder had a no-show rate of 16.7%. This does not mean reminders cause no-shows. The more likely explanation is that SMS reminders were sent more often to patients with longer wait times, and longer wait times independently predict no-shows. Further analysis controlling for wait time is needed before drawing conclusions about the effectiveness of the reminder system.
4. **Clinic-Level Variation is Significant
No-show rates vary widely across the 81 clinics in the dataset. The top 5 clinics by no-show volume account for a disproportionate share of missed appointments. Targeting interventions at these clinics would have the highest immediate impact.
5. **Gender Difference is Small but Consistent
Female patients showed a slightly higher attendance rate (78.8%) compared to male patients (77.4%). This gap is small and should not be the primary focus of any intervention.

## Assumptions
**A no_show value of 1 means the patient did not attend. A value of 0 means they attended.
**Appointments where wait_days equals 0 (booked and scheduled on the same day) are treated as valid.
**All records are from the local Brazilian timezone.
**Patients under 18 are included in the analysis as they appear as valid appointment holders in the dataset.
**The SMS reminder analysis does not establish causation. The correlation between SMS receipt and higher no-show rates is likely explained by confounding with wait time.

## Recommendations
1. **Target Long Wait Times First
Appointments booked more than 14 days in advance have a significantly higher no-show risk. Where possible, aim to keep scheduling windows under 7 days. For unavoidable long waits, implement a re-confirmation step at the 7-day mark.
2. **Redesign the SMS Reminder Strategy
The current SMS system appears to reach patients who are already high-risk due to long wait times, but is not reducing no-shows in that group. Consider sending reminders at two fixed points: 48 hours and 24 hours before the appointment, regardless of how far in advance it was booked.
3. **Prioritise the Top 5 Clinics by No-Show Volume
A small number of clinics account for a large share of missed appointments. Concentrated intervention in these clinics will deliver faster measurable results than a system-wide rollout.
4. **Consider Controlled Overbooking in High-Risk Slots
For time slots and clinics with historically high no-show rates, a 5 to 10 percent overbooking buffer can reduce wasted clinical capacity without significantly increasing patient wait times on the day.
5. **Collect Appointment Time Data More Consistently
The dataset includes an appointment_time field in the schema but this was not reliably captured in the raw data. Early morning appointments are reported in healthcare literature to have better attendance. Collecting this data consistently would allow the clinic to test and quantify that pattern.

## Files In This Repositoryy
- `appointments_cleaned.csv`: Cleaned and transformed dataset ready for SQL and Power BI
- `healthcare_no_show_cleaning.ipynb`: Python notebook: data loading, cleaning, and exploratory analysis
- `sql_kpi_queries.sql`: SQL Server: table schema and KPI queries
- `healthcare_dashboard.pbix`: Power BI report with interactive dashboard
- `README.md`: This documentation

## Tools Used
- **Power BI Desktop**: Dashboard development and DAX measures. Build an interactive dashboard that highlights key patterns and trends, enabling stakeholders to make data-driven decisions.
- **SQL**: Data querying and KPI calculations
- **Power Query**: Data cleaning and transformation
- **Data Preparation,Modeling & Exploratory Data Analysis Python (pandas)**: Alternative data cleaning pipeline and transform the raw dataset for analysis.

