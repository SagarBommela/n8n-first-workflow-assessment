# Topic 11: HTTP Request Node – n8n Hands-On Beginner Course

## Overview

In this topic, I learned how to use the HTTP Request node in n8n to communicate with a public REST API. I used a GET request to retrieve user details and a POST request to send data to a mock API endpoint.

I also used the Edit Fields node and dynamic expressions to prepare the request payload using the retrieved user information.

## Objective

- Learn how to use the HTTP Request node in n8n.
- Retrieve user details using a GET request.
- Prepare data using the Edit Fields node.
- Send data using a POST request.
- Use dynamic expressions to pass data between nodes.
- Test the workflow and verify the API response.

## Workflow Name

`Topic 11 HTTP Request Node Workflow`

## Workflow Architecture

Manual Trigger → Fetch User → Prepare Post Payload → Send Custom Post

## Nodes Used

### 1. Manual Trigger

Starts the workflow when I click **Test workflow**.

### 2. Fetch User

- **Node:** HTTP Request
- **Method:** GET
- **URL:** `https://jsonplaceholder.typicode.com/users/1`
- **Authentication:** None

This node retrieves sample user details, such as the user's name, username, and email address.

### 3. Prepare Post Payload

- **Node:** Edit Fields
- **Fields:** `title` and `body`

I used dynamic expressions to prepare the data for the POST request.

| Field | Expression |
|---|---|
| `title` | `User Post by {{ $json.name }}` |
| `body` | `Email: {{ $json.email }}` |

For example, the prepared data will look like this:

```json
{
  "title": "User Post by Leanne Graham",
  "body": "Email: Sincere@april.biz"
}
```

### 4. Send Custom Post

- **Node:** HTTP Request
- **Method:** POST
- **URL:** `https://jsonplaceholder.typicode.com/posts`
- **Body Content Type:** JSON
- **Specify Body:** Using Fields Below

I configured the following fields:

| Parameter | Value |
|---|---|
| `title` | `{{ $json.title }}` |
| `body` | `{{ $json.body }}` |

This node sends the prepared data to the JSONPlaceholder API.

## Steps to Execute the Workflow

1. Create a new workflow in n8n.
2. Add the Manual Trigger node.
3. Add an HTTP Request node named **Fetch User** and configure the GET request.
4. Add the Edit Fields node named **Prepare Post Payload**.
5. Create the `title` and `body` fields using dynamic expressions.
6. Add another HTTP Request node named **Send Custom Post**.
7. Configure the POST request and select JSON as the body content type.
8. Map the `title` and `body` fields using expressions.
9. Click **Test workflow** to execute all the nodes.
10. Check the output of the final node and verify the returned data.
11. Save the workflow.

## Expected Output

The final node should return a JSON response containing the submitted title and body, along with a mock post ID, typically `101`.

Example:

```json
{
  "title": "User Post by Leanne Graham",
  "body": "Email: Sincere@april.biz",
  "id": 101
}
```

GIT url:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom Video:

https://www.loom.com/share/7eeef6a0290645d0888f157c105d9da1

