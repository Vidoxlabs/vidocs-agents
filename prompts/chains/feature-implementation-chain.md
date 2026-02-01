# Full-Stack Feature Implementation Chain

Use this chain when adding a new feature that requires changes to both the Database/API and the UI.

## Phase 1: Database & Schema (Backend Architect)

<reasoning>
1.  **Data Modeling**: What new data do we need to store?
    - Define changes to `schema.prisma`.
2.  **API Schema**: How will this data be exposed?
    - Define Pydantic models (Request/Response) in `apps/api`.
</reasoning>

## Phase 2: API Logic (Backend Architect)

<reasoning>
1.  **Endpoint Definition**: Define routes in `apps/api/app/api/endpoints/`.
2.  **Service Layer**: Implement business logic (CRUD, processing).
3.  **Verification**: How do we curl/test this endpoint?
</reasoning>

## Phase 3: UI Components (Frontend Architect)

<reasoning>
1.  **Component Design**: What UI elements are needed? (Forms, Lists, Charts).
    - Check `packages/ui` for existing primitives.
2.  **Data Fetching**: How do we get the data?
    - React Server Component (fetch) vs Client Component (useEffect/React Query).
</reasoning>

## Phase 4: Integration (Monorepo Manager)

<reasoning>
1.  **Wiring**: Connect the UI to the API endpoint.
2.  **Type Sync**: Ensure TS types match Python Pydantic models.
3.  **Route Protection**: Does this feature require Authentication?
</reasoning>

## Output Format

Generate a plan listing the files to create/edit in order:

1.  `packages/database/prisma/schema.prisma`
2.  `apps/api/app/models.py`
3.  `apps/api/app/api/endpoints/new_feature.py`
4.  `apps/web/src/types/new_feature.ts`
5.  `apps/web/src/components/new_feature/NewFeatureForm.tsx`
6.  `apps/web/src/app/new-feature/page.tsx`
