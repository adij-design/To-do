# AGENT.md --- Personal + College Productivity & Task Tracker

> **Purpose:** This file is the product, design, architecture, and
> implementation brief for Codex. Treat it as the source of truth while
> planning and building this application. Inspect the existing
> repository before changing anything. Preserve working code and adapt
> this specification to the current stack where sensible.

------------------------------------------------------------------------

## 1. Project Overview

Build a modern, responsive productivity web application that combines:

1.  A **Personal Task Manager** for everyday responsibilities and goals.
2.  A **College Task Manager** for assignments, projects, submissions,
    examinations, and academic deadlines.
3.  A **College Timetable and Calendar** that lets students view their
    official schedule by day, week, and month.
4.  An **AI Productivity Agent** that helps users summarize information,
    create and organize tables, plan schedules, and reduce repetitive
    manual work.

The application should feel like a polished, friendly productivity
product---not a traditional, complicated student management portal.

### Product goals

-   Help students understand what they need to do today.
-   Make it easy to plan tasks around their actual college timetable.
-   Keep personal tasks private while making the official timetable
    available to authorized students.
-   Give users a calm, welcoming interface that does not feel
    overwhelming.
-   Use AI to turn time-consuming organizational work into simple,
    reviewable actions.

### Primary modes

**Personal mode** - Private personal dashboard. - Personal tasks,
deadlines, priorities, notes, and tags. - Daily thought / intention. -
Personal productivity overview.

**College mode** - College assignments, projects, presentations,
examinations, and submissions. - Individual college tasks and
deadlines. - Shared official class timetable. - Optional task
association with classmates or group projects, subject to explicit
permissions.

Users must be able to switch between Personal and College modes without
logging out. Switching modes must never mix one student's private data
with another student's data.

------------------------------------------------------------------------

## 2. Important Product Principles

1.  **Clarity before complexity:** show the most useful information
    first.
2.  **One connected ecosystem:** tasks, calendar, timetable, and AI
    should work together.
3.  **User control:** AI may prepare suggestions and actions, but must
    request confirmation before destructive or externally visible
    changes.
4.  **Privacy by design:** personal tasks are private; college timetable
    access is based on verified college/class membership.
5.  **Responsive by default:** create a purposeful desktop layout and a
    carefully adapted mobile layout.
6.  **Real functionality:** do not leave buttons, menus, filters, or
    forms as decorative mockups.
7.  **Honest integration states:** never claim Google, Firebase, or AI
    integrations are connected when credentials or authorization are
    missing.
8.  **Progressive delivery:** establish a polished working core before
    implementing complex integrations.

------------------------------------------------------------------------

## 3. Reference Material and How to Interpret It

Use the supplied materials as complementary references:

### Hand-drawn wireframe 1 --- Main dashboard

Use this as the structural reference: - Header with circular avatar,
user name, dropdown, and an Add Task action. - A large **Daily Thought**
/ thought-of-the-day area where the user can write or customize a
thought, intention, or short note. - A **Need to Do Today** card with a
structured task list/table. - A **College Timetable** card below the
task section.

The wireframe is a layout guide, not a visual style to copy literally.
Convert it into a polished, aligned interface.

### Hand-drawn wireframe 2 --- Add Task form

Use this as the form-content reference: - Task name. - Date /
deadline. - Status. - Priority. - Tags / person association. - Notes /
description. - Clear Save Task and Cancel actions.

### Supplied app UI screenshot --- Visual reference

Use the supplied three-screen mobile UI as the primary visual-language
reference. Recreate its design principles in the productivity app
without copying its health-specific content.

Observe and apply: - Soft pastel gradients and gentle color
transitions. - A calm, airy, friendly visual mood. - Large rounded
panels and cards. - White or translucent surfaces over subtly tinted
backgrounds. - Soft shadows and restrained borders. - Light, decorative
floral / petal geometry used as subtle background texture. - Circular
icon containers and small, clear icons. - Comfortable whitespace and
generous corner radii. - Clear typographic hierarchy with large page
headings and compact supporting labels. - Pill-shaped filters and
controls. - A floating or softly elevated navigation treatment where
appropriate. - Strong contrast for important text and primary actions.

Do not turn the entire app into a collection of gradients. Use pastel
colors as atmosphere and accent; preserve readability and functional
hierarchy.

------------------------------------------------------------------------

## 4. Visual Design System

### 4.1 Overall style

**Style keywords:** minimal, friendly, expressive, calm, premium, soft,
approachable, organized.

The interface should feel warm and personal rather than corporate or
overly technical. Keep the layout uncluttered. Use color to distinguish
sections and states, not as decoration everywhere.

### 4.2 Color palette

Create reusable design tokens / CSS variables. Start with this palette
and tune it against the supplied screenshot:

  -----------------------------------------------------------------------
  Token                   Suggested value         Usage
  ----------------------- ----------------------- -----------------------
  `--background`          `#F8F5FA`               Main app background;
                                                  may be paired with a
                                                  very soft lavender tint

  `--surface`             `#FFFFFF`               Main cards and form
                                                  surfaces

  `--surface-soft`        `#FCF9FD`               Secondary surfaces

  `--text-primary`        `#25212A`               Main headings and task
                                                  text

  `--text-secondary`      `#77717D`               Descriptions, metadata,
                                                  helper text

  `--border`              `#EEE8F0`               Subtle borders and
                                                  dividers

  `--lavender`            `#DCC8F0`               Pastel background /
                                                  accent

  `--mint`                `#CBEAE3`               Soft section tint

  `--pink`                `#F3D5E4`               Soft section tint

  `--peach`               `#F8D6BD`               Soft section tint

  `--primary`             `#29232D`               Primary text-first CTA
                                                  / strong action

  `--accent`              `#B78BD4`               Main accent for
                                                  selected states and
                                                  highlights

  `--success`             `#69A88D`               Completed / success

  `--warning`             `#D9A35F`               Due soon / medium
                                                  attention

  `--danger`              `#D47779`               Overdue / destructive
                                                  states

  `--info`                `#79BBD0`               Informational labels
  -----------------------------------------------------------------------

Suggested atmospheric gradients: - Mint → pale blue for a calm Daily
Thought panel. - Lavender → blush pink for an assistant or welcome
panel. - Pale yellow → peach for a calendar or date-focused panel.

Gradients should be subtle and low contrast. Avoid neon colors, harsh
saturated fills, and strong multi-stop gradients.

### 4.3 Typography

Use **Inter** or **Geist** as the primary sans-serif typeface. Use one
family consistently unless the existing project already has a strong,
accessible type system.

Typography guidance: - Large but restrained page greeting / dashboard
heading. - Medium-weight card titles. - Clear, readable task names. -
Small muted metadata for due dates, tags, and supporting information. -
Avoid excessively thin text for important information. - Use consistent
line heights and a deliberate type scale.

Suggested hierarchy: - Page title: 30--36px desktop, 25--30px mobile. -
Section title: 18--22px. - Task title: 14--16px. - Supporting text:
12--14px. - Small labels: 11--12px, with adequate contrast.

### 4.4 Shapes, spacing, and surfaces

-   Cards: large rounded corners, approximately 22--30px depending on
    size.
-   Inputs and buttons: approximately 12--18px corner radius.
-   Pills / filters: fully rounded.
-   Use soft, diffused shadows sparingly.
-   Prefer subtle 1px borders over heavy outlines.
-   Use a consistent spacing scale (4, 8, 12, 16, 20, 24, 32, 40px).
-   Keep content aligned to a clear grid and use generous whitespace.
-   Avoid excessive dividers and dense tables.

### 4.5 Decorative elements

-   Use subtle petal / floral geometry or abstract translucent shapes
    inspired by the reference screenshot.
-   Keep decoration behind content and at low opacity.
-   Decorative shapes must never reduce text contrast or interfere with
    clicks.
-   Do not add random illustrations, emojis, or unnecessary icons.
-   Use Lucide icons consistently and only where they clarify an action
    or state.

### 4.6 Interaction patterns

Use patterns inspired by the reference UI: - Rounded cards with clear
section headings. - Small circular icon badges. - Pill-shaped tabs and
filters. - Softly elevated profile avatar. - Clear selected states. -
Modal or side drawer for Add/Edit Task. - Gentle hover, focus, pressed,
and transition states. - Toast feedback for successful and failed
actions. - Helpful empty states with one obvious next action.

------------------------------------------------------------------------

## 5. Application Navigation and Main Layout

Create two main working environments: 1. Personal Dashboard. 2. College
Dashboard.

### Header

Include: - Circular profile avatar. - User name and dropdown arrow. -
Personal / College mode selector. - Add Task primary action. - AI
assistant entry point.

The profile dropdown should contain: - Personal Dashboard. - College
Dashboard. - View Class Timetable. - Profile Settings. - Sign out.

The active mode must be visually obvious. Preserve each mode's data when
switching.

### Main dashboard content order

1.  Header / profile.
2.  Daily Thought panel.
3.  Need to Do Today task card.
4.  College Timetable card.
5.  Optional compact productivity summary, if it does not crowd the
    primary experience.
6.  AI assistant access, preferably through a clear assistant panel or
    persistent entry point.

Use a centered desktop content area with a sensible maximum width. Do
not simply stretch a mobile screen to desktop width.

------------------------------------------------------------------------

## 6. Screen 01 --- Dashboard

### 6.1 Daily Thought panel

Create a welcoming banner near the top of the dashboard.

Purpose: - Let users write a daily thought, intention, reminder,
affirmation, or short personal note. - Allow users to edit or customize
it. - Display the saved thought for the selected day. - Provide a simple
edit action. - Keep this panel visually distinct using a subtle pastel
gradient, inspired by the reference screenshot.

Suggested content: - Small eyebrow label: "A thought for today" or
"Daily intention". - Main thought text. - Edit / customize action. -
Optional date context.

Behavior: - Save the user's thought to their own account. - Support
empty state with a gentle writing prompt. - Do not make up personal
thoughts on the user's behalf. A suggested thought can be offered as an
optional AI suggestion and must be editable.

### 6.2 Need to Do Today card

This is the primary functional section.

Heading: **Need to Do Today**

Show today's tasks in a clean table/list hybrid. Each task should
have: - Completion checkbox. - Task name. - Priority. - Status. -
Deadline.

The task name should be the most visually prominent field. Keep columns
aligned on desktop. On mobile, convert each row into a compact card or
stacked layout without hiding essential information.

Suggested task examples for visual testing only: - Complete Branding
Project. - Revise French. - Complete Typography Elements. - Prepare
Design Presentation.

These are placeholder examples, not user data.

### Task status

-   To Do.
-   In Progress.
-   Done.

### Priority

-   Low.
-   Medium.
-   High.

Use restrained color labels: - High: soft red / coral tint. - Medium:
soft amber tint. - Low: soft mint tint.

### Checkbox behavior

When clicked: - Mark the task as Done. - Apply a strikethrough to the
task title. - Update the status label. - Persist the change. - Update
the interface immediately. - Provide an accessible label and keyboard
support.

### Task card actions

-   Add Task button at the bottom or top-right of the card.
-   Filter tabs: Today, Upcoming, Completed, All.
-   Optional search and priority filter if space allows.
-   Keep the card usable with many tasks; use a sensible max-height with
    internal scrolling only if necessary.

### Deadline indicators

Show clear labels such as: - Due today. - Due tomorrow. - Upcoming. -
Overdue. - Completed.

Use the user's local timezone and local date. Do not rely on UTC date
boundaries for day grouping.

------------------------------------------------------------------------

## 7. Screen 02 --- Add / Edit Task

Build a dedicated page, modal, or side drawer. Prefer a spacious modal
or drawer that is comfortable on desktop and becomes a full-screen sheet
on small mobile screens.

### Fields

1.  **Task Name**
    -   Required text field.
    -   Example placeholder: "Complete Branding Project".
2.  **Date / Deadline**
    -   Date picker.
    -   Required for tasks that need a deadline; if optional, clearly
        communicate that it is optional.
    -   Store dates consistently.
3.  **Status**
    -   To Do.
    -   In Progress.
    -   Done.
4.  **Priority**
    -   Low.
    -   Medium.
    -   High.
5.  **Tags**
    -   Support multiple tags.
    -   Example tags: Branding, Typography, French, College, Personal,
        Group Project.
6.  **People / Assignees**
    -   Allow optional person association in College mode.
    -   Only show people the current user is authorized to access.
    -   Do not imply a task is shared merely because a classmate is
        selected.
7.  **Notes / Description**
    -   Multiline text area.
    -   Example: "Complete the logo exploration and prepare three final
        variations."
8.  **Optional Google Calendar sync**
    -   Allow the user to opt into calendar synchronization when
        integration is configured.

### Form actions

-   Cancel.
-   Save Task.

### Form behavior

-   Validate required fields with clear field-level messages.
-   Prevent duplicate submissions while saving.
-   Save to the correct task collection based on the active mode.
-   Close the form only after a successful save.
-   Update the dashboard immediately.
-   Display success or error feedback.
-   Support editing without losing existing values.
-   Confirm before deleting a task.
-   Support keyboard navigation and accessible labels.

------------------------------------------------------------------------

## 8. Screen 03 --- College Timetable and Calendar

Place the College Timetable below the task section on the dashboard,
with a dedicated expanded view available.

### Views

Support: - **Day view:** detailed vertical time-based schedule. - **Week
view:** seven-day overview. - **Month view:** monthly calendar grid with
event indicators.

The user must be able to switch between these views easily. The selected
view should be visually clear.

### Day view

Display: - Selected date. - Day of week. - Start time. - End time. -
Subject / activity name. - Class duration. - Room / classroom, if
provided. - Teacher, if provided. - Lunch break. - Free periods. - Other
scheduled activities.

Prefer a vertical timeline with a clear time rail and event blocks.
Distinguish lunch breaks and free periods with subtle visual treatment.

### Week view

-   Show the days of the selected week.
-   Display classes in a compact, readable weekly schedule.
-   Allow the user to select a day to open its detailed schedule.
-   On mobile, use a horizontally scrollable week strip or a stacked
    agenda.

### Month view

-   Standard monthly calendar grid.
-   Show small event indicators or short subject labels.
-   Selecting a date opens that date's timetable.
-   Clearly indicate today and the selected date.

### Calendar navigation

Include: - Previous / next period. - Today button. - Date picker. - Day
/ Week / Month view selector.

### Timetable source of truth

The user will provide a Google Spreadsheet containing the actual college
timetable.

**Do not invent real subjects, class timings, rooms, teachers, or
holidays.**

Initially, use clearly labeled sample placeholder data only to test the
interface. Keep it isolated from real imported data. Replace it when the
actual spreadsheet structure is provided.

Example placeholder schedule for UI testing only: - 09:00--10:00 ---
Typography. - 10:00--11:00 --- Branding. - 11:00--12:00 --- French. -
12:00--13:00 --- Lunch Break. - 13:00--14:00 --- Design Studio. -
14:00--15:00 --- Practical Session.

These are illustrative values, not an actual college schedule.

### Google Sheets integration

Build a modular integration that can: 1. Read the configured spreadsheet
through an authorized server-side integration. 2. Parse rows and columns
into normalized timetable events. 3. Validate required fields and report
malformed rows. 4. Store or cache imported timetable data in Firestore.
5. Display timetable data in day, week, and month views. 6. Allow
authorized administrators to refresh the imported timetable. 7. Record
the last successful sync time and sync errors.

The exact spreadsheet structure is not yet available. Build a flexible
parser interface and wait for the actual sheet before finalizing column
mappings. Keep spreadsheet ID and configuration in environment
variables. Never expose private credentials in client code.

------------------------------------------------------------------------

## 9. AI Productivity Agent

The AI agent is a core product capability, not a decorative chatbot. It
should help users complete organizational work that would otherwise take
a lot of manual effort.

### 9.1 Main purpose

The assistant should help users: - Summarize tasks, notes, schedules,
and academic information. - Create tables from unstructured notes or
pasted content. - Turn long instructions into actionable task lists. -
Organize tasks by date, priority, status, subject, or category. -
Suggest a realistic daily or weekly plan based on the timetable and
deadlines. - Identify schedule conflicts and overloaded days. -
Summarize upcoming deadlines. - Convert meeting / lecture / project
notes into structured actions. - Draft checklists, study plans, project
plans, and revision schedules. - Find repetitive organizational steps
that could be simplified. - Explain the user's current workload in plain
language.

### 9.2 Example user requests

The interface should be designed to support requests such as: -
"Summarize what I need to finish this week." - "Turn these notes into a
table with task, priority, and deadline." - "Make a revision plan around
my college timetable." - "Which assignments are overdue?" - "Break this
project into smaller tasks." - "Organize these tasks by priority." -
"Find free slots in my timetable for studying." - "Summarize my college
schedule for tomorrow." - "Create a checklist from this assignment
brief." - "Show me all tasks tagged Branding." - "Prepare a weekly
progress summary."

### 9.3 Agent interaction design

Create a friendly assistant experience that matches the visual system: -
A clear AI assistant entry point in the dashboard. - A dedicated
assistant panel, drawer, or page. - A welcoming greeting and suggested
prompt chips. - A readable conversation layout. - Structured responses
with headings, lists, and tables when useful. - A visible indication
when the assistant is processing. - Clear error and retry states. - A
way to review proposed changes before applying them.

Avoid a generic, oversized chatbot interface that takes over the entire
product. The assistant should feel integrated into the task workflow.

### 9.4 Tool / action capabilities

Design the agent around explicit application actions, for example: -
Read the current user's tasks. - Read authorized timetable events. -
Summarize tasks and deadlines. - Generate a proposed task list. -
Generate a table from user-provided content. - Suggest task
priorities. - Propose a schedule using available timetable slots. -
Create or update tasks after user confirmation. - Prepare a calendar
event after user confirmation, if calendar integration is connected.

All operations must enforce the same ownership and access rules as the
normal app.

### 9.5 Confirmation and safety rules

-   The assistant may analyze and suggest without confirmation.
-   Before creating, editing, deleting, sharing, or syncing records,
    show a preview and ask the user to confirm.
-   Never delete tasks or alter the official timetable autonomously.
-   Never share a private task with classmates without explicit user
    approval.
-   Never invent timetable entries, deadlines, or task data.
-   Clearly distinguish saved facts from AI suggestions.
-   Do not expose another user's personal tasks or private information.
-   If AI credentials are not configured, show a clear unavailable /
    setup state; the rest of the app must continue working.
-   Keep AI provider keys on the server, never in browser code.
-   Log tool/action failures safely without storing unnecessary
    sensitive content.

### 9.6 AI implementation architecture

Create a provider-agnostic server-side AI service so the model provider
can be configured later. Keep prompts, tool schemas, validation, and
action execution separate from UI components.

Suggested modules: - `lib/ai/agent.ts` --- orchestration. -
`lib/ai/prompts.ts` --- system and task prompts. - `lib/ai/tools.ts` ---
permitted application tools. - `lib/ai/schemas.ts` --- Zod schemas for
structured outputs. - `lib/ai/permissions.ts` --- ownership and
authorization checks. - `app/api/ai/route.ts` --- authenticated server
endpoint, if using Next.js route handlers.

Use structured outputs for task proposals and tables wherever possible.
Validate AI-generated data before presenting or saving it. Never trust
model output as authorization.

------------------------------------------------------------------------

## 10. Google Calendar Integration

Google Calendar is for each user's own calendar synchronization. It is
not the source of truth for the official college timetable.

Features: - Connect Google account. - Request only the OAuth scopes
required. - Create calendar events from tasks when the user opts in. -
Update an existing event when a synced task's deadline changes. - Store
the Google Calendar event ID on the task. - Prevent duplicate event
creation. - Handle task completion and deletion according to the user's
sync preference. - Continue normal app functionality when Calendar is
not connected.

Suggested sync flow: 1. Save the task in Firestore. 2. If the user
enabled sync and authorized Google Calendar, create the corresponding
event server-side. 3. Store the event ID and sync metadata. 4. Update
the mapped event when the task changes. 5. Handle deletion according to
the selected preference. 6. Report sync errors without losing the task.

Do not treat Google Sheets and Google Calendar as interchangeable: -
Google Sheets = official college timetable source. - Google Calendar =
optional personal task/event synchronization.

------------------------------------------------------------------------

## 11. Authentication, Backend, and Data Architecture

### Recommended stack

Use the existing repository stack if it is already configured and
working. If starting fresh, prefer:

**Frontend** - Next.js App Router. - React. - TypeScript. - Tailwind
CSS. - shadcn/ui. - Lucide React. - React Hook Form. - Zod.

**Backend** - Firebase Authentication. - Cloud Firestore. - Firebase
Storage only if attachments are implemented. - Firebase Cloud Functions
or secure Next.js server routes for privileged operations.

**Integrations** - Google Authentication / OAuth 2.0. - Google Sheets
API. - Google Calendar API. - AI model provider through a server-side
adapter.

### Authentication

Implement: - Google sign-in. - Authentication state persistence. -
Protected dashboard routes. - User profile creation on first login. -
Logout. - Profile settings.

Suggested user fields: - `uid` - `displayName` - `email` - `photoURL` -
`collegeId` - `classId` - `role` - `createdAt` - `updatedAt` -
`lastLoginAt`

Use Firebase UID as the unique user identifier.

### Suggested Firestore structure

``` text
users/{uid}
  - profile fields

users/{uid}/personalTasks/{taskId}
  - title
  - description
  - dueDate
  - status
  - priority
  - tags
  - assignedTo
  - createdAt
  - updatedAt
  - googleCalendarEventId
  - calendarSyncEnabled

users/{uid}/collegeTasks/{taskId}
  - title
  - description
  - dueDate
  - status
  - priority
  - tags
  - assignedTo
  - createdAt
  - updatedAt
  - googleCalendarEventId
  - calendarSyncEnabled

users/{uid}/dailyThoughts/{thoughtId}
  - date
  - content
  - createdAt
  - updatedAt

colleges/{collegeId}
  - collegeName
  - spreadsheetId
  - createdAt
  - updatedAt

colleges/{collegeId}/classes/{classId}
  - className
  - semester
  - section
  - createdAt

colleges/{collegeId}/classes/{classId}/timetable/{eventId}
  - date
  - day
  - subject
  - startTime
  - endTime
  - room
  - teacher
  - type
  - updatedAt
```

College tasks should remain private to their creator by default. If
tasks are shared with classmates, implement explicit membership /
sharing permissions and enforce them in Firestore rules.

### Security rules

Implement and include Firestore security rules in the repository.

Requirements: - Authenticated users can access their own profile. -
Users can read and write only their own personal tasks. - Users can read
and write only their own college tasks unless explicit sharing
permissions are implemented. - Users can read timetable information only
if they belong to the relevant college and class. - Only authorized
administrators can update shared timetable information. - Validate
ownership and allowed fields on writes. - Do not rely on frontend
filtering for privacy.

Keep privileged operations on trusted server-side code. Never expose
Firebase Admin credentials, service account keys, Google client secrets,
or AI provider keys in client bundles.

------------------------------------------------------------------------

## 12. Task Management Logic

Every task should support: - Create. - Read. - Update. - Delete. - Mark
complete. - Change status. - Change priority. - Add / remove tags. - Add
notes. - Set deadline. - Optional assignee / person association. -
Optional Google Calendar sync.

### Categories

**Personal** - Personal activities. - Daily reminders. - Individual
projects.

**College** - Assignments. - Design projects. - Presentations. -
Examinations. - Practical work. - Group projects.

### Deadline grouping

Automatically identify: - Due Today. - Due Tomorrow. - Upcoming. -
Overdue. - Completed.

Use local date and timezone consistently. Make date calculations
testable and isolate them in utility functions.

------------------------------------------------------------------------

## 13. Suggested Component and Folder Architecture

Adapt to the repository's current architecture. Do not force this
structure if a sound structure already exists.

``` text
src/
  app/
    login/
    dashboard/
    personal/
    college/
    timetable/
    assistant/
    settings/
    api/
      ai/
      google/
    layout.tsx

  components/
    layout/
      Header.tsx
      ProfileDropdown.tsx
      ModeSwitcher.tsx

    dashboard/
      DailyThoughtCard.tsx
      ProductivitySummary.tsx

    tasks/
      TaskCard.tsx
      TaskList.tsx
      TaskRow.tsx
      TaskItem.tsx
      AddTaskForm.tsx
      TaskPriority.tsx
      TaskStatus.tsx
      TaskFilters.tsx

    timetable/
      TimetableCard.tsx
      DailyTimetable.tsx
      WeeklyTimetable.tsx
      MonthlyCalendar.tsx
      TimetableEvent.tsx
      DateNavigation.tsx
      CalendarViewSwitcher.tsx

    assistant/
      AssistantPanel.tsx
      ChatMessage.tsx
      SuggestedPrompts.tsx
      ActionPreview.tsx

    ui/

  lib/
    firebase.ts
    auth.ts
    firestore.ts
    googleCalendar.ts
    googleSheets.ts
    ai/
      agent.ts
      prompts.ts
      tools.ts
      schemas.ts
      permissions.ts

  hooks/
    useAuth.ts
    useTasks.ts
    useTimetable.ts
    useDailyThought.ts

  types/
    user.ts
    task.ts
    timetable.ts
    ai.ts

  utils/
    date.ts
    taskFilters.ts
    timetableParser.ts

  styles/
    tokens.css

firestore.rules
.env.example
README.md
AGENT.md
```

------------------------------------------------------------------------

## 14. Responsive Design Requirements

### Desktop

-   Centered content with a comfortable maximum width.
-   Header with profile / mode switcher and primary actions.
-   Daily Thought panel near the top.
-   Task card above the timetable.
-   Table-like task layout with aligned columns.
-   Day / Week / Month calendar controls.
-   AI assistant accessible without obscuring the main dashboard.

### Tablet

-   Reduce horizontal spacing.
-   Keep task columns readable or adapt to compact rows.
-   Allow calendar week view to scroll horizontally when needed.

### Mobile

-   Single-column layout.
-   Compact header and touch-friendly controls.
-   Task rows become stacked cards.
-   Avoid horizontal overflow.
-   Calendar week view may scroll horizontally.
-   Day view remains readable.
-   Forms become full-screen sheets or drawers.
-   Assistant panel becomes a dedicated screen or bottom sheet.
-   Ensure touch targets are comfortably sized.

Test at common viewport sizes. Do not simply shrink the desktop layout.

------------------------------------------------------------------------

## 15. Accessibility and Quality

-   Use semantic HTML and accessible component patterns.
-   Provide labels for all inputs.
-   Support keyboard navigation and visible focus states.
-   Ensure sufficient text contrast on pastel surfaces.
-   Do not communicate task status through color alone.
-   Respect reduced-motion preferences.
-   Provide loading, empty, success, and error states.
-   Avoid layout shifts when data loads.
-   Use optimistic updates only where rollback/error handling is
    implemented.
-   Validate forms on both client and server where applicable.
-   Keep components typed and reusable.
-   Avoid unnecessary dependencies.

------------------------------------------------------------------------

## 16. Development Phases and Priorities

Build in this order. Keep the app runnable at the end of each phase.

### Phase 0 --- Repository inspection

-   Inspect files, package scripts, framework, existing components,
    styles, and backend configuration.
-   Identify what is already implemented.
-   Do not overwrite working code or replace the stack without a clear
    reason.
-   Report assumptions and missing credentials.

### Phase 1 --- Design system and frontend core

Build: - Color and typography tokens. - App shell and header. - Profile
dropdown. - Personal / College mode switcher. - Daily Thought panel. -
Need to Do Today card. - Task table / responsive task rows. - Add / Edit
Task modal or drawer. - College Timetable card. - Day / Week / Month
view controls. - AI assistant entry point and initial UI. - Responsive
desktop, tablet, and mobile layouts.

Use clearly labeled placeholder data while backend work is not ready.

### Phase 2 --- Task and thought behavior

-   Implement task create, read, update, delete.
-   Implement checkbox completion.
-   Implement status and priority changes.
-   Implement filters and deadline grouping.
-   Implement Daily Thought editing and persistence.
-   Ensure Personal and College data remain separate.

### Phase 3 --- Firebase authentication and Firestore

-   Configure Firebase.
-   Implement Google login and logout.
-   Create / update user profile.
-   Protect routes.
-   Implement Firestore task and thought persistence.
-   Add real-time listeners where appropriate.
-   Add Firestore security rules.
-   Test ownership and access restrictions.

### Phase 4 --- Timetable and Google Sheets

-   Wait for the actual spreadsheet structure.
-   Implement the parser against the real sheet.
-   Validate imported rows.
-   Store normalized timetable events.
-   Implement day, week, and month data views.
-   Add authorized refresh and sync status.

### Phase 5 --- Google Calendar

-   Implement OAuth authorization.
-   Create, update, and map events.
-   Prevent duplicates.
-   Handle task deletion and completion according to user preference.
-   Handle disconnected and failed sync states.

### Phase 6 --- AI Productivity Agent

-   Implement secure server-side AI provider adapter.
-   Add task and timetable read tools.
-   Add summarization and table-generation workflows.
-   Add task planning and schedule suggestions.
-   Add structured action previews.
-   Require confirmation before any data mutation.
-   Enforce user ownership and authorization in every tool.
-   Document required AI credentials.

### Phase 7 --- Testing and refinement

Test: - Login / logout. - Personal / College switching. - Daily Thought
save and edit. - Task create, edit, delete, and completion. - Status and
priority updates. - Today / Upcoming / Completed / All filters. - Local
date and timezone behavior. - Timetable day / week / month navigation. -
Empty, loading, error, and success states. - Google Sheets import and
refresh. - Google Calendar event synchronization and duplicate
prevention. - AI summaries, generated tables, and proposed task
actions. - AI confirmation and permission boundaries. - Firestore
security rules. - Mobile responsiveness and keyboard accessibility.

------------------------------------------------------------------------

## 17. Functional Acceptance Criteria

The initial product is successful when a student can:

1.  Open the app and sign in with Google.
2.  View their Personal Dashboard.
3.  Switch to College mode without logging out.
4.  Write and edit a Daily Thought.
5.  View today's tasks in a clear task table/list.
6.  Add a task with name, deadline, status, priority, tags, and notes.
7.  Edit and delete tasks.
8.  Mark a task complete and see the status update immediately.
9.  Filter tasks by Today, Upcoming, Completed, and All.
10. View the college timetable in Day, Week, and Month formats.
11. Navigate dates and return to Today.
12. Access the official timetable only when authorized.
13. Optionally synchronize tasks with Google Calendar.
14. Ask the AI agent to summarize tasks and schedules.
15. Ask the AI agent to convert notes into a structured table or
    checklist.
16. Review and approve proposed task changes before they are applied.
17. Use the app on desktop and mobile without broken layouts.

### Data and privacy acceptance criteria

-   Personal tasks are visible only to their owner.
-   College tasks are private to their creator by default.
-   Shared timetable data is visible only to authorized class members.
-   Only authorized administrators can update official timetable data.
-   AI tools cannot bypass these permissions.
-   No integration is described as connected unless it has been
    successfully configured and authorized.

------------------------------------------------------------------------

## 18. Development Rules for Codex

1.  Start by inspecting the existing repository.
2.  Summarize the existing stack and implementation before making
    significant changes.
3.  Make a short implementation plan and then proceed.
4.  Reuse existing configuration and components when appropriate.
5.  Do not delete existing working functionality.
6.  Prioritize a polished, usable dashboard before complex integrations.
7.  Every visible interactive control must perform a real action.
8.  Do not leave fake buttons or misleading integration states.
9.  Use TypeScript and reusable components.
10. Use Zod for important input and AI output validation.
11. Keep secrets in environment variables and server-side code.
12. Keep Personal and College task data separate.
13. Enforce security in Firestore rules and trusted server code, not
    only in the UI.
14. Clearly label sample timetable data as placeholder data.
15. Do not invent the actual college timetable.
16. Ask for the real Google Spreadsheet structure when timetable
    integration reaches that phase.
17. For AI changes to user data, show a preview and request
    confirmation.
18. Handle loading, empty, success, and error states.
19. Run available lint, type-check, test, and build commands before
    declaring completion.
20. Fix errors where possible and document anything that remains blocked
    by missing credentials or authorization.

------------------------------------------------------------------------

## 19. Environment Variables and Setup Documentation

Create `.env.example` with placeholder variable names only. Never commit
real secrets.

Potential configuration (adapt to the chosen Firebase and Google setup):

``` env
NEXT_PUBLIC_FIREBASE_API_KEY=
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=

GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REDIRECT_URI=

GOOGLE_SHEETS_SPREADSHEET_ID=
GOOGLE_SHEETS_RANGE=

AI_PROVIDER=
AI_API_KEY=
```

Use only the variables needed by the implementation. Public Firebase web
configuration may be exposed as intended by Firebase, but privileged
credentials and private API keys must remain server-side.

Update `README.md` with: - Local development instructions. - Firebase
project setup. - Google OAuth setup. - Google Sheets access and
spreadsheet configuration. - Google Calendar authorization. - AI
provider setup. - Firestore rules deployment. - Any remaining manual
setup steps.

------------------------------------------------------------------------

## 20. Final Product Direction

The final application should combine the simplicity of a daily planner,
the usefulness of a college timetable, and the productivity of an AI
assistant.

The main experience should answer three questions immediately:

1.  **What is important today?** --- Daily Thought and Need to Do Today.
2.  **Where do I need to be and when?** --- College Timetable with day,
    week, and month views.
3.  **How can I get this done faster?** --- AI Productivity Agent for
    summaries, tables, planning, and confirmed actions.

The visual experience should remain faithful to the supplied reference:
soft pastel atmosphere, rounded white surfaces, subtle gradients, gentle
decorative geometry, clean typography, and generous spacing. The result
must be original to this productivity product, fully usable, accessible,
responsive, secure, and built for future growth.

**Do not stop at a static mockup. Build the working product
incrementally, verify each phase, and clearly document any feature that
still requires external credentials, data, or user authorization.**
