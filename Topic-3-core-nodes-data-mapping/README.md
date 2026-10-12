# Topic 3: Working with Core Nodes & Data Mapping

## 1. Project Overview

This project demonstrates how to use core n8n nodes to create, modify, and map data between workflow steps.

The workflow uses a Manual Trigger and two Edit Fields (Set) nodes to create product information, update an existing Boolean field, map a dynamic value, and calculate a price including 10% tax.

**Workflow Name:** `Topic 3 Core Nodes Workflow`

## 2. Learning Objectives

By completing this assessment, I will demonstrate how to:

- Create and configure an n8n workflow.
- Use the Manual Trigger node to start a workflow manually.
- Create String, Number, and Boolean fields using Edit Fields.
- Modify an existing field using its exact field name.
- Map an incoming value dynamically using an expression.
- Calculate a new value using an expression.
- Test workflow execution and validate the output JSON.

## 3. Workflow Architecture

The workflow contains three nodes:

```text
Manual Trigger
      |
      v
Set Original Data
      |
      v
Modify & Map
```

### Node 1: Manual Trigger

**Purpose:** Starts the workflow when the user clicks Test workflow.

### Node 2: Set Original Data

**Purpose:** Creates the initial mock product data.

| Field | Type | Value |
|---|---|---|
| productName | String | Wireless Mouse |
| basePrice | Number | 25 |
| isAvailable | Boolean | true |

Expected output:

```json
{
  "productName": "Wireless Mouse",
  "basePrice": 25,
  "isAvailable": true
}
```

### Node 3: Modify & Map

**Purpose:** Updates the availability value, maps the product name into a new field, and calculates the price including tax.

#### Task A: Modify an Existing Field

The `isAvailable` field is changed from `true` to `false`.

The field name must match the incoming field name exactly.

#### Task B: Map a Dynamic Value

The `inventoryLabel` field receives its value from the incoming `productName` field.

Expression:

```javascript
{{ $json.productName }}
```

Expected value:

```text
Wireless Mouse
```

#### Task C: Calculate Price Including Tax

The `priceWithTax` field calculates the base price plus 10% tax.

Expression:

```javascript
{{ $json.basePrice * 1.1 }}
```

Calculation:

```text
25 × 1.1 = 27.5
```

## 4. Implementation Steps

1. Create a new workflow named `Topic 3 Core Nodes Workflow`.
2. Add a Manual Trigger node.
3. Add an Edit Fields node and rename it `Set Original Data`.
4. Configure `productName`, `basePrice`, and `isAvailable`.
5. Test the `Set Original Data` node and confirm the three fields appear in the output.
6. Add a second Edit Fields node and rename it `Modify & Map`.
7. Set `isAvailable` to `false`.
8. Add `inventoryLabel` and map it from `productName`.
9. Add `priceWithTax` using the expression `{{ $json.basePrice * 1.1 }}`.
10. Execute the workflow and inspect the final output in JSON mode.
11. Save the workflow and export its JSON.
12. Capture screenshots of the workflow, field configurations, expressions, and output.

## 5. Expected Final Output

The final output should contain the following values:

```json
[
  {
    "productName": "Wireless Mouse",
    "basePrice": 25,
    "isAvailable": false,
    "inventoryLabel": "Wireless Mouse",
    "priceWithTax": 27.5
  }
]
```

The output is expected to retain the original fields while updating `isAvailable` and adding `inventoryLabel` and `priceWithTax`.

