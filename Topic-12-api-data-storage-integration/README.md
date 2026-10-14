# Topic 12: API & Data Storage Integration

## 1. Overview

In this topic, I learned how to connect an API with Google Sheets using n8n. I retrieved sample user details from a public API and stored them in a Google spreadsheet.

I also learned how to use expressions to extract user details, including company names from nested JSON data, and how n8n processes multiple records automatically.

## 2. Objective

- Fetch user details from a public API.
- Connect n8n to Google Sheets.
- Store API data in a spreadsheet.
- Use expressions to map data to the correct columns.
- Extract company names from nested JSON data.
- Test the workflow and verify the stored records.

## 3. Workflow Name

`Topic 12 API & Data Storage Integration Workflow`

## 4. Workflow Setup

The workflow contains three nodes:

**Manual Trigger → Fetch API Users → Store Users in Sheet**

### Node 1: Manual Trigger

This node starts the workflow when I click **Test workflow**.

### Node 2: Fetch API Users

I used the HTTP Request node to retrieve user details from the JSONPlaceholder API.

- **Method:** GET
- **URL:** `https://jsonplaceholder.typicode.com/users`
- **Authentication:** None

The API returns 10 sample user records containing details such as ID, name, email, and company information.

### Node 3: Store Users in Sheet

I used the Google Sheets node to save the retrieved user details in a spreadsheet.

- **Credential:** Authorized Google Sheets account
- **Operation:** Append Row
- **Spreadsheet:** `N8N API Storage Spreadsheet`
- **Sheet:** `Sheet1`

Before running the workflow, I created the spreadsheet and added these column headers in the first row:

| ID | Name | Email | Company |
|---|---|---|---|

## 5. Field Mapping Using Expressions

I mapped the API response fields to the corresponding Google Sheets columns using n8n expressions.

| Column | Expression |
|---|---|
| ID | `{{ $json.id }}` |
| Name | `{{ $json.name }}` |
| Email | `{{ $json.email }}` |
| Company | `{{ $json.company.name }}` |

The expression `{{ $json.company.name }}` retrieves the company name from the nested company object in the API response.

For example, the first record contains:

- **ID:** 1
- **Name:** Leanne Graham
- **Email:** Sincere@april.biz
- **Company:** Romaguera-Crona

## 6. Steps to Execute the Workflow

1. Create a new workflow in n8n.
2. Add the Manual Trigger node.
3. Add the HTTP Request node and rename it **Fetch API Users**.
4. Configure the GET request using the JSONPlaceholder users URL.
5. Execute the node and check the returned user details.
6. Create a Google spreadsheet named `N8N API Storage Spreadsheet`.
7. Add the headers ID, Name, Email, and Company.
8. Add the Google Sheets node and rename it **Store Users in Sheet**.
9. Connect your Google account and select the spreadsheet and worksheet.
10. Map the four columns using the expressions listed above.
11. Run the complete workflow by clicking **Test workflow**.
12. Open Google Sheets and check whether the user records were added.
13. Save the workflow.

## 7. Expected Output

After successful execution, the Google spreadsheet should contain 10 user records below the header row.

| ID | Name | Email | Company |
|---|---|---|---|
| 1 | Leanne Graham | Sincere@april.biz | Romaguera-Crona |
| 2 | Ervin Howell | Shanna@melissa.tv | Deckow-Crist |
| 3 | Clementine Bauch | Nathan@yesenia.net | Romaguera-Jacobson |


Git URL:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom Video:

https://www.loom.com/share/2decb59195544f6cb9a00c55661849b8
