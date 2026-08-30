# Maintenance Integration Plan

## Current merged state

The Maintenance client and server source are included unchanged under `maintenance/`. This protects existing functionality while allowing the main ERP application to remain stable.

## Why the backend is not blindly merged into `server/src/index.js`

The ERP backend and Maintenance backend both have their own authentication, database schema and route assumptions. In particular, the Maintenance schema uses a generic `users` table, while the ERP database already contains its own users/employee/customer structures. Copying the routes directly into the ERP backend could overwrite or conflict with authentication and user data.

## Safe integration sequence

1. Deploy both modules against a new test environment.
2. Verify ERP, HR and Customer Portal exactly as before.
3. Verify Maintenance vehicles, expenses, users and reports.
4. Create namespaced Maintenance tables (for example `maintenance_users`, `maintenance_vehicles`, `maintenance_expenses`) or map Maintenance authentication to the ERP user model.
5. Add `/api/maintenance/*` routes to the ERP backend.
6. Configure the Maintenance client to use the unified API.
7. Add a Maintenance entry point/menu to the ERP web UI.
8. Test all four user portals before migrating real data.

## Database migration rule

Do not merge production data until the new test project has been fully verified. When ready, back up both existing databases first, then perform a controlled data migration with duplicate-user checking and row-count validation.
