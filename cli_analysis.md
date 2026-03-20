# My Notes on `cli.py`

## 1. Functions

**`format_task(task)`**  
- Basically takes a task and makes it look nice when printing.  
- Shows status, priority, due date, tags, and when it was created.  
- Uses `TaskStatus` and `TaskPriority` to put symbols like `[ ]` or `!!!`.  
- Handles cases when there’s no due date or no tags.

**`main()`**  
- This is the main thing that runs the CLI.  
- Uses `argparse` to read what command I typed, like `create`, `list`, `status`, etc.  
- Makes a `TaskManager` object and calls the right function depending on the command.  
- Prints the result or errors so I can see what happened.

**`if __name__ == "__main__":`**  
- Just makes sure `main()` runs only if I run `cli.py` directly, not if I import it somewhere else.

---

## 2. Flow

1. I type a command in terminal, like:  
   ```bash
   python cli.py create "My Task" -d "Do this today" -p 2 -u "2026-03-21" -t "work,urgent"
