# Apollo Unified Platform (HRApollo)

This repository is the **new test/merge project** for Apollo Freight Solutions.

It combines the existing working source code without changing the original repositories:

- **ERP** – shipment, manifest, billing, dashboard and operations
- **HR Portal** – employee and leave management
- **Customer Portal** – customer-facing shipment functions
- **Maintenance** – vehicles, expenses and maintenance records

## Source preservation

The ERP application remains the primary web application at the repository root. The Maintenance application is preserved under `maintenance/` so its complete React client and Node.js API remain available while the unified integration is tested.

Original repositories are not deployment targets for this test project and should remain unchanged.

## Structure

```text
HRApollo/
├── web/                 ERP + HR + Customer Portal frontend
├── server/              ERP API and PostgreSQL migrations
├── maintenance/
│   ├── client/          Maintenance React web application
│   └── server/          Maintenance Node.js API
├── DEPLOYMENT.md
└── MAINTENANCE-INTEGRATION.md
```

## Safe test deployment

Use a **new database** and new test deployments. Do not point this project at production databases until the application is verified.

### ERP / main application

1. Create a new PostgreSQL database.
2. Deploy `server/` as the main API service.
3. Deploy `web/` as the main web frontend.
4. Configure the frontend API URL according to the existing `web/config.js` configuration.
5. Run the existing ERP migrations against the new database.

### Maintenance module

1. Deploy `maintenance/server/` as a separate test API service during the initial migration phase.
2. Deploy `maintenance/client/` as a web application and set `VITE_API_URL` to the new Maintenance API URL.
3. Point it to the **same new PostgreSQL server/database only after table-name validation** described in `MAINTENANCE-INTEGRATION.md`.

## Important

This repository intentionally keeps both applications' original source trees intact first. That makes it possible to test every existing function before a deeper single-backend refactor. The next engineering step is to namespace/merge the Maintenance API tables and routes into the ERP backend after test validation.
