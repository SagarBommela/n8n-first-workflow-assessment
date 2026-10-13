# Topic 7: Schedule Trigger

## Overview

This project demonstrates how to configure the Schedule Trigger node in n8n to execute a workflow automatically based on time-based schedules.

The workflow includes two scheduling rules and an Edit Fields node that captures the execution timestamp in a readable format.

**Workflow Name:** Topic 7 Schedule Trigger Workflow

## Learning Objectives

- Understand the purpose of the Schedule Trigger node.
- Configure a daily schedule.
- Configure a custom weekday schedule using cron syntax.
- Understand the basic structure of a five-field cron expression.
- Use the `$now` expression to generate a formatted timestamp.
- Test, save, and activate a scheduled workflow.

## Workflow Design

The workflow contains the following nodes:

1. **Schedule Trigger** – Defines the workflow's scheduled execution rules.
2. **Log Execution** – Uses the Edit Fields node to create a formatted execution timestamp.

Workflow structure:

```text
Schedule Trigger
       |
       v
Log Execution
```

## Schedule Configuration

### Rule 1: Daily Schedule

- Trigger Interval: Days / Every Day
- Days Interval: 1
- Time: 09:00

This rule schedules the workflow to run every day at 9:00 AM.

### Rule 2: Weekday Cron Schedule

Cron expression:

```text
30 8 * * 1-5
```

This rule schedules the workflow to run at 8:30 AM, Monday through Friday, using standard five-field cron syntax.

| Field | Value | Meaning |
|---|---|---|
| Minute | `30` | At minute 30 |
| Hour | `8` | At 8 AM |
| Day of month | `*` | Every day of the month |
| Month | `*` | Every month |
| Day of week | `1-5` | Monday through Friday in standard cron syntax |

**Note:** n8n versions may present custom cron configuration differently. Confirm that the node accepts the five-field expression and interprets the weekday values as expected.

## Log Execution Configuration

The downstream Edit Fields node is renamed **Log Execution**.

Create the following field:

| Field | Type | Expression |
|---|---|---|
| `executionTime` | String | `{{ $now.toFormat('yyyy-MM-dd HH:mm:ss') }}` |

The expression formats the current date and time as:

```text
yyyy-MM-dd HH:mm:ss
```

For example, a timestamp might look like:

```text
2026-10-13 12:30:00
```

The value above is an example only. The actual value depends on when the workflow executes and the applicable timezone.

## Implementation Steps

1. Create a new workflow named `Topic 7 Schedule Trigger Workflow`.
2. Add the Schedule Trigger node.
3. Configure the daily schedule for 9:00 AM.
4. Add the custom weekday cron rule: `30 8 * * 1-5`.
5. Add an Edit Fields node and rename it `Log Execution`.
6. Add the String field `executionTime`.
7. Configure its value using `{{ $now.toFormat('yyyy-MM-dd HH:mm:ss') }}`.
8. Execute a manual test and inspect the output.
9. Save the workflow.
10. Set the appropriate workflow timezone.
11. Activate the workflow if permitted and required for the assessment.

## Expected Output

The Log Execution node should produce an item similar to the following:

```json
[
  {
    "executionTime": "2026-10-13 12:30:00"
  }
]
```

The timestamp is illustrative. Your actual output should reflect the execution time.


## Submission

- GitHub Repository: 

https://github.com/SagarBommela/n8n-first-workflow-assessment


- Loom Video: 

https://www.loom.com/share/caebd01651ed4b9aacd85e46512289b9
