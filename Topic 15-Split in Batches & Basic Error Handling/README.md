# Topic 15: Split in Batches & Basic Error Handling

## 1. Overview

In this workflow, I used the Loop Over Items (Split in Batches) node in n8n to process five URLs in batches of two.

I also added an invalid URL to test error handling. The workflow should continue processing the remaining URLs even if one request fails.

## 2. Objective

- Create five URL items.
- Process them in batches of two.
- Send HTTP GET requests for each URL.
- Handle errors without stopping the workflow.
- Process all batches and reach the final node.

## 3. Workflow Nodes

1. **Manual Trigger:** Starts the workflow.
2. **Mock Items List:** Contains five URLs.
3. **Loop Over Items:** Processes the URLs in batches of two.
4. **Fetch Details:** Sends HTTP requests to the URLs.
5. **Compile Final List:** Adds a final status to the output.

## 4. Test Data

I used the following five URLs:

- Item 1: `https://jsonplaceholder.typicode.com/posts/1`
- Item 2: `https://jsonplaceholder.typicode.com/posts/1`
- Item 3: `https://invalid-url-domain-does-not-exist.xyz/`
- Item 4: `https://jsonplaceholder.typicode.com/posts/1`
- Item 5: `https://jsonplaceholder.typicode.com/posts/1`

The third URL is intentionally invalid to test error handling.

## 5. HTTP Request Configuration

In the Fetch Details node, I configured the following settings:

- Method: GET
- URL: `{{ $json.url }}`
- Authentication: None
- On Error: Continue

The URL expression takes the URL from the current input item.

## 6. Batch Processing

I set the batch size to 2 in the Loop Over Items node.

The items are processed in three batches:

- Batch 1: Items 1 and 2
- Batch 2: Items 3 and 4
- Batch 3: Item 5

After processing each batch, I connected the Fetch Details node back to the Loop Over Items node to process the next batch.

## 7. Error Handling

I used an invalid URL to test what happens when an HTTP request fails.

I configured the Fetch Details node to continue when an error occurs. This allows the workflow to attempt processing the remaining items instead of stopping at the first failed request.

## 8. Final Output

After all batches are processed, the workflow continues through the Done output to the Compile Final List node.

I added a status field with the value `All Batches Processed`.

This shows that the workflow reached the final node. I also checked the execution results to verify how the requests were handled.


Git Url:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom Video:

https://www.loom.com/share/62c55dd8a88a46de925adceedbf07dc7