# Product Requirements Document: Personal Project Tracker

| Field | Value |
|---|---|
| Document status | Draft |
| Version | 0.1 |
| Created | 2026-10-19 (Day 1 of the 30-day .NET build-and-ship challenge) |
| Product type | Responsive web application |

> **How to read this document:** A PRD describes *what* the product must do and *why*. It does not decide *how* to build it. Technical choices such as the database, hosting, authentication, and architecture are listed as open questions in Section 8, to be decided later.

---

## 1. Project Overview

Personal Project Tracker is a responsive web application for one person who wants to organize personal goals and everyday projects. It offers one place to:

- organize work into **projects**,
- manage **tasks** and their **due dates**, and
- see **what needs attention next** through Today, Upcoming, and Overdue views.

Reminders appear **only inside the application**. The product does not send email, browser, or push notifications.

**Product promise:** *One place to organize projects, manage tasks and deadlines, and identify what needs attention next.*

---

## 2. Problem Statement

People managing personal goals and everyday projects **forget tasks and deadlines**. When tasks are kept in their heads, on paper, or across several unconnected tools, it is hard to answer three questions:

1. What do I need to do today?
2. What is coming up soon?
3. What have I already missed?

Without clear answers, tasks slip, deadlines pass unnoticed, and it is hard to tell how far along each project is.

---

## 3. Target User

**Primary user:** An individual managing personal goals and everyday projects.

| Characteristic | Description |
|---|---|
| Who | One person managing their own work (not a team) |
| What they manage | Personal goals and everyday projects, each broken into tasks |
| Main pain point | Forgetting tasks and deadlines |
| Devices | Desktop and mobile web browsers |
| What they need | A quick way to capture tasks, set deadlines, and see what needs attention |

> **Why this matters:** Designing for one individual keeps Version 1 small. Features for multiple people, such as sharing, permissions, and assigning tasks, are out of scope (see Section 7).

---

## 4. Goals and Success Criteria

### 4.1 Goals

| # | Goal |
|---|---|
| G1 | Give the user one place to organize projects and their tasks. |
| G2 | Help the user keep track of deadlines so tasks are not forgotten. |
| G3 | Show the user what needs attention next (Today, Upcoming, Overdue). |
| G4 | Show how far along each project is. |
| G5 | Keep the user's data safe between sessions. |
| G6 | Work well on both desktop and mobile browsers. |

### 4.2 Success Criteria

Version 1 is successful when **all** of the following are true:

1. All nine must-have features in Section 5 are implemented.
2. Every acceptance criterion in Section 6 passes.
3. A user can create a project, add tasks with due dates, and find those tasks in the correct deadline view without help.
4. Data created before closing the application is still there after reopening it.
5. Core workflows (managing projects and tasks, viewing deadline views, checking progress) can be completed on both a desktop browser and a mobile browser.
6. When input is invalid or a save fails, the user receives a message explaining what went wrong.

---

## 5. MVP Features and Priorities

All features below are **Must Have** for Version 1. Without any one of them, the product promise is not met.

| ID | Feature | Priority | Supports goal |
|---|---|---|---|
| F1 | Create, view, edit, and delete projects | Must Have | G1 |
| F2 | Create, view, edit, and delete tasks | Must Have | G1 |
| F3 | Associate tasks with projects | Must Have | G1, G4 |
| F4 | Set optional task due dates | Must Have | G2 |
| F5 | Mark tasks complete or incomplete | Must Have | G2, G4 |
| F6 | Show Today, Upcoming, and Overdue task views | Must Have | G2, G3 |
| F7 | Calculate project progress from completed tasks | Must Have | G4 |
| F8 | Persist data after the application closes and reopens | Must Have | G5 |
| F9 | Provide a responsive, usable interface on desktop and mobile | Must Have | G6 |

### Suggested build order

Features depend on each other, so a sensible build order is:

1. **F1 → F2 → F3** — Projects and tasks are the core data. Everything else builds on them.
2. **F8** — Persistence should be in place early so later features are tested against saved data.
3. **F4 → F5** — Due dates and completion status are needed before the views and progress can work.
4. **F6 → F7** — Deadline views and progress use the data from the steps above.
5. **F9** — Responsiveness should be checked throughout, with a final review at the end.

> This is a suggested order for learning and delivery. It is not a requirement.

---

## 6. User Stories and Acceptance Criteria

User stories use the format: *As a user, I want [action] so that [benefit].*

### US1 — Manage projects (F1)

**As a user, I want to create, view, edit, and delete projects so that I can organize my goals and everyday work.**

Acceptance criteria:
- [ ] I can create a project by entering a name.
- [ ] A project name is required.
- [ ] A project name that contains only whitespace is rejected.
- [ ] When a project name is invalid, I see a message explaining why.
- [ ] I can view a list of my projects.
- [ ] I can edit a project's name, and the same validation rules apply.
- [ ] I can delete a project.

### US2 — Manage tasks (F2)

**As a user, I want to create, view, edit, and delete tasks so that I can track the work I need to do.**

Acceptance criteria:
- [ ] I can create a task by entering a title.
- [ ] A task title is required.
- [ ] A task title that contains only whitespace is rejected.
- [ ] When a task title is invalid, I see a message explaining why.
- [ ] I can view my tasks.
- [ ] I can edit a task, and the same validation rules apply.
- [ ] I can delete a task.

### US3 — Associate tasks with projects (F3)

**As a user, I want to associate tasks with a project so that related work is grouped together.**

Acceptance criteria:
- [ ] I can associate a task with a project.
- [ ] When I view a project, I can see the tasks associated with it.

### US4 — Set optional due dates (F4)

**As a user, I want to optionally set a due date on a task so that I know when it needs to be done.**

Acceptance criteria:
- [ ] I can set a due date on a task.
- [ ] I can save a task without a due date.
- [ ] I can change or remove a task's due date.

### US5 — Mark tasks complete or incomplete (F5)

**As a user, I want to mark tasks complete or incomplete so that I can track what is finished.**

Acceptance criteria:
- [ ] I can mark an incomplete task as complete.
- [ ] I can mark a complete task as incomplete.
- [ ] Changing a task's completion status updates the deadline views and project progress.

### US6 — See what needs attention (F6)

**As a user, I want Today, Upcoming, and Overdue views so that I can see what needs attention next.**

Acceptance criteria:
- [ ] **Today** shows incomplete tasks due on the current date.
- [ ] **Upcoming** shows incomplete tasks due after today.
- [ ] **Overdue** shows incomplete tasks with due dates before today.
- [ ] Tasks without due dates are excluded from the Today, Upcoming, and Overdue views.
- [ ] Completed tasks are excluded from the Today, Upcoming, and Overdue views.

Example, assuming today is 2026-10-19:

| Task | Due date | Complete? | Appears in |
|---|---|---|---|
| A | 2026-10-19 | No | Today |
| B | 2026-10-25 | No | Upcoming |
| C | 2026-10-15 | No | Overdue |
| D | 2026-10-15 | Yes | None (completed) |
| E | No due date | No | None (no due date) |

### US7 — See project progress (F7)

**As a user, I want to see each project's progress so that I know how close it is to being finished.**

Acceptance criteria:
- [ ] Project progress is calculated as **completed tasks ÷ total tasks** for that project.
- [ ] A project with no tasks displays **0%** progress.
- [ ] Progress updates when tasks are added, deleted, completed, or marked incomplete.

Example:

| Project | Completed tasks | Total tasks | Progress |
|---|---|---|---|
| Garden | 3 | 4 | 75% |
| Reading list | 0 | 5 | 0% |
| New project | 0 | 0 | 0% |

### US8 — Keep my data (F8)

**As a user, I want my data saved so that nothing is lost when I close and reopen the application.**

Acceptance criteria:
- [ ] Projects and tasks I create are still present after restarting the application.
- [ ] Edits, deletions, due dates, and completion status changes persist after restarting the application.
- [ ] When a save fails, I see a message explaining that my change was not saved.

### US9 — Use it on any device (F9)

**As a user, I want the application to work on desktop and mobile browsers so that I can manage my tasks wherever I am.**

Acceptance criteria:
- [ ] All features in this document can be used in a desktop browser.
- [ ] All features in this document can be used in a mobile browser.
- [ ] The layout adapts to the screen size, and content remains readable and usable.

### Cross-cutting acceptance criteria

These apply to every user story:
- [ ] Validation errors provide useful feedback that tells the user what to fix.
- [ ] Save errors provide useful feedback that tells the user the change was not saved.

---

## 7. Out-of-Scope Features

The following are **not** part of Version 1. Listing them explicitly prevents scope creep and keeps the 30-day timeline realistic.

| Feature | Reason it is out of scope |
|---|---|
| Native mobile app | The product is a responsive web application that works in mobile browsers. |
| Email and browser notifications | Reminders are in-app only. |
| Push notifications | Reminders are in-app only. |
| Team collaboration | The target user is one individual. |
| AI-generated tasks | Not needed to solve the core problem. |
| Calendar integrations | Not needed to solve the core problem. |
| Advanced analytics | Project progress (F7) is the only reporting in Version 1. |
| Payments | Not part of the Version 1 product. |

---

## 8. Assumptions and Open Questions

### 8.1 Assumptions

These are treated as true for Version 1. If any turn out to be wrong, this document should be updated.

| # | Assumption |
|---|---|
| A1 | The application is used by one individual. |
| A2 | Users access the application through modern desktop and mobile web browsers. |
| A3 | Due dates are calendar dates. The acceptance criteria compare dates (before, on, or after today), not times of day. |
| A4 | "Reminders" means the Today, Upcoming, and Overdue views inside the application. |

### 8.2 Open Questions — Technical decisions

These have deliberately **not** been decided in this PRD.

| # | Question |
|---|---|
| Q1 | **Authentication:** Does the application need user accounts and sign-in? If so, how will users sign in? |
| Q2 | **Database:** Where and how will data be stored to meet the persistence requirement (F8)? |
| Q3 | **Hosting:** Where will the application run — locally only, or deployed online? |
| Q4 | **Architecture:** How will the .NET application be structured (for example, which web framework, and how front end and back end are organized)? |

### 8.3 Open Questions — Product behavior

These details are not specified by the requirements and need a decision before or during implementation.

| # | Question |
|---|---|
| Q5 | Must every task belong to a project, or can a task exist without a project? |
| Q6 | Can a task belong to more than one project, or only one? |
| Q7 | What happens to a project's tasks when the project is deleted? Should the user be asked to confirm? |
| Q8 | Should deleting a task require confirmation? |
| Q9 | Which time zone defines "today" — the user's device time zone or another source? |
| Q10 | How should progress percentages be rounded and displayed (for example, 1 of 3 = 33% or 33.3%)? |
| Q11 | Are there maximum lengths for project names and task titles? |
| Q12 | Should project names be unique? |
| Q13 | Can a due date be set in the past when creating or editing a task? |
| Q14 | Do tasks or projects have any fields beyond name/title, due date, and completion status (for example, a description)? |
| Q15 | In what order should tasks appear in each view (for example, by due date or by creation order)? |
| Q16 | Which screen sizes and browsers must be tested to confirm "responsive and usable" (F9)? |
