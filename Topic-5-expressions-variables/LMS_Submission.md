# LMS Submission – Topic 5: Expressions & Variables

## 1. Assessment Details

**Course:** n8n Hands-On Beginner Course  
**Topic:** Topic 5 – Expressions & Variables  
**Workflow Name:** `Topic 5 Expressions Workflow`

## 2. Implementation Summary

I created an n8n workflow using a Manual Trigger and two Edit Fields (Set) nodes.

The `Set Student Info` node initializes the following fields:

- `firstName`: `alex`
- `lastName`: `smith`
- `birthDate`: `1998-04-12T10:15:30.000Z`

The `Format and Transform` node uses n8n expressions to:

1. Combine the first and last names and convert the result to uppercase.
2. Parse the ISO birth date and format it as a readable date.
3. Generate the current date in `yyyy-MM-dd` format.

## 3. Expressions Implemented

| Output field | Expression | Expected result |
|---|---|---|
| fullNameUpperCase | `{{ ($json.firstName + ' ' + $json.lastName).toUpperCase() }}` | `ALEX SMITH` |
| formattedBirthDate | `{{ DateTime.fromISO($json.birthDate).toFormat('MMMM dd, yyyy') }}` | `April 12, 1998` |
| processedDate | `{{ $now.toFormat('yyyy-MM-dd') }}` | Actual execution date |

## 5. Expected Final Output

The output should contain the following values. Replace the date placeholder with the actual date returned by your execution.

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



##  Submission Links

- GitHub Repository:

https://github.com/SagarBommela/n8n-first-workflow-assessment

- Loom Demo:

 https://www.loom.com/share/5297b5d6a4b746f0b2e0548f1e61021d


