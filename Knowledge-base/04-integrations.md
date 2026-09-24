# TaskFlow Help Center: Integrations

## Available Integrations
TaskFlow currently supports native integrations with:
- Slack
- Google Calendar
- Google Drive
- Zoom
- GitHub

Integrations are managed under **Workspace Settings → Integrations**. Only Workspace Admins and Owners can connect or disconnect integrations.

## Slack Integration
The Slack integration sends TaskFlow notifications (task assignments, due date reminders, @mentions) to a Slack channel of your choice.

**Setup:**
1. Go to **Workspace Settings → Integrations → Slack**.
2. Click "Connect Slack."
3. Log in to your Slack workspace and authorize TaskFlow's requested permissions.
4. Choose which Slack channel should receive notifications.

**Common issue — "Slack notifications stopped working":** This is almost always caused by the Slack authorization token expiring or being revoked (e.g., a Slack workspace admin removed the app, or the connecting user's Slack account was deactivated). Fix: go to Integrations → Slack and click "Reconnect." If the issue persists after reconnecting, it may indicate a Slack-side permissions restriction set by the customer's own Slack admin — this requires the customer's Slack administrator to review app permissions on their end, which TaskFlow support cannot do on their behalf.

## Google Calendar Integration
Syncs Task due dates to a connected Google Calendar as calendar events. This is a one-way sync (TaskFlow → Google Calendar); editing the event in Google Calendar does not update the Task in TaskFlow.

**Setup:**
1. Go to **Workspace Settings → Integrations → Google Calendar**.
2. Click "Connect" and authorize with your Google account.
3. Select which Projects should sync to your calendar.

Only Tasks with a due date set will appear on the calendar. Tasks without a due date are not synced.

## Google Drive Integration
Allows attaching Google Drive files directly to Tasks (instead of uploading a copy). Requires connecting a Google account under Integrations. Permissions on the Drive file itself are not changed by TaskFlow — if a teammate doesn't already have access to the Drive file, attaching it in TaskFlow does not grant them access. The file owner must share it separately in Google Drive.

## Zoom Integration
Allows scheduling a Zoom meeting directly from a Task and automatically attaching the meeting link. Requires connecting a Zoom account (Pro Zoom account or higher required by Zoom, not a TaskFlow limitation).

## GitHub Integration
Links GitHub commits and pull requests to Tasks by referencing the Task ID in a commit message or PR description (e.g., "Fixes TASK-482"). When linked, the Task will show a reference to the related commit/PR. This integration is currently read-only — TaskFlow does not create GitHub issues automatically.

## Disconnecting an Integration
Go to **Workspace Settings → Integrations**, find the integration, and click "Disconnect." This stops all syncing immediately but does not delete data already synced (e.g., previously created calendar events remain in Google Calendar).

## API Access
TaskFlow offers a REST API for custom integrations, available on Business plan and above. API keys are generated under **Workspace Settings → API**. Full API documentation is available separately at developers.taskflow.com. Note: the AI assistant does not have access to full API technical documentation — for API-specific development questions, please escalate to a human support/developer relations contact.
