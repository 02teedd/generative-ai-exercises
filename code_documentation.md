# Code Documentation Exercise

## Selected Function
parse_task_from_text (from task_parser.py)

---

## Prompt 1: Function Documentation

### Description
This function takes a piece of text and converts it into a structured task. It extracts information like the task title, priority, tags, and due date from the text.

### Parameters
- `text` (string): The input text that contains task details.

### Returns
- A Task object with the extracted values (title, priority, due date, and tags).

### Possible Errors
- If the text format is incorrect, some values may not be extracted.
- Date parsing may fail if the format is invalid.

### Example Usage
```python
task = parse_task_from_text("Finish report @work !3 #tomorrow")
