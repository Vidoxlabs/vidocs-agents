# Context Overlay: VidoxLabs Studio

This overlay provides specific architectural context for the `vidoxlabs-studio` repository. Apply this context when working on the Studio codebase.

## 📂 Repository Structure

- **`apps/web`**: Next.js 14+ (App Router). The public face and dashboard.
  - **Port**: 3000
  - **Auth**: NextAuth.js
  - **Styling**: Tailwind + Shadcn UI
- **`apps/api`**: Python FastAPI. The intelligence layer.
  - **Port**: 8000
  - **Docs**: `/docs` (Swagger UI)
  - **Database**: Prisma / PostgreSQL
- **`packages/ui`**: Shared React components (Shadcn based).
- **`packages/database`**: Shared Prisma schema and client.

## 🔌 Integration Patterns

1.  **Frontend -> Backend**:
    - The frontend communicates with the Python API via REST.
    - Base URL: `http://localhost:8000` (Local) or env var `NEXT_PUBLIC_API_URL`.
    - Authentication tokens are passed via Authorization header.

2.  **Shared Types**:
    - Since we have TS (Frontend) and Python (Backend), types are **NOT** automatically shared.
    - **Rule**: When changing a Pydantic model in `apps/api`, you MUST update the corresponding TypeScript interface in `apps/web/types`.

## 🚀 Development Workflow

```bash
# Start everything
pnpm dev

# This runs:
# - apps/web: pnpm dev (Port 3000)
# - apps/api: poetry run uvicorn (Port 8000)
```

## 🚨 Project Specific Rules

- No Direct DB Access in Web: apps/web should rarely access the DB directly. Prefer fetching data through apps/api for logic-heavy operations.
- Strict Linting: We use eslint and ruff (Python). Ensure no errors before pushing.
