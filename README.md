# Healthcare Appointments No-Show Analysis
## Problem Statement
Healthcare clinics lose revenue and operational efficiency when patients miss scheduled appointments without notice. This analysis identifies no-show patterns across 110,000+ appointments to help administrators reduce missed appointments and improve resource allocation.
## Dataset
Source: Kaggle - Medical Appointment No Shows Dataset
Link: https://www.kaggle.com/datasets/joniarroba/noshowappointments
Size: 110,527 appointment records from Brazilian public hospitals
Key Columns:

appointment_id - Unique identifier for each appointment
patient_id - Unique patient identifier (allows tracking repeat patients)
clinic (neighbourhood) - Clinic location name
scheduled_date - When the appointment was booked
appointment_date - When the appointment was scheduled to occur
no_show - Whether patient attended (Yes = missed, No = attended)
gender - Patient gender (M/F)
age - Patient age in years
wait_days (calculated) - Days between booking and appointment date

## Tools Used 
* Primary Tools:

* Power BI Desktop - Dashboard creation, DAX measures, interactive visualizations
* Power Query (M language) - Data cleaning and transformation
* SQL - KPI calculations and data validation queries
* Python (pandas) - Alternative data cleaning pipeline for technical users.

## Steps Taken
### Data Cleaning
* Issues Identified:

* Column names had inconsistent formatting (ScheduledDay, AppointmentDay, No-show)

* Date fields stored as text strings instead of date type

* Invalid age values (negative ages and ages over 100)

* Missing clinic names (null values)

* 15 duplicate appointment IDs

* No calculated field for wait time between scheduling and appointment

### Actions Taken:

* Renamed all columns to snake_case format for consistency

* Converted scheduled_date and appointment_date from text to date type

* Removed records with ages outside 0-100 range (data quality filter)

* Filled null clinic names with "Unknown" placeholder

* Removed duplicate appointment_id records

* Created wait_days calculated column: appointment_date - scheduled_date

* Converted no_show from text (Yes/No) to binary (1/0) for calculations

* Final Clean Dataset: 110,512 valid records.


