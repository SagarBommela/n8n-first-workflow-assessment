# Topic 14: Switch Node & Workflow Routing

## 1. Overview

In this workflow, I used the Switch node in n8n to route users based on their roles.

I created four users with different roles: admin, editor, viewer, and guest. Each user is sent to a different branch, where I set their access status.

## 2. Objective

- Create sample user data.
- Check user roles using the Switch node.
- Route users to the correct branches.
- Set the access status for each user.
- Check the output of all four branches.

## 3. Workflow Name

`Topic 14 Switch Node Workflow`

## 4. Workflow Structure

Manual Trigger → Mock Users → Route by Role

The Switch node has four outputs:

- Output 0: Set Admin
- Output 1: Set Editor
- Output 2: Set Viewer
- Output 3: Set Guest

## 5. Node Configuration

### Node 1: Manual Trigger

Starts the workflow when I click Test workflow.

### Node 2: Mock Users

I used the Edit Fields node to create four sample user records.

| Username | Role |
|---|---|
| Alice | admin |
| Bob | editor |
| Charlie | viewer |
| Dave | guest |

### Node 3: Route by Role

I added the Switch node and configured it to check the user's role using:

`{{ $json.role }}`



I enabled the fallback output for roles that do not match these rules. The guest user goes through this output.

### Node 4: Set Admin

I connected this node to Output 0 and set the status to `Admin Access`.

Alice receives Admin Access because her role is admin.

### Node 5: Set Editor

I connected this node to Output 1 and set the status to `Editor Access`.

Bob receives Editor Access because his role is editor.

### Node 6: Set Viewer

I connected this node to Output 2 and set the status to `Viewer Access`.

Charlie receives Viewer Access because his role is viewer.

### Node 7: Set Guest

I connected this node to the fallback output and set the status to `Guest Access`.

Dave receives Guest Access because his role is guest.

I enabled Include Other Input Fields in the Edit Fields nodes to keep the original user details in the output.

## 6. Execution Steps

1. Created a new workflow named Topic 14 Switch Node Workflow.
2. Added the Manual Trigger node.
3. Created four sample users in the Mock Users node.
4. Added the Switch node and configured the role conditions.
5. Enabled the fallback output.
6. Connected each output to the correct Edit Fields node.
7. Set the access status for each user.
8. Executed the workflow and checked all four outputs.
9. Saved the workflow and captured screenshots.

## 7. Expected Results

**Admin Output**

Alice receives Admin Access.

```json
{
  "username": "Alice",
  "role": "admin",
  "status": "Admin Access"
}
```

**Editor Output**

Bob receives Editor Access.

```json
{
  "username": "Bob",
  "role": "editor",
  "status": "Editor Access"
}
```

**Viewer Output**

Charlie receives Viewer Access.

```json
{
  "username": "Charlie",
  "role": "viewer",
  "status": "Viewer Access"
}
```

**Guest Output**

Dave receives Guest Access.

```json
{
  "username": "Dave",
  "role": "guest",
  "status": "Guest Access"
}
```

Git URL:

https://github.com/SagarBommela/n8n-first-workflow-assessment

Loom Video:

https://www.loom.com/share/84e377e614cb447a80cad4e31d2dac34

