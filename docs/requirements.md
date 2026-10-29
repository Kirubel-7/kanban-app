# Kanban Board Application

## Software Requirements Specification (SRS)

**Version:** 1.0
**Status:** Approved Baseline 
**Project:** Full-Stack Engineering Learning Project

---

## 1. Introduction

### 1.1 Purpose

This document defines the functional and non-functional
requirements for Version 1 of the Kanban Board Application.

It serves as the requirements baseline for system design,
implementation, and testing.

### 1.2 Project Objective

Develop a web-based Kanban application that enables
users to organize tasks into boards and columns,
track progress, and manage their workflow.

The project also serves as a practical full-stack
engineering learning environment.

### 1.3 Version 1 Scope (MVP)

Version 1 will support:

- User registration, login, and logout
- Personal board creation, archiving, restoration and management
- Column creation, editing, ordering, and deletion
- Task creation, editing, ordering, and deletion
- Moving tasks between columns
- Persistent storage of user data
- Ownership-based access control

### 1.4 Out of Scope for Version 1

The following features are deferred to later versions:

- Shared boards and team membership
- Task assignment
- Comments and activity history
- Real-time collaboration
- Notifications
- Advanced role-based permissions

## 2. Functional Requirements

### FR-01: User Authentication

The system shall allow users to register, log in,
and log out.

### FR-02: Board Creation and Viewing

Authenticated users shall be able to create
and view their own boards.

<!-- ### FR-03: Board Management
Board owners shall be able to rename and delete
their boards. -->

### FR-03: Board Management

Board owners shall be able to rename, archive,
and restore their boards.

Archiving a board shall preserve its columns
and tasks while removing it from the active
board list.

Archived boards shall be read-only until restored.

### FR-04: Column Management

Board owners shall be able to create, rename,
reorder, and delete columns.

### FR-05: Task Management

Board owners shall be able to create, edit,
and delete tasks within their active boards.

#### FR-05.1: Task Deletion

- The system shall request confirmation before
  deleting a task.
- Upon confirmation, the system shall permanently
  delete the task.
- The deleted task shall no longer appear on
  the board after successful deletion.
- If deletion fails, the system shall notify
  the user and preserve the task.

### FR-06: Task Movement and Ordering

Board owners shall be able to move tasks between
columns and reorder tasks within a column.

The selected position shall persist after
refreshing the application.

### FR-07: Data Persistence

Successfully saved changes to boards, columns,
and tasks shall remain available across
sessions and application server restarts.

Archiving a board shall preserve its columns,
tasks, and ordering until the board is restored.

### FR-08: Access Control

Users shall only be able to access and modify
boards they own.

## 3. Acceptance Criteria

### FR-01: User Authentication

- AC-01.1: Valid registration details create an account.
- AC-01.2: Duplicate email registration is rejected.
- AC-01.3: Valid credentials allow login.
- AC-01.4: Invalid credentials are rejected.
- AC-01.5: Logout ends the user's authenticated session.

### FR-02: Board Creation

- AC-02.1: A valid board name creates a board.
- AC-02.2: Empty or whitespace-only names are rejected.
- AC-02.3: The created board appears in the owner's board list.
- AC-02.4: The board remains available after refreshing.

<!-- ### FR-03: Board Management
- AC-03.1: The owner can rename a board.
- AC-03.2: Empty board names are rejected.
- AC-03.3: The owner can delete a board.
- AC-03.4: A deleted board is no longer accessible. -->

### FR-03: Board Management

- AC-03.1: The owner can rename an active board.
- AC-03.2: Empty or whitespace-only board names
  are rejected.
- AC-03.3: The system requests confirmation
  before archiving a board.
- AC-03.4: An archived board disappears from
  the active board list.
- AC-03.5: Archived boards remain accessible
  to their owners through an archive view.
- AC-03.6: Archived boards and their contents
  cannot be modified until restored.
- AC-03.7: The owner can restore an archived board.
- AC-03.8: Restoring a board returns it to the
  active board list with its columns, tasks,
  and task ordering preserved.
- AC-03.9: Other users cannot view, archive,
  or restore the owner's boards.

### FR-04: Column Management

- AC-04.1: The owner can create a column.
- AC-04.2: The owner can rename a column.
- AC-04.3: The owner can reorder columns.
- AC-04.4: Column ordering persists after refresh.
<!-- - AC-04.5: The owner can delete a column. -->
- AC-04.5: The owner can delete an empty column.
- AC-04.6: The system rejects deletion of a column
  containing one or more tasks.
- AC-04.7: When deletion is rejected, the column
  and its tasks remain unchanged.
- AC-04.8: The system informs the user that the
  column must be empty before deletion.

### FR-05: Task Management

- AC-05.1: The owner can create a task.
- AC-05.2: The owner can edit a task.
- AC-05.3: Deletion requires confirmation.
- AC-05.4: Confirmed deletion removes the task.
- AC-05.5: Failed deletion displays an error
  and preserves the task.

### FR-06: Task Movement

- AC-06.1: The owner can move tasks between columns.
- AC-06.2: The owner can reorder tasks within a column.
- AC-06.3: The selected position persists after refresh.

### FR-07: Data Persistence

- AC-07.1: Saved changes remain after refresh.
- AC-07.2: Saved data remains after logging out
  and logging back in.

### FR-08: Access Control

- AC-08.1: Unauthenticated users cannot access
  protected boards.
- AC-08.2: Users cannot view another owner's board.
- AC-08.3: Users cannot modify or delete another
  owner's board, columns, or tasks.

## 4. Non-Functional Requirements

<!-- ### NFR-01: Performance
Under a defined test workload, at least 95% of
board-read API requests shall complete within
500 milliseconds for boards containing up to
100 tasks. -->

### NFR-01: Performance

When retrieving a board containing up to 100 tasks,
the API shall achieve a 95th-percentile response
time of 500 milliseconds or less under a workload
of 10 concurrent simulated users.

Testing shall use a documented local environment.
The request rate, test duration, and hardware
configuration shall be recorded before executing
the performance test.

Initial application startup is excluded from
response-time measurements.

### NFR-02: Security

The system shall require authentication for
protected operations and enforce board ownership
on the backend.

Unauthorized requests shall not expose or
modify private board data.

### NFR-03: Reliability

Successfully committed changes shall remain
available after page refresh, re-login, and
application server restart.

### NFR-04: Usability

Core board and task operations shall work
on supported desktop and mobile browsers.

### NFR-05: Maintainability

Core business rules shall be independently
testable without requiring a running web server.

## 5. Assumptions and Constraints

### 5.1 Assumptions

- V1 boards are private and have one owner.
- Users manage their own boards independently.
- Real-time collaboration is not required for V1.
- Each task belongs to exactly one column.
- Each column belongs to exactly one board.

### 5.2 Constraints

- The application shall be web-based.
- V1 shall be developed incrementally by one developer.
- The system shall support desktop and mobile browsers.
- Technology and architecture selections shall be
  justified against project requirements.
- The project shall prioritize maintainability
  and learning over unnecessary complexity.
