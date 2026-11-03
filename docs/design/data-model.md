
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

### 4.2 User

| Attribute | Role |
|---|---|
| id | Primary key |
| name | Display name |
| email | Required, unique |
| passwordHash | Required, password verifier |

Constraints:
- User email must be unique.
- Plaintext passwords must not be stored.

### 4.3 Column

| Attribute | Role |
|---|---|
| id | Primary key |
| boardId | Foreign key to Board |
| name | Required |
| position | Ordering within Board |

Constraints:
- Each Column belongs to exactly one Board.
- A Column may contain zero or more Tasks.
- A non-empty Column cannot be deleted.

### 4.4 Task

| Attribute | Role |
|---|---|
| id | Primary key |
| columnId | Foreign key to Column |
| title | Required |
| position | Ordering within Column |

Constraints:
- Each Task belongs to exactly one Column.
- Tasks can be moved and reordered.
- Ordering must persist after saving.

## 5. Logical Model Constraints

- All entity identifiers must be unique.
- Foreign-key references must point to valid records.
- Archived Boards and their contents are read-only.
- Column and Task ordering is scoped to the parent.
- Cross-board task movement is excluded from V1
  unless the requirements baseline is revised.

## 6. Modeling Status

- Conceptual model: Defined
- Core logical entities and attributes: Drafted
- Detailed integrity and ordering rules: Pending
- Physical database schema: Pending
