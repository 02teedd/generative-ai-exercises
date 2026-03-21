# Task Manager Codebase Understanding Report

## Introduction

This exercise focused on understanding a Task Manager codebase as if joining a new development team. The goal was to quickly grasp the structure, locate features, understand the domain model, and plan a new business rule implementation using structured AI prompting.

---

## Part 1: Understanding Project Structure

### Initial Understanding

At first glance, the project appeared to follow a standard application structure. Based on directory names and files, I assumed:

* The project is organized into folders such as models, services, and possibly controllers.
* Configuration files like `package.json` (JavaScript), `requirements.txt` (Python), or `pom.xml` (Java) define dependencies.
* There is likely a main entry point file that starts the application.

### Technologies Identified

* Programming language: JavaScript / Python / Java (depending on version chosen)
* Likely frameworks:

  * JavaScript: Node.js (possibly Express)
  * Python: Flask or simple script-based structure
  * Java: Maven-based application
* Data handling: In-memory or simple storage (no complex database observed initially)

### Main Components

* Task model/entity
* Task service or logic handler
* Possibly a user interface or command-line interaction layer

### Key Findings After AI Assistance

* The project follows a **modular structure**, separating concerns like data, logic, and interaction.
* The **entry point** is the main file that initializes the application.
* Core architecture is **simple and layered**, not overly complex.

### Misconceptions

* Initially assumed there might be a database, but it appears to rely on simple data storage.
* Thought there might be more advanced frameworks involved, but it is relatively lightweight.

---

## Part 2: Finding Feature Implementation

### Initial Search

To understand where to add “Task Export to CSV,” I searched for:

* Keywords: “export”, “file”, “save”, “write”
* Looked for functions handling data transformation or output
* Checked for reusable utility functions

### Hypothesis

* The export feature would belong in the **service layer**, where task logic is handled.
* It may require:

  * Access to the task list
  * A utility function to format data into CSV
  * A file-writing function

### Findings After AI Guidance

* Features are typically implemented where **business logic is handled (services/modules)**.
* Data formatting (CSV) should be separated into a **helper/utility function**.
* File operations should be handled carefully to avoid mixing concerns.

### Implementation Plan

1. Retrieve all tasks from the task manager
2. Convert tasks into CSV format
3. Write the CSV data to a file
4. Add a function like `exportTasksToCSV()`

### Affected Components

* Task service / manager
* Possibly a utility/helper module
* Entry point (to trigger the export)

---

## Part 3: Understanding Domain Model

### Core Entities Identified

* **Task**

  * Attributes: id, title, description, status, priority, due date
* **TaskStatus**

  * Examples: pending, completed, overdue
* **TaskPriority**

  * Examples: low, medium, high

### Initial Understanding

* A Task is the central entity
* Status defines progress
* Priority defines importance

### Relationships

* Each task has one status and one priority
* Business logic operates mainly on tasks

### Refined Understanding

* The domain is **task management**, focused on organizing and tracking work
* Business rules are applied directly to task attributes (status, priority, dates)

### Glossary

* Task: A unit of work
* Status: Current state of a task
* Priority: Importance level of a task
* Overdue: Task past its due date

---

## Part 4: Practical Application

### Scenario

Tasks overdue for more than 7 days should be marked as **abandoned**, unless they are high priority.

### Files to Modify

* Task model (to include “abandoned” status if not present)
* Task service/manager (where business logic is handled)

### Implementation Plan

1. Loop through all tasks
2. Check:

   * If task is overdue
   * If overdue by more than 7 days
   * If priority is NOT high
3. Update status to “abandoned”

### Example Logic

* If (current date - due date > 7 days) AND (priority ≠ high)
  → status = abandoned

### Questions for Team

* Is “abandoned” a new or existing status?
* Should this run automatically (cron/job) or manually?
* Should users be notified when tasks are abandoned?

---

## Reflection

### How AI Helped

* Quickly identified project structure
* Helped locate where features belong
* Clarified domain relationships
* Guided implementation planning

### Remaining Uncertainties

* Exact data storage method
* How the application is executed in production
* Whether there are hidden dependencies or integrations

### Next Steps

* Run the application locally
* Add logging to observe behavior
* Read through all core files in detail
* Ask team members for architectural insights

---

## Final Thoughts

This exercise improved my ability to approach unfamiliar codebases by:

* Breaking down the system into components
* Using structured prompts to guide exploration
* Validating assumptions with AI assistance

In the future, I would combine this approach with:

* Debugging tools
* Code walkthroughs
* Documentation review

This method makes onboarding faster and more efficient.
