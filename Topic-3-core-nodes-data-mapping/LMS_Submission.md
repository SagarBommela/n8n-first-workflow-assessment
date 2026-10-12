# LMS Submission – Topic 3: Working with Core Nodes & Data Mapping

## 1. Assessment Details

**Course:** n8n Hands-On Course  
**Topic:** Topic 3 – Working with Core Nodes & Data Mapping  
**Workflow Name:** `Topic 3 Core Nodes Workflow`

## 2. Implementation Summary

I created an n8n workflow using a Manual Trigger and two Edit Fields (Set) nodes.

The first Edit Fields node, `Set Original Data`, creates the following product data:

- `productName`: `Wireless Mouse`
- `basePrice`: `25`
- `isAvailable`: `true`

The second Edit Fields node, `Modify & Map`, performs the following operations:

1. Changes `isAvailable` from `true` to `false`.
2. Maps the incoming `productName` value into the new `inventoryLabel` field using an expression.
3. Calculates `priceWithTax` by multiplying `basePrice` by `1.1`.


##  Expected Output

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



##  Submission Links

- **GitHub Repository:**
https://github.com/SagarBommela/n8n-first-workflow-assessment/tree/main/Topic-2-debugging


- **Loom Demo:** 

https://www.loom.com/share/ef0063abbd514dec92f9a2f571b11bb6
