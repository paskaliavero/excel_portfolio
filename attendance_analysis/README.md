# Attendance Analysis

## Project Overview

This project is an Excel-based analysis of a company's employee attendance data.

The goal is to process raw attendance records, calculate regular working hours and overtime, evaluate attendance consistency, and generate an employee-level attendance summary.

## Dataset

The dataset contains approximately 100,000 employee attendance records for August 2026.

The raw attendance data is organized into separate sheets based on employee division. Each division sheet contains the same attendance data structure.

### Raw Data Columns

| Column      | Description                  |
| ----------- | ---------------------------- |
| No. ID      | Employee ID                  |
| Nama        | Employee name                |
| Tanggal     | Attendance date              |
| Jam Kerja   | Scheduled working period     |
| Jam Masuk   | Scheduled clock-in time      |
| Jam Pulang  | Scheduled clock-out time     |
| Scan Masuk  | Actual clock-in time         |
| Scan Pulang | Actual clock-out time        |
| Riil        | Actual regular working hours |
| Lembur      | Actual overtime duration     |

### Working Hour Rules

* Regular working hours are **07:00–15:00**.
* Working time after **15:00** is classified as overtime.
* Sundays and holidays are treated as non-working days.
* Attendance on Sundays or holidays is tracked separately.

## Data Processing

Several helper columns are created in the raw data to transform and prepare the attendance records for analysis.

### Set Tanggal

The original `Tanggal` column is stored as text rather than a proper Excel date.

A helper column called `Set Tanggal` is used to convert the text value into an Excel date so that the data can be filtered and analyzed based on date ranges.

### Minggu/Libur

A helper column called `Minggu/Libur` identifies Sundays and holidays.

* `0` → Regular working day
* `1` → Sunday or holiday

This flag is used to distinguish regular working days from non-working days when calculating attendance.

### Hitung Lembur

The raw `Lembur` value is recorded in `HH:MM` format.

Overtime is converted into calculated hours based on the following rule:

* **00–49 minutes:** keep the current hour
* **50–59 minutes:** round up to the next hour

For example:

| Raw Overtime | Calculated Overtime |
| ------------ | ------------------: |
| 03:49        |                   3 |
| 03:50        |                   4 |
| 04:49        |                   4 |
| 04:50        |                   5 |

A helper column called `Hitung Lembur` is used to apply this calculation before the overtime hours are aggregated.

## Employee Summary

The processed data from each division is consolidated into a separate `REKAP` sheet.

The summary contains:

| Column      | Description                                                |
| ----------- | ---------------------------------------------------------- |
| No          | Row sequence                                               |
| NIK         | Employee ID                                                |
| Nama        | Employee name                                              |
| Divisi      | Employee division                                          |
| Harian      | Total actual regular working hours                         |
| Lemburan    | Total calculated overtime hours                            |
| Kerajinan 1 | Full attendance indicator for the first evaluation period  |
| Kerajinan 2 | Full attendance indicator for the second evaluation period |

### Harian

`Harian` represents the total regular working hours accumulated by each employee.

It is calculated by summing the `Riil` values for each employee across their attendance records.

### Lemburan

`Lemburan` represents the total calculated overtime hours accumulated by each employee.

The calculation uses the processed `Hitung Lembur` values from the raw attendance sheets.

### Kerajinan

`Kerajinan 1` and `Kerajinan 2` are binary attendance indicators.

* `1` → Employee attended every scheduled working day during the evaluation period
* `0` → Employee missed at least one scheduled working day during the evaluation period

The calculation is based on the employee's actual attendance on regular working days and excludes Sundays and holidays.

The two indicators represent two separate attendance evaluation periods.

## Analysis Performed

* Calculate total regular working hours for each employee
* Calculate total overtime hours for each employee
* Identify employees with full attendance during each evaluation period
* Track attendance on Sundays and holidays
* Aggregate attendance data across multiple employee divisions
* Generate an employee-level attendance summary

## Excel Concepts Used

* Data Cleaning
* Data Formatting
* Date and Time Functions
* Conditional Logic
* `IF`
* `SUMIF`
* `SUMIFS`
* `COUNTIFS`
* `NETWORKDAYS.INTL`
* `INDIRECT`
* Helper Columns
* Multi-sheet Data Aggregation

## Project Output

The final output is an Excel-based employee attendance report containing:

* Employee information
* Division
* Total regular working hours
* Total overtime hours
* Attendance consistency indicators
* Attendance on Sundays and holidays

## Project Preview

*Screenshots of the final Excel report will be added here.*

## Key Questions

* How many regular working hours did each employee accumulate?
* How many overtime hours did each employee accumulate?
* Which employees maintained full attendance during each evaluation period?
* How many employees worked on Sundays or holidays?
* How can attendance data from multiple divisions be consolidated into one employee-level report?
