# task_manager/task_parser.md

## Functions / Classes

### **parse_task_from_text(text)**
- Parses free-form text into a `Task` object.
- **Arguments**: 
  - `text` → a string describing a task, e.g., `"Buy milk @shopping !2 #tomorrow"`
- **Flow**:
  1. Set default task properties (`title`, `priority=MEDIUM`, `due_date=None`, `tags=[]`).
  2. Extract priority markers:
     - `!N` (1–4) or `!low`, `!medium`, `!high`, `!urgent`.
     - Remove priority from title and assign corresponding `TaskPriority`.
  3. Extract tags marked with `@tag` and remove them from title.
  4. Extract date markers `#date`:
     - Supports `today`, `tomorrow`, `next_week`, weekday names, or `YYYY-MM-DD`.
     - Converts to `datetime` object.
  5. Trim whitespace from title.
  6. Create a new `Task` object and assign parsed priority, due date, and tags.
- **Returns**: `Task` object with parsed properties.

### **get_next_weekday(current_date, weekday)**
- Helper function to find the next occurrence of a specific weekday.
- **Arguments**:
  - `current_date` → `datetime` object representing today
  - `weekday` → integer 0–6 (Monday=0, Sunday=6)
- **Returns**: `datetime` object of the next matching weekday

## Dependencies
- `models.py` → uses `Task`, `TaskPriority`, `TaskStatus`.
- `datetime` → for due dates
- `re` → regex parsing for priority, tags, and dates

## Observations / Questions
- Flexible parser supporting tags, priorities, and due dates.
- Handles both textual (tomorrow, monday) and numeric / date formats.
- Could be extended for more natural language parsing (e.g., "in 3 days").
