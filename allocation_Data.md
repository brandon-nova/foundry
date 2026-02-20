<table><tr><td>Finance Research</td></tr></table>

## Table of Contents
1. [Objective](#objective)
2. [Data Source](#data-source)
3. [Architecture](#architecture)
4. [Pipeline Design](#pipeline-design)
5. [Implementation Steps](#implementation-steps)
6. [Configuration Decisions](#configuration-decisions)
7. [Performance & Runtime](#performance--runtime)
8. [Validation & QA](#validation--qa)
9. [Troubleshooting](#troubleshooting)
---

## Objective
Research Paper: Finding if there is significant tilt towards domestic equities prior to elections 
Technical Objhective: Create a workshop or slate in Foundry demonstrating final results. 

## Data Source
I was given a flashdrive with 4ish GB of PDFs and other documents of pension fund data. 
Documents include:
    annual reports
    investment results summaries
    asset allocation disclosures
    policy asset mix statements
Source variability:
    multiple languages (primarily Japanese & English)
    mixed formatting styles
    tables embedded as images or text
Coverage spans multiple fiscal years

## Architecture
```plaintext
Media Set (PDFs)
    ↓
Text Extraction 
    ↓
Page-level segmentation
    ↓
Table detection & classification
    ↓
Structured extraction (LLM)
    ↓
Normalization & unit harmonization
    ↓
Ontology snapshot creation
    ↓
Workshop analytics & visualization
```

## Pipeline Design
Data extraction: Powershell to move all documents to root of folder, uploaded to foundry as media set

   <sup><sub>Initial direct uplaod failed even after cleaning</sub></sup>
   
Course I used to help do LLM transform/data cleaning: 
https://learn.palantir.com/speedrun-your-e2e-aip-workflow/1961888
#### OCR (Reading from handwriting) 
- decided to do RAW first and later will split and do OCR for items that did not work
- 
#### Explode Array with Position 
- turns each page into a row

#### Extract Many Struct Fields 
- seperate position [page number] and element [content]. We now have the below as output
<img width="3092" height="862" alt="image" src="https://github.com/user-attachments/assets/7877418c-b007-4a82-99bb-368a272717c0" />

#### Filter likely allocation pages
- keyword filtering (asset, allocation, equities, bonds)  
- numeric density detection  
- regex-based table heuristics  

#### LLM classification
- identifies pages containing allocation tables  
- filters narrative-only pages  

#### Structured allocation extraction
- extract asset class values  
- extract totals and currency  
- enforce numeric-only output  

#### Data cleaning & normalization
- remove symbols and formatting artifacts  
- standardize currency & numeric types  
- normalize percent vs monetary values  

#### Snapshot ID creation
- composite key: fund + fiscal year + page  
- ensures deterministic ontology instances  

#### Ontology write
- publish structured allocation snapshots  
- enable downstream analytics  



## Implementation Steps
- Standardized document ingestion into media set  
- Built page-level dataset for fine-grained analysis  
- Implemented heuristic filtering to reduce LLM load  
- Added classification transform to isolate allocation tables  
- Designed extraction prompt for structured financial data  
- Implemented normalization logic for mixed units  
- Created composite snapshot identifier  
- Published ontology object type (`FundAllocationSnapshot`)  
- Validated lineage from ontology object → page → source PDF  

## Configuration Decisions
- Added a classification step to get pages that were allocation tables 
- Switched LLM model after nano model failed to classify tables reliably  
- Structured output as a single ontology object per fund-year snapshot  
- Used snapshot write mode to maintain one authoritative record per period  
- Retined page number & document path for auditability  
- Chose classification-first strategy to reduce extraction cost  

## Performance & Runtime
- Page-level filtering reduced LLM processing volume by >80%  
- Classification step significantly lowered extraction token usage  
- Snapshot writes minimize duplication and improve ontology query performance  
- Pipeline scales linearly with document volume  
- Runtime bottlenecks primarily occur during LLM extraction and ontology publish
#### Was very slow, currently 12+ hours and pipeline not done, there was defenietly a way to do this more efficiency, though developer tier rate limit is a bottleneck 

## Validation & QA
- One row worked in preview so i deployed 

## Troubleshooting
### Classification returned NULL
Cause: lightweight model insufficient for complex page text  
Fix: switched to higher capability model  
### First attempt timed out 
Cause: I made the pipeline end to end and it was running tens of thousands of rows which each had a large content, wrote to an ontology, and I'm rate limited to 60-120k tokens per minute
Fix: I split the pipe into seperate cleaning and writing pipes. I also wrote to dataset instead of ontology. 

### Extraction returned NULL
Cause: pages lacked allocation tables or contained narrative tables  
Fix: improved classification filtering  

### Mixed formatting & OCR artifacts
Mitigation: numeric-only extraction + cleaning stage  

### Percent vs monetary values
Mitigation: post-processing logic using totals threshold  

### Large document ingestion failures
Workaround: flattened directory structure before upload

