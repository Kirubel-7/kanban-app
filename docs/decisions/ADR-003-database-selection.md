
# ADR-003: Database Technology Selection

**Status:** Accepted
**Date:** 2026-11-05

## Context

Kanban V1 requires persistent storage for Users,
Boards, Columns, and Tasks.

The data model contains well-defined relationships,
ownership rules, ordering constraints, and
transactional operations.

As a solo developer to develop practical database
administration and deployment skills.

## Considered Options

1. PostgreSQL
2. MySQL
3. SQLite

## Decision

Use PostgreSQL as the primary relational database
for Kanban V1.

## Rationale

- Supports relational integrity through foreign keys
  and other constraints.
- Supports ACID transactions for multi-step operations.
- Provides concurrency capabilities suitable for
  a multi-user web application.
- Supports complex queries and indexing.
- Provides experience operating a database server.
- Fits our full-stack learning objectives.

## Consequences

### Benefits

- Strong relational and transactional capabilities.
- Suitable foundation for future application growth.
- Practical experience with database administration.

### Trade-offs

- Requires operating a separate database service.
- Introduces connection and credential management.
- Requires database backup and recovery planning.
- More infrastructure setup than embedded SQLite.

## Revisit When

- Deployment or operational constraints change.
- The application's storage requirements change.
- Evidence shows the selected database is unsuitable.

## Related Requirements

- FR-01: User Authentication
- FR-02: Board Creation
- FR-04: Column Management
- FR-05: Task Management
- FR-06: Task Movement and Ordering
- FR-07: Data Persistence
- FR-08: Access Control
- NFR-01: Performance
- NFR-03: Reliability
