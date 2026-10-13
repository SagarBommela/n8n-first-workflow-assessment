# Topic 9: Google Sheets Integration

## Overview

This project demonstrates how to integrate n8n with Google Sheets to append, read, and update spreadsheet rows.

The workflow simulates a new customer registration. It creates mock customer data, appends the customer to a Google spreadsheet with a Pending status, reads the customer records, and updates the matching customer's status to Verified.

**Workflow Name:** Topic 9 Google Sheets Integration Workflow

## Learning Objectives

- Configure Google Sheets credentials in n8n.
- Create a spreadsheet with the required column headers.
- Understand Spreadsheet IDs and sheet names.
- Append customer data to a Google Sheet.
- Read rows from a spreadsheet.
- Locate an existing row using a lookup column and value.
- Update a customer's status dynamically.
- Verify the workflow output and spreadsheet changes.

## Workflow Design

The workflow contains five nodes:

1. **When clicking "Test workflow"** – Starts the workflow manually.
2. **Mock Customer Data** – Creates sample customer information.
3. **Append Customer Row** – Adds the customer to Google Sheets.
4. **Read Customers** – Reads customer records from the spreadsheet.
5. **Update Customer Status** – Finds the relevant row and changes its status.

Workflow structure:

```text
Manual Trigger
      |
      v
Mock Customer Data
      |
      v
Append Customer Row
      |
      v
Read Customers
      |
      v
Update Customer Status
```

## Mock Customer Data

Configure the Edit Fields node named `Mock Customer Data` with these String fields:

| Field | Value |
|---|---|
| `customerName` | `Charlie Brown` |
| `customerEmail` | `charlie@example.com` |

Expected output:

```json
[
  {
    "customerName": "Charlie Brown",
    "customerEmail": "charlie@example.com"
  }
]
```

## Google Sheets Preparation

Create a Google spreadsheet named:

`N8N Test Spreadsheet`

In the first worksheet, create these headers in row 1:

| Cell | Header |
|---|---|
| A1 | Name |
| B1 | Email |
| C1 | Status |

The worksheet tab is commonly named `Sheet1` by default. If you rename it, use the new name in all Google Sheets nodes.

### Spreadsheet ID

Open the spreadsheet and copy its ID from the URL.

Example URL:

```text
https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit
```

In this example, `SPREADSHEET_ID` represents the long identifier between `/d/` and `/edit`. Use your actual ID, not the placeholder.

## Google Sheets Credentials

Configure Google Sheets credentials in n8n before testing the integration.

Depending on your environment, you may use OAuth2 or Service Account authentication.

- **OAuth2:** Connect the Google account that has access to the spreadsheet and complete the authorization flow.
- **Service Account:** Share the spreadsheet with the service account email and grant Editor access.

Use the credential configured for your environment. Do not include access tokens, private keys, client secrets, or other credentials in your repository or screenshots.

## Node 1: Manual Trigger

Use the `When clicking "Test workflow"` node to start the workflow manually during testing.

No additional configuration is required.

## Node 2: Mock Customer Data

Use an Edit Fields node renamed `Mock Customer Data`.

Add the following fields:

| Name | Type | Value |
|---|---|---|
| `customerName` | String | `Charlie Brown` |
| `customerEmail` | String | `charlie@example.com` |

Execute the node and confirm that both values appear in the output.

## Node 3: Append Customer Row

Add a Google Sheets node and rename it `Append Customer Row`.

Configure it as follows. Exact option labels can vary by n8n version.

| Setting | Value |
|---|---|
| Credential | Your Google Sheets credential |
| Resource | Row |
| Operation | Append / Append Row |
| Document | `N8N Test Spreadsheet` or its Spreadsheet ID |
| Sheet | `Sheet1` or your actual worksheet name |

Map the columns as follows:

| Google Sheets Column | Value |
|---|---|
| Name | `{{ $json.customerName }}` |
| Email | `{{ $json.customerEmail }}` |
| Status | `Pending` |

The Name and Email expressions dynamically use the mock input data. Status is a static value.

Expected spreadsheet row after appending:

| Name | Email | Status |
|---|---|---|
| Charlie Brown | charlie@example.com | Pending |

Execute the node and confirm that the new row appears in the spreadsheet.

**Important:** Every time you execute the append operation successfully, it may add another row. Check the spreadsheet before rerunning the workflow.

## Node 4: Read Customers

Add another Google Sheets node named `Read Customers`.

Configure it to read rows from the same spreadsheet and worksheet.

| Setting | Value |
|---|---|
| Credential | Your Google Sheets credential |
| Resource | Row |
| Operation | Read / Get Row(s), depending on your version |
| Document | `N8N Test Spreadsheet` or its Spreadsheet ID |
| Sheet | `Sheet1` or your actual worksheet name |

Execute the node and inspect its JSON output. Confirm that the customer record is present.

The output field names will typically match the spreadsheet headers, for example:

```json
{
  "Name": "Charlie Brown",
  "Email": "charlie@example.com",
  "Status": "Pending"
}
```

The actual output depends on your column names and Google Sheets node version.

## Node 5: Update Customer Status

Add a Google Sheets node named `Update Customer Status`.

Configure it to update a matching row.

| Setting | Value |
|---|---|
| Credential | Your Google Sheets credential |
| Resource | Row |
| Operation | Update / Update Row |
| Document | `N8N Test Spreadsheet` or its Spreadsheet ID |
| Sheet | `Sheet1` or your actual worksheet name |
| Lookup Column | `Email` |
| Lookup Value | Expression matching the email field in the incoming item |
| Field to Update | `Status` |
| New Status | `Verified` |

### Lookup Value expression

The assessment specifies:

```javascript
{{ $json.customerEmail }}
```

Use this expression if the incoming item contains a `customerEmail` property.

However, the preceding `Read Customers` node normally outputs spreadsheet columns such as `Name`, `Email`, and `Status`. If that is what you see in its output, use:

```javascript
{{ $json.Email }}
```

This matches the current item's Email value to the Google Sheets Email lookup column.

Always inspect the actual input to the Update Customer Status node and choose the expression that matches its field names.

## Expected Final Result

After a successful workflow execution, the matching spreadsheet row should show:

| Name | Email | Status |
|---|---|---|
| Charlie Brown | charlie@example.com | Verified |

The existing row should be updated rather than adding a second row for the same customer through the Update operation.

## Implementation Steps

1. Create the workflow named `Topic 9 Google Sheets Integration Workflow`.
2. Add the Manual Trigger node.
3. Add the Edit Fields node named `Mock Customer Data`.
4. Set `customerName` to `Charlie Brown` and `customerEmail` to `charlie@example.com`.
5. Create the `N8N Test Spreadsheet` spreadsheet.
6. Add the headers `Name`, `Email`, and `Status`.
7. Configure Google Sheets credentials in n8n.
8. Add and configure `Append Customer Row`.
9. Verify that the customer is appended with status `Pending`.
10. Add and configure `Read Customers`.
11. Inspect the output to identify the actual email field name.
12. Add and configure `Update Customer Status`.
13. Set the lookup column to Email and update Status to `Verified`.
14. Execute the workflow and inspect the spreadsheet.
15. Save the workflow and export the actual workflow JSON.



## Submission

- GitHub Repository:

https://github.com/SagarBommela/n8n-first-workflow-assessment

- Loom Video: 

https://www.loom.com/share/4209552414724e0ea314e669b083ef2d