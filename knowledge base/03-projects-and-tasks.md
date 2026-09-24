# TaskFlow Help Center: Projects & Task Management

## Creating a Project
1. From your Workspace dashboard, click "+ New Project."
2. Enter a Project name and optional description.
3. Choose a visibility setting: Public (visible to all Workspace members) or Private (invite-only).
4. Click "Create."

You can change a Project's name, description, and visibility later under **Project Settings**.

## Creating a Task
1. Open a Project.
2. Click "+ Add Task."
3. Enter a Task name.
4. Optionally set: Assignee, Due Date, Priority (Low/Medium/High/Urgent), Tags, and Description.
5. Click "Save."

## Assigning Tasks
A Task can be assigned to one person at a time. To assign:
1. Open the Task.
2. Click the Assignee field.
3. Select a Workspace member with access to that Project.

You cannot assign a Task to someone who doesn't have access to the Project — add them to the Project first.

## Subtasks
Tasks can have Subtasks for breaking down larger work. To add a Subtask, open a Task and click "+ Add Subtask" at the bottom of the Task detail view. Subtasks have their own assignee, due date, and status, but do not appear as separate items on the main Project board — they're nested inside their parent Task.

## Task Statuses
Default statuses are: To Do, In Progress, In Review, Done. Workspace Admins can customize these under **Project Settings → Statuses** to match their team's workflow (e.g., adding "Blocked" or "QA").

## Due Dates & Reminders
Setting a due date on a Task automatically enables a reminder notification sent 24 hours before the deadline, and again if the task becomes overdue. Reminder timing cannot currently be customized per-task, but can be turned off entirely per-user under **Profile Settings → Notifications**.

## Recurring Tasks
To make a Task repeat:
1. Open the Task.
2. Click "Set Recurring."
3. Choose a frequency: Daily, Weekly, Monthly, or Custom interval.

When a recurring Task is marked Done, a new instance is automatically created based on the recurrence schedule. Editing a recurring Task's details only affects future instances, not past completed ones.

## Deleting vs. Archiving Tasks
- **Archiving** hides a Task from the active board but keeps it retrievable under **Project → Archived Tasks**. Archiving does not delete any data.
- **Deleting** permanently removes the Task and all its comments/attachments after 30 days in the Trash. Items in Trash can be restored within that 30-day window; after that, deletion is permanent and cannot be reversed.

## Comments & Attachments
Any Project member with access can comment on a Task and attach files (max file size: 25MB per file on Free/Pro plans, 100MB on Business plan and above). @mentioning a teammate in a comment sends them a notification.

## Task Dependencies
Tasks can be marked as dependent on other Tasks (e.g., "Task B can't start until Task A is Done"). To set this, open a Task, go to "Dependencies," and select the Task it depends on. TaskFlow will visually flag a dependent Task if its prerequisite isn't yet complete, but does not currently block status changes — this is a visual indicator only, not an enforced restriction.

## Common Issues
- **"I can't delete this task"** — only the Task creator, Assignee, or a Project/Workspace Admin can delete a Task. Ask one of them, or check if you have edit access to the Project at all.
- **"My recurring task didn't create a new instance"** — new instances are only generated when the Task is marked Done, not simply when the due date passes. Overdue recurring tasks won't auto-regenerate.
- **"I can't find a task I deleted"** — check Project → Trash. If it's been more than 30 days, it cannot be recovered.
