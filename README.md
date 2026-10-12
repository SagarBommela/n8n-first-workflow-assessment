# n8n Hands-On Beginner Course — Topic 1

## Create Your First Workflow

**Assessment:** Tayana Academy LMS — n8n Hands-On Level 1  
**Difficulty:** Beginner  
**Workflow Name:** My First N8N Workflow

## 1. Project Objective

The objective of this project is to create, configure, execute, and validate a basic n8n workflow using a Manual Trigger node and an Edit Fields (Set) node.

The workflow produces a structured output containing a greeting field with the value `Hello, n8n!`.

## 2. Prerequisites

- Access to an n8n Cloud, self-hosted, or local instance.
- A compatible web browser.
- Permission to create, edit, execute, and save workflows.
- Basic knowledge of navigating a web application.
- GitHub access for publishing the assessment files.

## 3. Workflow Architecture

The workflow contains two nodes connected in sequence:

1. **Manual Trigger:** Starts execution when the workflow is run manually.
2. **Edit Fields (Set):** Creates a String field named `greeting` with the value `Hello, n8n!`.

### Workflow Sequence

Manual Trigger → Edit Fields (Set)

No external API, database, credentials, or additional integrations are required for this workflow.

## 4. Node Configuration

### Manual Trigger

- Purpose: Start the workflow manually.
- Configuration: No additional input is required for this basic exercise.

### Edit Fields (Set)

- Mode: Manual Mapping, if available.
- Field Name: `greeting`
- Field Type: String
- Field Value: `Hello, n8n!`

## 5. Expected Output

The workflow should produce one output item containing the following JSON object:

```json
{
  "greeting": "Hello, n8n!"
}
```

Depending on the output viewer, n8n may display the object inside an array representing the workflow's output items.

## 6. Implementation Steps

1. Open the n8n workspace.
2. Create a new workflow.
3. Name the workflow `My First N8N Workflow`.
4. Add the Manual Trigger node.
5. Add the Edit Fields (Set) node.
6. Connect Manual Trigger to Edit Fields (Set).
7. Configure the `greeting` String field.
8. Execute the workflow using the manual test or execution button.
9. Inspect the output in Table, JSON, and Schema views where available.
10. Save the completed workflow.
11. Export the workflow as a JSON file.
12. Capture screenshots and record a demonstration video.

## 7. Execution Instructions

1. Open the workflow in n8n.
2. Select the manual execution or test button.
3. Wait for the workflow to finish.
4. Select the Edit Fields node.
5. Inspect the output.
6. Verify that `greeting` equals `Hello, n8n!`.

