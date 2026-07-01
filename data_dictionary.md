# Data Dictionary — clean_online_retail.csv

This file describes the columns in the cleaned dataset exported from MiniProject_01.ipynb.
Starting from 541,909 raw rows, 19,408 were removed during cleaning, leaving 522,501 rows.

| Column | Type | Notes |
|--------|------|-------|
| invoice_no | str | cancellations (prefix 'C') already removed |
| description | str | whitespace stripped, converted to title case |
| quantity | int | positive values only, negatives and zeros dropped |
| invoice_date | datetime | originally stored as text, parsed to datetime |
| unit_price | float | positive values only in GBP, zeros and negatives dropped |
| customer_id | str | filled with 'UNKNOWN' where original CustomerID was missing |
| country | str | non-standard labels fixed (EIRE, RSA, Unspecified) |
| revenue | float | quantity × unit_price, calculated after cleaning |
| region | str | added by merging country against our region lookup table |
