# Topic 6: Data Transformation

## 1. Project Overview

This project demonstrates how to clean and standardize raw data using n8n core nodes and expressions.

The workflow uses a Manual Trigger and two Edit Fields (Set) nodes. The first node creates sample raw data with inconsistent casing and surrounding whitespace. The second node transforms the data into a standardized output schema containing only the clean fields.

**Workflow Name:** `Topic 6 Data Transformation Workflow`

## 2. Learning Objectives

By completing this assessment, I will demonstrate how to:

- Create mock raw data using the Edit Fields node.
- Reference incoming values with `$json`.
- Remove leading and trailing whitespace using `.trim()`.
- Convert names to uppercase using `.toUpperCase()`.
- Convert email addresses to lowercase using `.toLowerCase()`.
- Map raw fields into standardized field names.
- Exclude original input fields from the final output.
- Execute the workflow and validate the transformed JSON.

## 3. Workflow Architecture

```text
Manual Trigger
      |
      v
Dirty Raw Data
      |
      v
Reformat & Map
```

### Node 1: Manual Trigger

**Purpose:** Starts the workflow when the user clicks Test workflow.

### Node 2: Dirty Raw Data

**Node type:** Edit Fields (Set)

**Purpose:** Creates mock raw data to simulate an external form submission or incoming payload.

Configure the following fields as Strings.

| Field | Example value |
|---|---|
| Raw_Name | `  Jane DOE  ` |
| contact_email | ` JANE@Example.com ` |
| phone_number | ` 123-456-7890 ` |



Expected raw data:

```json
{
  "Raw_Name": "  Jane DOE  ",
  "contact_email": " JANE@Example.com ",
  "phone_number": " 123-456-7890 "
}
```

### Node 3: Reformat & Map

**Node type:** Edit Fields (Set)

**Purpose:** Cleans the raw values, maps them into standardized field names, and excludes the original fields.

Set **Include Other Input Fields** to **Off** so that only the three new fields appear in the final output.

### Task A: Clean the Name

**Output field:** `cleanName`

**Type:** String

Expression:

```javascript
{{ $json.Raw_Name.trim().toUpperCase() }}
```

Explanation:

- `$json.Raw_Name` retrieves the original name.
- `.trim()` removes leading and trailing whitespace.
- `.toUpperCase()` converts the name to uppercase.

Expected value: `JANE DOE`

### Task B: Clean the Email

**Output field:** `cleanEmail`

**Type:** String

Expression:

```javascript
{{ $json.contact_email.trim().toLowerCase() }}
```

Explanation:

- `$json.contact_email` retrieves the original email.
- `.trim()` removes surrounding whitespace.
- `.toLowerCase()` converts the email address to lowercase.

Expected value: `jane@example.com`

### Task C: Clean the Phone Number

**Output field:** `cleanPhone`

**Type:** String

Expression:

```javascript
{{ $json.phone_number.trim() }}
```

Explanation:

- `$json.phone_number` retrieves the raw phone number.
- `.trim()` removes leading and trailing whitespace.
- The phone number remains a String, preserving its formatting.

Expected value: `123-456-7890`

This task removes surrounding whitespace only. It does not remove hyphens or change the phone number's internal format.

## 4. Implementation Steps

1. Create a workflow named `Topic 6 Data Transformation Workflow`.
2. Add a Manual Trigger node.
3. Add an Edit Fields node and rename it `Dirty Raw Data`.
4. Create the three raw String fields with intentional surrounding spaces and inconsistent casing.
5. Test the first Edit Fields node.
6. Add another Edit Fields node and rename it `Reformat & Map`.
7. Set Include Other Input Fields to Off.
8. Create `cleanName` with the trim and uppercase expression.
9. Create `cleanEmail` with the trim and lowercase expression.
10. Create `cleanPhone` with the trim expression.
11. Execute the complete workflow.
12. Inspect the final output in JSON mode.
13. Verify that only the three clean fields appear.
14. Save the workflow and export its actual JSON.
15. Capture screenshots of the workflow, expressions, and output.

## 5. Expected Final Output

The final output should contain only the standardized fields:

```json
[
  {
    "cleanName": "JANE DOE",
    "cleanEmail": "jane@example.com",
    "cleanPhone": "123-456-7890"
  }
]
```

The original fields `Raw_Name`, `contact_email`, and `phone_number` should not appear in the final output when Include Other Input Fields is disabled.

