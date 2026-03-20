# task_manager.py Analysis

## Functions / Methods

### `__init__(self, storage_path="tasks.json")`
- Initializes the `TaskManager` and sets up a storage system using `TaskStorage`.
- Default storage file is `tasks.json`.

### `create_task(self, title, description="", priority_value=2, due_date_str=None, tags=None)`
- Creates a new `Task` object.
- Converts priority from integer to `TaskPriority` Enum.
- Parses the due date string if provided.
- Saves the task in storage and returns its ID.

### `list_tasks(self, status_filter=None, priority_filter=None, show_overdue=False)`
- Returns tasks based on filters:
  - `show_overdue=True` returns only overdue tasks.
  - `status_filter` filters by task status.
  - `priority_filter` filters by task priority.
  - No filters: returns all tasks.

### `update_task_status(self, task_id, new_status_value)`
- Updates a task’s status by task ID.
- If marking as DONE, also sets the completion timestamp.

### `update_task_priority(self, task_id, new_priority_value)`
- Updates a task’s priority.

### `update_task_due_date(self, task_id, due_date_str)`
- Updates a task’s due date from a string formatted as `YYYY-MM-DD`.

### `delete_task(self, task_id)`
- Removes a task from storage.

### `get_task_details(self, task_id)`
- Returns the task object for a given ID.

### `add_tag_to_task(self, task_id, tag)` / `remove_tag_from_task(self, task_id, tag)`
- Adds or removes tags from a task.
- Saves the updated task.

### `get_statistics(self)`
- Returns statistics including:
  - Total tasks
  - Tasks by status
  - Tasks by priority
  - Overdue tasks
  - Tasks completed in the last 7 days

---

## Flow
1. Tasks are created with `create_task()` and stored in `TaskStorage`.
2. Users can list tasks with filters or see overdue tasks.
3. Tasks can be updated (status, priority, due date) or deleted.
4. Tags can be managed for individual tasks.
5. Statistics can be retrieved to summarize tasks by status, priority, and completion.

---

## Dependencies
- `models.py`: For `Task`, `TaskStatus`, and `TaskPriority`.
- `storage.py`: For `TaskStorage` class to save/load tasks.
- `datetime` and `timedelta`: For handling dates and overdue calculations.
- `argparse`: Not used directly in this class, but relevant for CLI integration.

---

## Observations / Questions
- TaskManager is a central controller that interacts with both `models` and `storage`.
- It ensures that business logic (status updates, completion timestamps, overdue checks) is separate from CLI and storage.
- Error handling for invalid dates exists, but could be improved for user feedback.
- Could be extended with more complex filters or task search functionality.
