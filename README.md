Structured dataset of real mortgage underwriting conditions (Freddie Mac, Fannie Mae).

This repository serves as a QA and fallback dataset for the ConditionSnap system — an internal tool that automatically parses and classifies underwriting conditions directly from official Freddie Mac and Fannie Mae guides.

Purpose

Preserve verified manual copies of underwriting conditions for testing and validation.

Provide a fallback source if the live parsing API is unavailable or the website structure changes.

Enable automated comparison (diff) between parsed and manual versions.

Support regression tests for each Freddie/Fannie update release.

Structure

conditions-database/
│
├── FreddieMac/
│ ├── LPA/
│ │ ├── 4100_Uniform_Instruments/
│ │ ├── 4703_Property_Insurance/
│ │ ├── 5102_Underwriting/
│ │ └── 6401_Nondelivery/
│ └── keep/
│
├── FannieMae/ ← reserved for future import
│
└── validation_list.csv ← manual verification checklist

Each folder follows the Freddie/Fannie guide numbering convention:
{series}{topic}{chapter}.md
Example:
4703.2_Property_Insurance.md → Series 4000 / Topic 4700 / Chapter 4703.2

Workflow

Live Parser automatically fetches and structures data from official Freddie/Fannie websites.

If the parser fails or a section changes, the system loads the corresponding .md file from this repository.

The rules engine runs a diff check between the parsed and manual texts to flag discrepancies.

Results are tracked in validation_list.csv for auditing and regression purposes.

Validation List Format

validation_list.csv includes all manually verified or pending sections:

section_id	title	effective_date	last_checked	match_status
4101.1	The Mortgage Application	2025-08-06	2025-11-04	✅ OK
4703.2	Property Insurance	2024-06-01	2025-11-04	⚠️ Pending
6401.2	Penalty for Nondelivery	2025-09-03	2025-11-04	✅ OK
Notes

This dataset is not borrower-facing and contains only compliance-safe underwriting metadata.

All sections originate from public Freddie Mac and Fannie Mae Selling & Servicing Guides.

For automation logic, see the main ConditionSnap repository.

Maintained by: @sashadatsenko888-code
Last updated: November 2025
