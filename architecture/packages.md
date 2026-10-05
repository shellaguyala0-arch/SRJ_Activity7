# Diagram 8 – Package Diagram: src/ folders and allowed dependencies

```mermaid
flowchart TB

SRC["src/"]

APP["app/<br/><br/>pages (student, driver, admin)<br/>and api/ route handlers"]

SERVICES["services/<br/><br/>business rules:<br/>booking, matching, tracking, auth"]

REPOSITORIES["repositories/<br/><br/>data access,<br/>one per table"]

ADAPTERS["adapters/<br/><br/>maps and notification wrappers"]

COMPONENTS["components/<br/><br/>reusable UI pieces"]

DB["db/<br/><br/>schema and database client"]

LIB["lib/<br/><br/>shared types, validation,<br/>constants"]

SRC --> APP
SRC --> COMPONENTS
SRC --> SERVICES
SRC --> REPOSITORIES
SRC --> ADAPTERS
SRC --> DB
SRC --> LIB

APP -.-> SERVICES
APP -.-> COMPONENTS
APP -.-> LIB

SERVICES -.-> REPOSITORIES
SERVICES -.-> ADAPTERS
SERVICES -.-> LIB

REPOSITORIES -.-> DB
REPOSITORIES -.-> LIB

ADAPTERS -.-> LIB

COMPONENTS -.-> LIB

style SRC fill:white,stroke:#555,stroke-width:2px
style APP fill:#eef6ff,stroke:#555
style SERVICES fill:#eef6ff,stroke:#555
style REPOSITORIES fill:#eef6ff,stroke:#555
style ADAPTERS fill:#eef6ff,stroke:#555
style COMPONENTS fill:#eef6ff,stroke:#555
style DB fill:#eef6ff,stroke:#555
style LIB fill:#eef6ff,stroke:#555
```

### Layering rule

- Pages/components never import repositories, adapters, or database directly.
- Only API route handlers call services.
- Only services call repositories/adapters.
- Only repositories touch `db`.
- Everyone may use `lib`.
