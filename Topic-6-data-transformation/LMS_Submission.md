# LMS Submission – Topic 6: Data Transformation

## 1. Assessment Details

**Course:** n8n Hands-On Beginner Course  
**Topic:** Topic 6 – Data Transformation  
**Workflow Name:** `Topic 6 Data Transformation Workflow`

## 2. Implementation Summary

I created an n8n workflow using a Manual Trigger and two Edit Fields (Set) nodes.

The `Dirty Raw Data` node generates sample raw data containing inconsistent name casing, an uppercase email address, and leading or trailing whitespace.

The `Reformat & Map` node transforms the input into a standardized output schema by:

1. Trimming surrounding whitespace and converting the name to uppercase.
2. Trimming surrounding whitespace and converting the email address to lowercase.
3. Trimming surrounding whitespace from the phone number.
4. Excluding the original input fields from the final output.

## 3. Expressions Implemented

| Output field | Expression | Expected value |
|---|---|---|
| cleanName | `{{ $json.Raw_Name.trim().toUpperCase() }}` | `JANE DOE` |
| cleanEmail | `{{ $json.contact_email.trim().toLowerCase() }}` | `jane@example.com` |
| cleanPhone | `{{ $json.phone_number.trim() }}` | `123-456-7890` |


##  Submission Links

- GitHub Repository:

https://github.com/SagarBommela/n8n-first-workflow-assessment

- Loom video:

https://www.loom.com/share/30cf5540173b4b928f04a1fb719b85cf

