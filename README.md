# Oddball Data Engineering Challenge - Customer Support Report
# Submitted by: Meagan McGourty, Applicant
To the reviewers, thank you for taking the time to read and recreate my work! I hope it's Odd enough :) 

# Overview
This project  processes contact center interaction data for a national organization. It ingests a January 2025 initial extract and February and March 2025 delta files, applies all changes chronologically across
four tables, and produces a summary report of interactions grouped by month, contact center, and department.

## Repository Structure
<img width="1211" height="1192" alt="image" src="https://github.com/user-attachments/assets/a6652037-95a8-4c01-bf4f-f71e4750391d" />

## Dependencies 
This project requires R (version 4.0 or higher, latest update recommended) and RStudio installed locally on your machine.
It is highly recommended to set your working directory now to wherever you deem fit to store your data. Please ensure that the directory you choose allows you to write csv. and pdf. outputs.
To install all required packages, please run the following in your RStudio console: 
```
install.packages(c("dplyr", "readr", "lubridate", "flextable", "tidyr", "styler"))

```
Additionally, rendering to PDF requires a LaTeX installation. If you do not already have LaTeX installed, you can install TinyTeX by running in your RStudio console: 
```
install.packages("tinytex")
tinytex::install_tinytex()

```

# How to Reproduce Results
Please follow these steps exactly to run the pipeline and reproduce all outputs from raw data. 

## Step 1: Clone the Repository
Download the repository onto your local machine. In your terminal or Git client, run: 
```
git clone https://github.com/meaganmcgourty-phd/OddballTechAssessment.git

```
Alternatively, you can download it as a ZIP file by clicking the green Code button on the repository page and selecting Download ZIP. Extract the ZIP to a location of your choice.

## STEP 2: Open the Project in R Studio
1. Open RStudio
2. Go to File -> New Project -> Existing Directory
3. Browse to the OddballTechAssessment folder and click Open

This sets your RStudio project root to the correct folder. Please ensure that you don't skip this step, or else your outputs will end up in Oz!

## STEP 3: Install Dependencies 
If you have not already installed the required packages, paste this into the RStudio console and press Enter: 
```
install.packages(c("dplyr", "readr", "lubridate", "flextable", "tidyr", "styler"))

```
If you still do not have a LaTeX distribution installed for PDF rendering, also run: 
```
install.packages("tinytex")
tinytex::install_tinytex()

```

## STEP 4: Update the Working Directory Path 
Open the .Rmd file in RStudio. Near the top of the file, in the setup-dirs chunk, you will see this line: 
```
project_path <- "~/Technical Challenges/recruiting-challenges-main/recruiting-challenges-main/data-engineer/customer-support-report"

```
Replace the path in quotes with the path to your local OddballTechAssessment foler. For example: 
```
project_path <- "~/Documents/OddballTechAssessment"

```
If you are unsure of your path, you can run getwd() in the RStudio console after completing Step 2. It will print the correct path for you to copy!

## STEP 5: Run Each Code Chunk or Knit the Document
You have a choice in how you would like to view the results. For a quick glance, you may simply run each chunk in order until you reach the end of the file, where all the flextables will be visible 
for you to analyze. If you would like a PDF output of the flextables, please run through the following steps in order: 
1. At the top of the file, where you see "output: github_document," change "github_document" to "pdf_document". Do not make any other changes!
2. With the .Rmd file open in R Studio, click the Knit button at the top of the editor (it has a small ball of yarn icon if you are unfamiliar).
3. Select Knit to PDF
4. RStudio will run the full pipeline from start to finish and produce a rendered PDF report.

## STEP 6: Check the Outputs
Once knitting is complete, the following files will be generated in the output/ folder: 
1. final_agents.csv; Final state of the agents table as of the end of March 2025.
2. final_contact_centers.csv; Final state of the contact centers table.
3. final_service_categories.csv; Final state of the service categories table.
4. final_interactions.csv; Complete interaction fact table with all changes applied.
5. support_report.csv; Aggregated report grouped by month, contact center, and department.


# Answers to Business Questions

## Q1: What were the total number of interactions handled by each contact center in Q1 2025?
See corresponding table. 
### Answer:
- Boston MA NE - 13 total interactions
- Atlanta GA SE - 8 total interactions
- Richmond VA E - 7 total interactions

Justification: Summing total_interactions from support_report.csv across all months and departments, grouped by contract_center_name, gives the Q1 totals in the respective table.
Boston MA NE handled the highest volume at 13 interactions across the quarter.

## Q2: Which month had the highest total interactions volume? 
See corresponding table. 
### Answer: February 2025
Justification: Summing total_interactions from support_report.csv grouped by month shows February as the peak month, which is consistent with the delta files. The February delta added the most
new interaction records as opposed to January and March, which reflects a higher volume of activity following the January baseline period.

## Q3: Which contact center had the longest average phone call duration?
See corresponding table.
### Answer: Boston MA NE had the longest average phone call duration at 12.7 minutes per call.

### Why might this be the case? 
Boston MA NE handles a high proportion of complex service categories (like IT, Operations, and Benefits), which likely require more agent interaction and longer lookup times compared to general 
inquiries like biling questions. With there being 11 calls across these categoires in Q1, Boston's higher average duration is likely a reflection of the nature of the reasons for the call, rather than inefficiency or 
different methods used by the center.

### Recommendation for Measuring Work Time More Accurately 
The current call_duration_minutes field measures total elapsed time from interaction_start to interaction_end, which includes any hold time, transfers, or wrap-ups. A more accurate measure of the true agent work time
might calculate the active handling window using interaction_start to agent_resolution_timestamp (the point at which the agent actually resolved the issue). The difference between agent_resolution_timestamp and interaction_end 
represents post-resolution time that might not reflect the agent's true efforts. Thus, excluding it could expose a clearer picture of how long agents are actively engaged per interaction.

This distinction is valuable for workforce management purposes, as call_duration_minutes is useful for understanding the caller's total experience, while the interaction_start to agent_resolution_timestamp window better isolates
the agent's active engagement time. Separating these two measures would allow the organization to track both caller experience and agent productivity independently, rather than conflating them into a sinlge metric.


# Notes
- All timestamps in the source data are in UTC. The pipeline converts them to Eastern Standard Time (America/New_York) before grouping by month to ensure interactions are attributed to the correct local date.
- Delta files do not exist for every table in every month. For example, contact_centers had no February delta, meaning no contact center records changed that month. The pipeline handles the missing delta files without error.
- Interactions referencing deleted dimension records (contact centers or service categories removed in a delta file) are retained in the report with their dimension values replaced by "Unknown" rather than being dropped,
  ensuring no interactions are lost from the final counts.

















