# models.py Analysis

## Overview
This file defines the core data structures for the Task Manager application. It handles task properties, statuses, and priorities. The main purpose is to represent tasks as objects that the CLI or other parts of the app can interact with.

---

## Classes & Functions

### 1. TaskPriority (Enum)
- Defines task priorities as LOW, MEDIUM, HIGH, URGENT.
- Each priority has a numeric value (1–4) to make sorting or comparisons easier.

### 2. TaskStatus (Enum)
- Defines possible states for a task: TODO, IN_PROGRESS, REVIEW, DONE.
- Helps track task progress consistently.

### 3. Task
Represents a single task in the system.

#### Attributes
- `id` → Unique identifier generated using `uuid`.
- `title` → Title of the task.
- `description` → Optional detailed description.
- `priority` → TaskPriority enum, default is MEDIUM.
- `status` → TaskStatus enum, default is TODO.
- `created_at` → Timestamp when task is created.
- `updated_at` → Timestamp of last update.
- `due_date` → Optional due date.
- `completed_at` → Timestamp when task was completed.
- `tags` → Optional list of tags.

#### Methods
- `update(**kwargs)` → Updates task attributes dynamically and refreshes `updated_at`.
- `mark_as_done()` → Sets task status to DONE and updates `completed_at` and `updated_at`.
- `is_overdue()` → Returns True if due date passed and task is not DONE, else False.

---

## Flow
1. When a task is created, it gets a unique ID and timestamps.
2. Updates to the task go through the `update()` method.
3. Task completion is handled by `mark_as_done()`.
4. The `is_overdue()` method checks if a task is past its due date.

---

## Dependencies
- Uses `datetime` for timestamps.
- Uses `uuid` to generate unique IDs.
- Uses `Enum` for TaskPriority and TaskStatus.

---

## Observations / Questions
- The file is self-contained: mostly data definitions and basic logic.
- Could consider validating input types in `update()` to avoid accidental mistakes.
- Works closely with `cli.py` to manipulate and display tasks.
