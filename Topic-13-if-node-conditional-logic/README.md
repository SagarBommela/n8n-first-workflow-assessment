Topic 13: IF Node & Conditional Logic

 1. Overview

In this workflow, I used the IF node in n8n to check order values and decide whether a customer is VIP or Regular.

If the order value is 100 or more, the customer is marked as VIP. If it is less than 100, the customer is marked as Regular.

2. Objective

- Create sample order data for two customers.
- Check their order values using the IF node.
- Set the customer status based on the order value.
- Check the results of both branches.

 3. Manual Trigger → Mock Orders → Check Order VIP Status

The IF node has two branches:
- True: Set VIP
- False: Set Regular


  1: Manual Trigger

Starts the workflow when I click Test workflow.

 2: Mock Orders

3: Check Order VIP Status

I added the IF node and configured the condition as follows:

- Value 1: `{{ $json.orderValue }}`
- Operator: Greater than or equal to
- Value 2: `100`

This checks whether the order value is 100 or more.

 4: Set VIP

I connected this node to the True branch and set the status to `VIP`.

Alice's order value is 150, so she is marked as VIP.

 5: Set Regular

I connected this node to the False branch and set the status to `Regular`.

Bob's order value is 75, so he is marked as Regular.

I enabled Include Other Input Fields to keep the customer name and order value in the output.

6. Execution Steps

1. Created a new workflow named Topic 13 IF Node Workflow.
2. Added the Manual Trigger node.
3. Added the Edit Fields node and created sample data for Alice and Bob.
4. Added the IF node and set the condition to check whether the order value is at least 100.
5. Connected the True branch to Set VIP.
6. Connected the False branch to Set Regular.
7. Executed the workflow and checked both outputs.
8. Saved the workflow and captured screenshots.



Git Url:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom video:

https://www.loom.com/share/3f84bb76e10b4a0f8edd5964151228db


