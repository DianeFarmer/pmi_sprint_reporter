---
layout: default
---

# Introduction

The purpose of the Data Sprint module is to provide a structured framework for data stewards at Health Provider Organizations to become familiar with the technical requirements associated with submitting EHR data for the All of us Research Program **prior** to operating within the live production environment. It is also an opportunity for the Data Resource Core (DRC) to assess the technical capabilities and needs of participating sites. Your participation as a HPO will provide key insight towards the integration of this information into the All of Us Research Program. We provide here an overview of the components of the Data Sprint process:

 1. Overview
 1. [Data Model](data_model.md)
 1. [File Transfer Procedures](file_transfer_procedures.md)

# Data Sprint Goals

 1.  **Examine Load Process of Data**. The data sent will be transformed into a common data model to examine the data integrity of the EHR data sent. This will allow the DRC to better facilitate HPOs in transforming their data to the OMOP Common Data Model.
 1.  **Become Familiar with the OHDSI Vocabulary**. Based on the previous data sprint, an abridged version of the OMOP vocabulary was created. This data sprint will assess sites capabilities in converting their coded data into OMOP concept IDs.

# Timeline

Sprints are planned according to the schedule below. For each deliverable you are expected to submit records associated with a sample of 100 unique patient records. For example, records in `visit_occurrence` and `condition_occurrence` records should be linked to records in `person`.

| Week | End date | Deliverable |
| --- | --- | --- |
| 1 | 11/19/17 | Tables: person, visit_occurrence |
| 2 | 11/26/17 | Tables: condition_occurrence, procedure_occurrence |
| 3 | 12/03/17 | Tables: drug_exposure |
| 4 | 12/10/17 | Tables: measurement |
| 5 | 12/15/17 | Catch up / Review reports |

Data sprint submissions **must not** contain Protected Health Information (PHI) or Personal Identiable Information (PII). See the guides provided by the [U.S. Department of Health and Human Services](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification) and [U.S. Department of Labor](https://www.dol.gov/general/ppii) for more information.

# De-Identification

For this sprint, all dates will be de-identified and patient ids will be converted to a random number. All date fields will preserve the year, but set the month and day to Jan 1. For example, if an encounter occurs on March 12, 1985, the date will be de-identified to Jan 1, 1985. Also, all patients **greater than 80 years** of age should be removed from the submission.

# Clinical Case Example

This document will use the following case example to show how a patient’s record would be exported.

A 51-year-old (DOB: 1/2/1965), African American, non-Hispanic, male patient named John Doe visited the ED on 3/1/2106 at 3:12 a.m. with groin and abdominal pain. During the ED visit, it was determined that the patient had a kidney stone. Patient received metoclopramide 10 mg IV and morphine 6 mg IV at the ED. Subsequently, the patient had two outpatient office visits with a urologist on 3/15/2016 and 3/31/2016 with a primary diagnosis of calculus of ureter (ICD9:592.1) and was prescribed Flomax for three months. Following these visits, the patient had a lithotripsy preformed on 4/5/2016 with an ICD9 diagnosis code of 592.1 and procedure code of 98.51.

# Data and Format

Sites are asked to send data for 100 unique patients who had an encounter during the 2015 calendar year. Ideally, patients’ data will have a good mix of inpatient, outpatient and ED visits. Sites are asked to submit one file per table in CSV format with the table name as part of the file name. The file format must adhere to the Comma-Separated Values (CSV) file format (<https://tools.ietf.org/html/rfc4180>).

For data in a given table

Each record should be located on a separate line, delimited by a line break `[CRLF]`

For example:

    aaa,bbb,ccc[CRLF]

For each table, there should be a header line appearing before the data with the same format as normal record lines. This header should contain meaningful names (use the field names from the data request specifics section) corresponding to the fields in the file and should contain the same number of fields as the records in the rest of the file.

For example:

    field_name,field_name,field_name[CRLF]

After the header, each field in a record must be separated by commas

Each field should be enclosed in double quotes and empty fields will be empty quoted.

For example:

    "aaa","bbb","","ddd"[CRLF]

Each line should contain the same number of fields throughout the file. Spaces may be used as needed within the quotes are considered part of a field and should not be ignored. Spaces outside quotes will be ignored.

The last field in the record must not be followed by a comma

A double-quote appearing inside a field must be escaped by preceding it with another double quote

For example:

    "aaa","b""bb","ccc"

## Datetime

Fields of type `datetime` will be represented as a string for export files. The format will be in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations) where time is represented in UTC with time offset in the extended format `[hh]:[mm]:[ss]`. 

*NOTE: for datetimes where the time is not known, assume midnight (00:00 time). For example in Eastern time, UTC would be represented as `00:00:00-05:00`. Please refer to [this article](https://en.wikipedia.org/wiki/List_of_UTC_time_offsets) for a list of UTC offsets.*

[Proceed to Data Model >>](data_model.md)