# Topic 5: Expressions & Variables

## 1. Project Overview

This project demonstrates how to use n8n expressions to transform text, combine input values, format dates, and generate the current date dynamically.

The workflow uses a Manual Trigger and two Edit Fields (Set) nodes. The first node creates sample student information. The second node transforms the name and birth date and generates the processing date.

**Workflow Name:** `Topic 5 Expressions Workflow`

## 2. Learning Objectives

By completing this assessment, I will demonstrate how to:

- Create input fields using the Edit Fields node.
- Reference incoming data using `$json`.
- Combine strings using JavaScript expressions.
- Convert text to uppercase.
- Parse an ISO date and format it into a readable date.
- Use `$now` to get the current date and time.
- Validate dynamic expressions by executing the workflow.

## 3. Workflow Architecture

```text
Manual Trigger
      |
      v
Set Student Info
      |
      v
Format and Transform
```

### Node 1: Manual Trigger

**Purpose:** Starts the workflow when the user clicks Test workflow.

### Node 2: Set Student Info

**Purpose:** Creates sample student information.

Configure the following fields:

| Field | Type | Value |
|---|---|---|
| firstName | String | alex |
| lastName | String | smith |
| birthDate | String | 1998-04-12T10:15:30.000Z |

Expected output:

```json
{
  "firstName": "alex",
  "lastName": "smith",
  "birthDate": "1998-04-12T10:15:30.000Z"
}
```

### Node 3: Format and Transform

**Purpose:** Uses expressions to transform the student information and create additional fields.

Configure these three fields.

### Task A: Combine Strings and Convert to Uppercase

**Output field:** `fullNameUpperCase`

**Type:** String

Expression:

```javascript
{{ ($json.firstName + ' ' + $json.lastName).toUpperCase() }}
```

Explanation:

- `$json.firstName` retrieves `alex`.
- `$json.lastName` retrieves `smith`.
- The `+` operator combines the names with a space.
- `.toUpperCase()` converts the result to uppercase.

Expected value:

```text
ALEX SMITH
```

### Task B: Parse and Format the Birth Date

**Output field:** `formattedBirthDate`

**Type:** String

Expression:

```javascript
{{ DateTime.fromISO($json.birthDate).toFormat('MMMM dd, yyyy') }}
```

Explanation:

- `DateTime.fromISO()` parses the ISO date string.
- `.toFormat('MMMM dd, yyyy')` formats it with the full month name, two-digit day, and four-digit year.

Expected value:

```text
April 12, 1998
```

**Note:** This expression uses `DateTime.fromISO()`, the documented Luxon date-time constructor in n8n expressions. The assessment's `$dateTime.fromISO(...)` spelling may not work in your n8n version. If you encounter an expression error, use the expression above. See the [n8n date and time documentation](https://docs.n8n.io/data/expression-reference/date-time/).

### Task C: Generate the Current Date

**Output field:** `processedDate`

**Type:** String

Expression:

```javascript
{{ $now.toFormat('yyyy-MM-dd') }}
```

Explanation:

- `$now` represents the current date and time in the workflow's configured time zone.
- `.toFormat('yyyy-MM-dd')` returns the date in year-month-day format.

Example value:

```text
2026-10-12
```

The actual value will depend on the date and time when the workflow executes and the workflow's time zone.

## 4. Implementation Steps

1. Create a workflow named `Topic 5 Expressions Workflow`.
2. Add a Manual Trigger node.
3. Add an Edit Fields node and rename it `Set Student Info`.
4. Configure `firstName`, `lastName`, and `birthDate`.
5. Test the first Edit Fields node.
6. Add a second Edit Fields node and rename it `Format and Transform`.
7. Add the `fullNameUpperCase` field using the string-combination expression.
8. Add the `formattedBirthDate` field using `DateTime.fromISO()`.
9. Add the `processedDate` field using `$now.toFormat()`.
10. Ensure the second node retains the original input fields if the required output should contain all six fields.
11. Execute the complete workflow.
12. Inspect the JSON output and verify the values.
13. Save the workflow and export the actual workflow JSON.
14. Capture screenshots of the node configurations, expressions, and final output.

## 5. Expected Final Output

The final output should contain the original student fields and three additional transformed fields.

```json
[
  {
    "firstName": "alex",
    "lastName": "smith",
    "birthDate": "1998-04-12T10:15:30.000Z",
    "fullNameUpperCase": "ALEX SMITH",
    "formattedBirthDate": "April 12, 1998",
    "processedDate": "2026-10-12"
  }
]
```


