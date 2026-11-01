
# Kanban V1 — Data Model

**Status:** Conceptual Model — Draft
**Related Document:** ../requirements.md

## 1. Core Entities

| Entity | Description |
|---|---|
| User | Registered person who owns boards |
| Board | Workspace that organizes columns |
| Column | Ordered grouping of tasks inside a board |
| Task | Work item belonging to a column |

## 2. Entity Relationships

- User (1) → Board (0..N)
- Board (1) → Column (0..N)
- Column (1) → Task (0..N)

Each Board belongs to exactly one User.
Each Column belongs to exactly one Board.
Each Task belongs to exactly one Column.

## 3. Business Rules

- V1 boards are private and have one owner.
- A board may be active or archived.
- Archived boards are read-only until restored.
- Archiving preserves columns, tasks, and ordering.
- A column can be deleted only when empty.
- Tasks can move between columns of the same board.
- Column and task ordering must persist.
- Only the board owner may modify its contents.


## 4. Logical Data Model (Draft)

### 4.1 Board

| Attribute | Role | Description |
|---|---|---|
| id | PK | Unique board identifier |
| name | Required | Board name |
| ownerId | FK | References User |
| status | Required | Active or Archived |

### Relationship

- Each Board must reference exactly one User.
- One User may own multiple Boards.

### Constraints

- Board name cannot be empty or whitespace-only.
- Board status must be Active or Archived.
- Archived boards cannot be modified until restored.
- Board ownership must be enforced by backend logic.


## 5. Modeling Status

- Conceptual entities: Defined
- Relationships: Defined
- Logical attributes and identifiers: Pending
- Physical database schema: Pending
