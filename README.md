# Oddball Data Engineering Challenge - Customer Support Report
# Submitted by: Meagan McGourty, Applicant
To the reviewers, thank you for taking the time to read and recreate my work! I hope it's Odd enough :) 

# Overview
This project  processes contact center interaction data for a national organization. It ingests a January 2025 initial extract and February and March 2025 delta files, applies all changes chronologically across
four tables, and produces a summary report of interactions grouped by month, contact center, and department.

## Repository Structure
<img width="834" height="742" alt="image" src="https://github.com/user-attachments/assets/54c4ca76-d066-4c3e-b67f-9eecc1248327" />


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


*** continue writing after referencing code file ***

















