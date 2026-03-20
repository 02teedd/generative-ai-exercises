# task_manager/task_list_merge.md

## Functions / Classes

### **merge_task_lists(local_tasks, remote_tasks)**
- Merges two dictionaries of tasks (`local_tasks` and `remote_tasks`) with conflict resolution.
- **Arguments**:
  - `local_tasks`: `{task_id: Task}` dictionary from local source
  - `remote_tasks`: `{task_id: Task}` dictionary from remote source
- **Returns**: tuple of
  1. `merged_tasks`: all tasks combined
  2. `to_create_remote`: tasks only in local that need to be added to remote
  3. `to_update_remote`: tasks in both sources but remote needs updating
  4. `to_create_local`: tasks only in remote that need to be added locally
  5. `to_update_local`: tasks in both sources but local needs updating

- **Flow**:
  1. Collect all unique task IDs from both sources.
  2. For each task ID:
     - If only in local → add to remote.
     - If only in remote → add to local.
     - If in both → call `resolve_task_conflict` to handle conflicts.

### **resolve_task_conflict(local_task, remote_task)**
- Resolves differences between two versions of the same task.
- **Logic**:
  - Start with a copy of the local task as base.
  - Most recent update wins for `title`, `description`, `priority`, `due_date`.
  - Completed status (`DONE`) overrides non-completed.
  - Tags are merged (union of local and remote tags).
  - Updates flags (`should_update_local`, `should_update_remote`) to indicate which side needs updating.
  - Updates `updated_at` timestamp to the latest among the two tasks.
- **Returns**: tuple `(merged_task, should_update_local, should_update_remote)`  

## Dependencies
- `models.py` → uses `TaskStatus`, `TaskPriority`.
- `copy` → used for `deepcopy` to safely merge tasks.

## Observations / Questions
- Ensures both local and remote task lists are synchronized intelligently.
- Handles conflicts using timestamps and completion status.
- Could be extended for additional conflict resolution strategies (e.g., priority-based or user-prompted merges).
