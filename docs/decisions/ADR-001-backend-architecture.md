
# ADR-001: Backend Architectural Style

**Status:** Accepted
**Date:** 2026-10-31

## Context

Kanban V1 requires authentication, board management,
column management, task management, and data persistence.

The application is developed by one developer.

The architecture should support maintainability,
independent testing of business rules, and manageable
deployment complexity.

## Considered Options

1. Modular monolith
2. Microservices

## Decision

Adopt a modular monolith for the Kanban V1 backend.

The backend will be deployed as one application,
with logically separated modules for major
business responsibilities.

## Rationale

- V1 does not require independent service deployment.
- A single backend reduces operational complexity.
- Internal modules support separation of concerns.
- Related business operations can be coordinated
  without introducing distributed service calls.
- The architecture supports our learning objectives.

## Consequences

### Positive
- Simpler development, debugging, and deployment.
- Easier end-to-end request tracing.
- Clear internal separation of responsibilities.

### Trade-offs
- Backend modules share a deployment lifecycle.
- Independent scaling of individual modules
  is not directly available.
- Poor module boundaries could create tight coupling.

## Revisit When

- Independent deployment becomes necessary.
- Different modules develop substantially different
  scaling or availability requirements.
- Team or organizational boundaries justify
  independent services.
