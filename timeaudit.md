# Time Audit Foundry

## System Architecture
Local Tracking: A Python script logs system activity into a local SQLite database.
- Cloud Storage: Local data is pushed to an AWS S3 bucket as an intermediary.
- Browser Tracking: A Chrome Extension captures web usage and sends it to a cloud endpoint or S3.
- Analysis: Palantir Foundry runs a scheduled ingest to pull data from S3 for visualization.

## Implementation Steps
1. Local Data Capture
Script: Python monitors active windows or keystrokes.
Storage: Data is saved to activity.db via SQLite.
Sync: A cron job runs a script to upload the .db or .csv file to S3 using boto3.

2. Browser Extension
Capture: background.js tracks URL changes and time spent.
Export: Data is POSTed to an API or directly to an S3 bucket (using a signed URL).

3. Foundry Integration
Data Connection: Create an S3 Source in Foundry.
Sync: Set up a Data Connection Task to ingest files hourly.
Pipeline: Use Code Repositories to clean the raw data and build a "Time Audit" dashboard.


<table border="0">
 <tr>
    <td><b style="font-size:30px">Title</b></td>
    <td><b style="font-size:30px">Title 2</b></td>
 </tr>
 <tr>
    <td>
'''
Chrome Extension
        ↓
API Gateway
        ↓
Lambda
        ↓
Foundry Stream Ingest API
        ↓
Stream-backed Dataset
        ↓
Streaming Pipeline
'''
      
    </td>
    <td>Lorem ipsum ...</td>
 </tr>
</table>
