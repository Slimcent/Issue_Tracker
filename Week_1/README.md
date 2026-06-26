# Week 1: Jira Issue Data Preparation for Apache Tika

## Project

This folder contains the Week 1 implementation for Assignment 3 of the Data Science for Software Engineering course.

The selected project is Apache Tika.

The goal of Week 1 is to prepare issue data for topic modeling. This includes reading the given issue list, downloading issue data from Apache Jira, preprocessing issue text, creating a vocabulary, and creating a document-term matrix.

## Folder Structure

```text
Week_1
¦
+-- data
¦   +-- raw
¦   ¦   +-- issues.xlsx
¦   +-- processed
¦   +-- outputs
¦
+-- scripts
¦   +-- 01_read_tika_issue_list.py
¦   +-- 02_download_tika_jira_issues.py
¦   +-- 03_preprocess_tika_text.py
¦   +-- 04_create_tika_vocabulary.py
¦   +-- 05_create_tika_document_term_matrix.py
¦
+-- notebooks
¦
+-- references
¦
+-- requirements.txt
+-- README.md
```

## Installation

Open PowerShell and go to the Week 1 folder:

```powershell
cd "C:\Users\DSSE\Week_1"
```

Create a Python virtual environment:

```powershell
python -m venv .venv
```

Activate the virtual environment:

```powershell
.\.venv\Scripts\activate
```

Install required packages:

```powershell
pip install -r requirements.txt
```

## Step 1: Read the Tika Issue List

Script:

```text
scripts\01_read_tika_issue_list.py
```

Run:

```powershell
python scripts\01_read_tika_issue_list.py
```

Purpose:

This script reads the Tika sheet from the Excel file and extracts the issue IDs and design-decision labels.

Input:

```text
data\raw\issues.xlsx
```

Expected output:

```text
data\processed\tika_issue_list.csv
```

The output contains:

```text
issue_key
existence
property
executive
```

## Step 2: Download Tika Issues from Apache Jira

Script:

```text
scripts\02_download_tika_jira_issues.py
```

Purpose:

This script will use the Apache Jira API to download full issue data for each Tika issue.

Expected output:

```text
data\raw\tika_jira_issues_raw.csv
```

## Step 3: Preprocess Issue Text

Script:

```text
scripts\03_preprocess_tika_text.py
```

Expected output:

```text
data\processed\tika_preprocessed_issues.csv
```

## Step 4: Create Vocabulary

Script:

```text
scripts\04_create_tika_vocabulary.py
```

Expected output:

```text
data\outputs\tika_vocabulary.csv
```

## Step 5: Create Document-Term Matrix

Script:

```text
scripts\05_create_tika_document_term_matrix.py
```

Expected outputs:

```text
data\outputs\tika_document_term_matrix.csv
data\outputs\tika_feature_names.csv
```

## Week 1 Outputs

```text
data\processed\tika_issue_list.csv
data\raw\tika_jira_issues_raw.csv
data\processed\tika_preprocessed_issues.csv
data\outputs\tika_vocabulary.csv
data\outputs\tika_document_term_matrix.csv
data\outputs\tika_feature_names.csv
```

## Notes

Only Apache Tika issues are used.

The issue summary and description are the main text fields used for preprocessing and topic modeling.

The design-decision labels are kept because they will be used later for co-occurrence analysis between topics and design-decision types.

The Jira metadata fields such as issue type, status, priority, comments, and attachments are stored because they will be used later to analyze issue characteristics.

---

## Completed Week 1 Results

The Week 1 pipeline was executed successfully for Apache Tika.

### Step 1: Tika Issue List

The Tika sheet was read from the provided Excel file.

Result:

```text
Number of Tika issues: 211
```

Output file:

```text
data\processed\tika_issue_list.csv
```

The cleaned issue list contains:

```text
issue_key
existence
property
executive
```

### Step 2: Jira Issue Download

The full issue data was downloaded from Apache Jira for all Tika issues.

Result:

```text
Downloaded issues: 211
```

Output files:

```text
data\raw\tika_jira_issues_raw.csv
data\raw\tika_jira_issues_raw.json
```

The downloaded data includes:

```text
issue_key
summary
description
issue_type
status
resolution
priority
labels
components
created
updated
resolved
votes
watchers
parent_key
comment_count
attachment_count
```

### Step 3: Text Preprocessing

The issue summary and description were concatenated and preprocessed.

Preprocessing included:

```text
lowercasing
URL removal
camel-case splitting
special-character removal
tokenization
stop-word removal
lemmatization
removal of very short tokens
```

Result:

```text
Number of issues: 211
Issues with zero tokens after preprocessing: 0
Average token count per issue: 69.78
```

Output file:

```text
data\processed\tika_preprocessed_issues.csv
```

### Step 4: Vocabulary Creation

A vocabulary was created from the preprocessed issue tokens.

Result:

```text
Number of issues: 211
Total number of tokens: 14,724
Number of unique tokens: 2,706
```

Top frequent tokens included:

```text
parser
file
metadata
type
text
content
test
code
document
version
pdf
user
server
stream
data
parse
class
java
vulnerability
cve
```

Output files:

```text
data\outputs\tika_vocabulary.csv
data\outputs\tika_top_50_tokens.csv
data\outputs\tika_vocabulary_summary.txt
```

### Step 5: Document-Term Matrix

A document-term matrix was created from the preprocessed text.

Result:

```text
Number of issues/documents: 211
Number of terms/features: 2,706
Matrix shape without metadata columns: 211 x 2706
Matrix shape with metadata columns: 211 x 2710
```

Output files:

```text
data\outputs\tika_document_term_matrix.csv
data\outputs\tika_feature_names.csv
data\outputs\tika_document_term_matrix_summary.txt
```

The first four columns of the matrix are metadata columns:

```text
issue_key
decision_existence
decision_property
decision_executive
```

The remaining columns are vocabulary tokens. Each cell contains the frequency of a token in a specific Tika issue.

## Week 1 Status

Week 1 is complete.

The generated document-term matrix will be used as input for LDA topic modeling in Week 2.
