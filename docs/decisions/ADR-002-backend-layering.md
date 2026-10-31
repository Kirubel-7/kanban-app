
# ADR-002: Backend Module and Layer Organization

**Status:** Accepted
**Date:** 2026-10-31

## Context

Kanban V1 uses a modular monolith (ADR-001).

The backend must support clear business boundaries,
maintainability, and independent testing of business
rules (NFR-05).

## Considered Options

1. Layer-first organization
2. Module-first organization with internal layers

## Decision

Adopt module-first organization with internal
separation of API, business logic, and data access.

Initial business modules:
- Authentication
- Boards (including column management)
- Tasks

## Rationale

- Related functionality stays together.
- Business responsibilities remain identifiable.
- Business rules can be tested independently.
- The structure supports future feature growth
  without requiring distributed services.

## Consequences

### Benefits
- Easier navigation by business feature.
- Better module cohesion.
- Clear separation of technical responsibilities.

### Trade-offs
- Requires discipline to prevent tight coupling.
- Some workflows cross module boundaries.
- Shared infrastructure must be managed carefully.

## Revisit When

Module boundaries become unclear or cross-module
dependencies become difficult to maintain.
