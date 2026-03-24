# Task Manager CLI - User Guide

## Getting Started
This guide explains how to use the Task Manager CLI step by step.

## Creating a Task
Run:

python cli.py create "My task" --priority 2 --due 2026-03-30


## Listing Tasks

python cli.py list


## Filtering Tasks

By status:

python cli.py list --status todo


By priority:

python cli.py list --priority 3


## Updating a Task

Change status:

python cli.py status <task_id> done


Change priority:

python cli.py priority <task_id> 4


Change due date:

python cli.py due <task_id> 2026-04-01


## Adding Tags

python cli.py tag <task_id> work


## Removing Tags

python cli.py untag <task_id> work


## Deleting a Task

python cli.py delete <task_id>


## Viewing Statistics

python cli.py stats


## Common Mistakes
- Using the wrong date format (must be YYYY-MM-DD)
- Entering an invalid task ID
- Forgetting required arguments
