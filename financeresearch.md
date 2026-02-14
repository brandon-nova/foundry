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

## Architecture
```plaintext
Media Set (PDFs)
    ↓
Document Extraction
    ↓
Chunking
    ↓
Embeddings / Summaries
    ↓
Semantic Search / Analysis
```

## Pipeline Design
Data extraction: Powershell to move all documents to root of folder, uploaded to foundry as media set

   <sup><sub>Initial direct uplaod failed even after cleaning</sub></sup>
   
Course I used to help do LLM transform/data cleaning: 
https://learn.palantir.com/speedrun-your-e2e-aip-workflow/1961888
1. OCR (Reading from handwriting) or raw?? I decided to do RAW first and later will split and do OCR for items that did not work 
2. Explode Array with Position (turns each page into a row)
3. Extract Many Struct Fields (seperate position [page number] and element [content]. We now have the below as output
<img width="3092" height="862" alt="image" src="https://github.com/user-attachments/assets/7877418c-b007-4a82-99bb-368a272717c0" />

4. 
5. 

## Implementation Steps

## Configuration Decisions

## Performance & Runtime

## Validation & QA

## Troubleshooting


