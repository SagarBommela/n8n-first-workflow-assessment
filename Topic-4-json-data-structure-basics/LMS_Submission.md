# LMS Submission – Topic 4: JSON & Data Structure Basics

## 1. Assessment Details

**Course:** n8n Hands-On Beginner Course  
**Topic:** Topic 4 – JSON & Data Structure Basics  
**Workflow Name:** `Topic 4 JSON Basics Workflow`

## 2. Implementation Summary

I created an n8n workflow using a Manual Trigger, a Code node, and an Edit Fields node.

The `Mock Nested JSON Data` Code node generates a sample customer profile containing:

- Customer name and email.
- A nested address object with city and ZIP code.
- An array containing two order objects.
- A customer status field.

I inspected the generated data in JSON, Table, and Schema views.

The `Extract Values` node uses n8n expressions to extract the customer name, city, and first order total into a flat JSON object.

## 3. Expressions Implemented

| Output field | Expression | Expected value |
|---|---|---|
| customerName | `{{ $json.customer.name }}` | Jane Doe |
| cityOfCustomer | `{{ $json.customer.address.city }}` | New York |
| firstOrderTotal | `{{ $json.orders[0].total }}` | 45.99 |


## 5. Expected Final Output

```json
[
  {
    "customerName": "Jane Doe",
    "cityOfCustomer": "New York",
    "firstOrderTotal": 45.99
  }
]
```

##  Submission Links

- GitHub Repository:

https://github.com/SagarBommela/n8n-first-workflow-assessment

- Loom Demo:

https://www.loom.com/share/a241fc3711a2448cae53f058baa2686a

