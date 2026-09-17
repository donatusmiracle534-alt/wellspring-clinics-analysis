# Wellspring Clinics — Power BI Analysis

A Power BI project analyzing clinic operations data for Wellspring Clinics, a multi-site healthcare provider. The project covers data modeling, DAX, data cleaning, and dashboard design, resulting in an interactive report on patient visits, consultation fees, and staff experience.

## 📊 Dashboard Preview

The dashboard includes:
- **KPI cards** — Average Wait Time (35.25 min), Total Consultation Fee (₦2,853,000)
- **Diagnostics gauge** — 422 total diagnostics
- **Wait Time distribution** — spread of visit wait times (0–100 min)
- **Consultation Fee by Department** — trend line across 7 departments
- **Staff Experience funnel** — years of experience across 24 staff members
- **Slicers** — Department, Staff Name, Follow Up Required Medication (Yes/No)

## 🗂️ Data Model

The dataset consists of 4 related tables:

| Table | Key Field(s) | Purpose |
|---|---|---|
| `Clinics` | ClinicID | One record per clinic: name, state, type, date opened |
| `Patients` | PatientID | One record per patient: demographics, registration date |
| `Staff` | StaffID, ClinicID | One record per staff member, linked to their clinic |
| `Visits` | VisitID, PatientID, ClinicID, StaffID | One record per visit — the fact table connecting patients, clinics, and staff |

`Visits` is the fact table at the center of the model — it's the only table where `PatientID` and `ClinicID` appear together, which is why any "per clinic" or "per patient" visual should be built from it.

## 🧮 Key DAX

**FeeCategory** — classifies each visit's consultation fee:
```dax
FeeCategory = IF(Visits[ConsultationFee] >= 10000, "Expensive", "Affordable")
```

**Unique Patients per Clinic** — uses `DISTINCTCOUNT` rather than `COUNT`, since a patient can visit the same clinic more than once:
```dax
UniquePatients = DISTINCTCOUNT(Visits[PatientID])
```

## 🧹 Data Cleaning Decisions

- `ConsultationFee` was stored inconsistently as text (e.g. `₦3,000`, `NGN 3000`). Cleaned in Power Query — stripped currency symbols/commas, converted to numeric — before any fee logic was applied.
- 18 of 422 patient records had no wait time logged, though all other fields were complete. Rather than deleting these rows, they were flagged with a **"Not Recorded"** category to preserve the rest of the data.
- Renamed `Follow Up Required` → `Follow Up Required Medication` for dashboard clarity.

## 🔍 Key Findings

- **Immunization** had the highest total consultation fees (470,500) — **32.16% higher** than **Antenatal**, the lowest (356,000).
- Immunization alone accounted for **16.49%** of total consultation fees across all 7 departments.
- Total consultation fees ranged from 356,000 to 470,500 across departments.
- Total diagnostics: **422**, with an average wait time of **35.25 minutes**.
- Staff experience ranged from **1 to 25 years** across 24 staff members.

## ⚠️ Modeling Notes

An unconnected table in Model View (no relationship lines) means Power BI has no key linking it to the rest of the model. This doesn't cause an error — it silently breaks filtering: slicers from other tables won't affect that table's visuals, and vice versa. Every table in this model was checked for an active relationship to avoid this.

## 🛠️ Tools

- Microsoft Power BI Desktop (data modeling, DAX, dashboard)
- Power Query (data cleaning)

## 📄 Full Report

See [`Wellspring_Clinics_Project_Report.docx`](./Wellspring_Clinics_Project_Report.docx) / [`.pdf`](./Wellspring_Clinics_Project_Report.pdf) for the full write-up.
