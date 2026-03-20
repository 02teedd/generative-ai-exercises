# task_manager/storage.md

## Functions / Classes

### **TaskEncoder**
- Custom JSON encoder for `Task` objects.
- Converts Python objects to JSON, including:
  - `priority` → integer value
  - `status` → string
  - Datetime fields (`created_at`, `updated_at`, `due_date`, `completed_at`) → ISO strings.

### **TaskDecoder**
- Custom JSON decoder for `Task` objects.
- Converts JSON back to Python `Task` objects.
- Parses datetime fields from ISO strings.
- Ensures all task attributes (`id`, `title`, `priority`, `status`, `tags`, dates) are restored correctly.

### **TaskStorage**
- Handles storing and retrieving tasks in a JSON file.
- **`__init__`** – Sets storage path and loads existing tasks.
- **`load()`** – Reads JSON file and decodes tasks using `TaskDecoder`.
- **`save()`** – Saves all tasks to JSON using `TaskEncoder`.
- **`add_task(task)`** – Adds a new task and saves.
- **`get_task(task_id)`** – Returns task by ID.
- **`update_task(task_id, **kwargs)`** – Updates task attributes.
- **`delete_task(task_id)`** – Deletes task by ID.
- **`get_all_tasks()`** – Returns all tasks as a list.
- **`get_tasks_by_status(status)`** – Returns tasks filtered by status.
- **`get_tasks_by_priority(priority)`** – Returns tasks filtered by priority.
- **`get_overdue_tasks()`** – Returns tasks past due date and not done.

## Flow
1. On initialization, `TaskStorage` loads tasks from `tasks.json`.
2. Tasks are kept in a dictionary keyed by `task.id`.
3. CRUD operations (`add`, `update`, `delete`, `get`) interact with this dictionary and call `save()` to persist changes.
4. Custom JSON encoder/decoder ensures tasks are correctly serialized/deserialized, including enums and dates.

## Dependencies
- `models.py` → uses `Task`, `TaskPriority`, `TaskStatus`.
- `json`, `os`, `datetime` standard libraries.

## Observations / Questions
- This class abstracts file handling so `TaskManager` doesn’t need to manage JSON directly.
- Could add error handling for concurrent writes if multiple processes use the same file.
- Efficient for small projects; for larger systems, a database might be better.
