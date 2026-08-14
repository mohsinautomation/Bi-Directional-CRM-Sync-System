# Bi-Directional-CRM-Sync-System

Production-ready n8n automation for synchronizing data between Airtable and Google Sheets in both directions.

Architecture
Airtable → Google Sheets
Airtable Record Created/Updated
        ↓
Validate & Normalize
        ↓
Find Matching Google Sheets Row
        ↓
Update Existing Row / Create New Row
        ↓
Sync Logging
Google Sheets → Airtable
Google Sheets Row Created/Updated
        ↓
Detect New or Modified Row
        ↓
Validate & Normalize
        ↓
Check Airtable Record ID
        ↓
Find Existing Airtable Record
        ↓
Update / Create Airtable Record
        ↓
Write Airtable Record ID to Sheet
        ↓
Sync Logging
Features
🔄 Bi-directional Airtable ↔ Google Sheets synchronization
🔑 Airtable Record ID-based matching
🔎 Secondary matching using business identifiers such as Email
➕ Automatic record creation
✏️ Automatic record updates
🛡️ Duplicate prevention
🔁 Loop-prevention logic
✅ Data validation and normalization
📝 Sync activity logging
⚠️ Error handling
🔐 n8n credential-based authentication
📊 Separate Google Sheets tabs for Update, Create, and Sync Logs
Google Sheets Structure
Update

Stores records updated from Airtable.

Create

Stores newly created records from Airtable.

Log sync

Stores synchronization history:

Timestamp
Airtable Record ID
Action
Sync Status
Source
Name
Email
Workflow Files
Airtable-to-Google-Sheets.json
Google-Sheets-to-Airtable.json

Import both JSON workflows into n8n.

Required Configuration

Before activating the workflows, configure:

Airtable credentials
Google Sheets credentials
Airtable Base
Airtable Table
Google Spreadsheet
Google Sheets tabs
Field/column mappings

Do not commit API keys, personal access tokens, passwords, or other secrets to GitHub.

Sync Logic
Airtable → Google Sheets

If a matching Google Sheets row exists:

UPDATE

If no matching row exists:

CREATE
Google Sheets → Airtable

If an Airtable Record ID exists and the record is found:

UPDATE

If the Record ID is unavailable:

Search by secondary identifier
        ↓
Found → UPDATE
Not Found → CREATE

After creating a new Airtable record, its Record ID is written back to Google Sheets.

Error Handling

The workflows are designed to handle invalid data and API failures without stopping the entire synchronization process.

Examples:

Invalid email
Missing required fields
Invalid numeric values
Missing Airtable Record ID
Duplicate records
API errors
Temporary service failures
