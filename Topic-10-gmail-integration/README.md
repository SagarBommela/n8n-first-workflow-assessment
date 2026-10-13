# Topic 10: Gmail Integration

## 1. Overview

In this topic, I learned how to connect Gmail with n8n and send personalized emails automatically. I used sample customer details and dynamic expressions to add the recipient's name and email address to the message.

## 2. Objective

- Connect Gmail to n8n using OAuth2 authentication.
- Create sample customer data using the Edit Fields node.
- Configure the Gmail node to send emails.
- Use dynamic expressions for the recipient, subject, and email body.
- Test the workflow and check whether the email was received.

## 3. Workflow Name

`Topic 10 Gmail Integration Workflow`

## 4. Workflow Setup

The workflow has three nodes:

**Manual Trigger → Mock Customer Data → Send Personalized Email**

### Node 1: Manual Trigger

This node starts the workflow when I click **Test workflow**.

### Node 2: Mock Customer Data

I used the Edit Fields node to add the following details:

| Field Name | Value |
|---|---|
| `customerName` | Alice Smith |
| `customerEmail` | My own email address |

These details are passed to the Gmail node.

### Node 3: Send Personalized Email

I configured the Gmail node with the following settings:

- **Credential:** Gmail OAuth2
- **Resource:** Message
- **Operation:** Send
- **To:** `{{ $json.customerEmail }}`
- **Subject:** `Welcome to N8N Course, {{ $json.customerName }}!`
- **Email Type:** Plain Text

**Email body:**

Hi {{ $json.customerName }},

Congratulations on completing Topic 10 of the N8N Hands-On Beginner Course!

This email was sent automatically using customer details from the previous node.

Best regards,  
Your Automation Engine

## 5. Using Dynamic Expressions

Dynamic expressions help n8n use data from a previous node when sending an email.

| Expression | Purpose |
|---|---|
| `{{ $json.customerEmail }}` | Gets the recipient's email address |
| `{{ $json.customerName }}` | Gets the customer's name |

For example, the subject becomes:

`Welcome to N8N Course, Alice Smith!`

The greeting becomes:

`Hi Alice Smith,`

This allows n8n to personalize emails without entering the details manually each time.

## 6. Steps to Execute the Workflow

1. Create a new workflow in n8n.
2. Add the Manual Trigger node.
3. Add the Edit Fields node and rename it **Mock Customer Data**.
4. Enter the customer name and your email address.
5. Add the Gmail node and rename it **Send Personalized Email**.
6. Connect your Gmail OAuth2 account.
7. Configure the recipient, subject, and message body using expressions.
8. Connect all three nodes in the correct order.
9. Click **Test workflow** to run it.
10. Check your Gmail inbox and confirm that you received the email.
11. Save the workflow.

## 7. Expected Output

After successful execution, I should receive an email with the following details.

**Subject:** Welcome to N8N Course, Alice Smith!

**Message:**

Hi Alice Smith,

Congratulations on completing Topic 10 of the N8N Hands-On Beginner Course!

This email was sent automatically using customer details from the previous node.

Best regards,  
Your Automation Engine


Git URL:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom Video:

https://www.loom.com/share/986b26d481764badb0ce27fa87abdad6

