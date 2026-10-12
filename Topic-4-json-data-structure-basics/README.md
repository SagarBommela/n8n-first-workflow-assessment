# Topic 4: JSON & Data Structure Basics

## 1. Project Overview

This project demonstrates how n8n represents data using JSON objects and arrays and how to extract values from nested JSON structures using expressions.

The workflow uses a Manual Trigger, a Code node that generates mock customer data, and an Edit Fields node that extracts selected values into a flat JSON object.

**Workflow Name:** `Topic 4 JSON Basics Workflow`

## 2. Learning Objectives

By completing this assessment, I will demonstrate how to:

- Understand JSON objects and key-value pairs.
- Understand JSON arrays and array indexes.
- Generate nested JSON data using an n8n Code node.
- Inspect JSON data using JSON, Table, and Schema views.
- Access nested values using dot notation.
- Retrieve an item from an array using its index.
- Use expressions in the Edit Fields node.
- Validate the final output and save the workflow.

## 3. Workflow Architecture

The workflow contains three nodes:

```text
Manual Trigger
      |
      v
Mock Nested JSON Data
      |
      v
Extract Values
```

### Node 1: Manual Trigger

**Purpose:** Starts the workflow when the user clicks Test workflow.

### Node 2: Mock Nested JSON Data

**Node type:** Code

**Language:** JavaScript

**Mode:** Run Once for All Items

**Purpose:** Generates a sample customer profile containing nested objects and an array of orders.

Use the following code in the Code node:

```javascript
return [
  {
    json: {
      customer: {
        name: "Jane Doe",
        email: "jane@example.com",
        address: {
          city: "New York",
          zipcode: "10001"
        }
      },
      orders: [
        { id: 101, total: 45.99 },
        { id: 102, total: 12.50 }
      ],
      status: "active"
    }
  }
];
```




### Node 3: Extract Values

**Node type:** Edit Fields (Set)

**Purpose:** Extracts selected values from the nested input data and creates a flat output object.

Configure the following fields.

| Output field | Type | Expression | Expected value |
|---|---|---|---|
| customerName | String | `{{ $json.customer.name }}` | Jane Doe |
| cityOfCustomer | String | `{{ $json.customer.address.city }}` | New York |
| firstOrderTotal | Number | `{{ $json.orders[0].total }}` | 45.99 |

Ensure the node retains only the intended output fields if that is how the assessment is configured. In Edit Fields, disable Include Other Input Fields when you want only these three extracted fields.

## 4. Understanding the Expressions

### Task A: Access a Nested Customer Name

Expression:

```javascript
{{ $json.customer.name }}
```

Explanation:

- `$json` refers to the current input item's JSON data.
- `customer` accesses the customer object.
- `name` accesses the customer's name.

Expected value: `Jane Doe`

### Task B: Access a Nested City

Expression:

```javascript
{{ $json.customer.address.city }}
```

Explanation:

- `$json` accesses the current input data.
- `customer` accesses the customer object.
- `address` accesses the nested address object.
- `city` retrieves the city value.

Expected value: `New York`

### Task C: Access the First Order Total

Expression:

```javascript
{{ $json.orders[0].total }}
```

Explanation:

- `orders` accesses the array of orders.
- `[0]` selects the first array item because array indexes start at zero.
- `total` retrieves the total from that order.

Expected value: `45.99`

The second order is at index `[1]`, and its total is `12.5`.

## 5. Implementation Steps

1. Create a new workflow named `Topic 4 JSON Basics Workflow`.
2. Add the Manual Trigger node.
3. Add a Code node and rename it `Mock Nested JSON Data`.
4. Set the Code node language to JavaScript.
5. Use the appropriate mode and paste the nested JSON generation code.
6. Test the Code node.
7. Inspect its output in JSON, Table, and Schema views.
8. Add an Edit Fields node and rename it `Extract Values`.
9. Configure `customerName`, `cityOfCustomer`, and `firstOrderTotal`.
10. Use the expressions documented above.
11. Configure the node to output only the three extracted fields.
12. Run the complete workflow.
13. Verify the output in JSON mode.
14. Save the workflow and export its JSON file.
15. Capture screenshots of the workflow, nested data, expressions, and final output.

## 6. Expected Final Output

The final output should contain one item with these three fields:

```json
[
  {
    "customerName": "Jane Doe",
    "cityOfCustomer": "New York",
    "firstOrderTotal": 45.99
  }
]
```

The output is a flat object: the selected nested values are extracted from the original customer payload.
