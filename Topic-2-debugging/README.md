# n8n Hands-On Level 1 — Topic 2

## Understanding Workflow Execution & Debugging Basics

**Topic:** 2 — Understanding Workflow Execution & Debugging Basics  
**Workflow Name:** Topic 2 Debugging Workflow

## 1. Project Objective

This project demonstrates how to analyze workflow execution, inspect data flowing between nodes, simulate an HTTP Request failure, diagnose an error, test an individual node, and review historical executions in n8n.

The workflow is based on the Topic 1 greeting workflow and adds an HTTP Request node for debugging practice.

## 2. Prerequisites

- Access to an n8n Cloud, self-hosted, or local instance.
- Permission to create, duplicate, execute, and save workflows.
- A compatible web browser.
- Completion of, or familiarity with, Topic 1.
- Access to the assessment-provided mock HTTP endpoint, if it remains available.
- GitHub access for publishing the project files.
- A screen recorder such as Loom or an equivalent tool.

## 3. Workflow Architecture

The workflow contains three nodes in the following sequence:

1. **Manual Trigger:** Starts workflow execution manually.
2. **Edit Fields (Set):** Creates the greeting field.
3. **HTTP Request:** Sends an HTTP GET request to the configured URL.

### Workflow Sequence

Manual Trigger → Edit Fields (Set) → HTTP Request

## 4. Node Configuration

### Manual Trigger

- Purpose: Start the workflow manually.
- Additional configuration: None required for this exercise.

### Edit Fields (Set)

- Field Name: `greeting`
- Field Type: String
- Field Value: `Hello, n8n!`

### HTTP Request

- Method: GET
- Failure-test URL: `https://this-domain-does-not-exist-12345.com`
- Assessment-provided test URL: `https://1cb106c19a1049339451476e8e4885c5.api.mockbin.io/`

The first URL is intended to simulate a hostname-resolution failure. The second URL is the endpoint supplied by the assessment and must be tested during implementation.

## 5. Expected Data Flow

The Edit Fields node should produce an item containing:

```json
{
  "greeting": "Hello, n8n!"
}
```

The HTTP Request node receives the output from the preceding node as its input. The greeting field does not automatically become an HTTP request parameter or request body; the HTTP Request configuration determines how a request is sent.

## 6. Implementation Steps

1. Open the original Topic 1 workflow.
2. Duplicate the workflow.
3. Rename the duplicate to `Topic 2 Debugging Workflow`.
4. Add an HTTP Request node after Edit Fields.
5. Configure the HTTP method as GET.
6. Set the intentionally invalid URL.
7. Run the workflow and inspect the failure.
8. Open the HTTP Request node's Input and error/output details.
9. Verify the incoming greeting data.
10. Replace the invalid URL with the assessment-provided mock endpoint.
11. Test the HTTP Request node individually using Test step, if available.
12. Inspect and record the actual result.
13. Open the Executions area and review historical runs.
14. Save and export the workflow JSON.
15. Capture screenshots and record a demonstration video.

## 7. Debugging Concepts Demonstrated

### Node execution status

Node status indicators help identify which steps succeeded and where execution failed.

### Input inspection

The Input panel helps confirm whether the preceding node supplied the expected data.

### Error inspection

The HTTP Request error details help identify the cause of a failed request. A DNS error such as `ENOTFOUND` indicates that the hostname could not be resolved.

