# Task Manager CLI - FAQ

## What is this project?
This is a command-line tool that helps you manage tasks using Python.

## How do I create a task?
Use:

python cli.py create "Task name"


## What format should dates be in?
Dates must be in this format:
YYYY-MM-DD (example: 2026-03-30)

## Why am I getting "Task not found"?
The task ID you entered might be incorrect.

## How do I mark a task as done?

python cli.py status <task_id> done


## Can I filter tasks?
Yes:

python cli.py list --status todo


## Where are tasks stored?
Tasks are saved in a file called `tasks.json`.

## What causes errors?
- Wrong date format  
- Incorrect command usage  
- Missing required arguments  
