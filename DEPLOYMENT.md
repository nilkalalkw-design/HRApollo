# Test Deployment Checklist

## Create new services

- New Vercel project for the ERP frontend (`web/`)
- New Render service for the ERP API (`server/`)
- New Vercel project for Maintenance (`maintenance/client/`) during test phase
- New Render service for Maintenance (`maintenance/server/`) during test phase
- New PostgreSQL database for testing

## Never use production values during testing

Do not reuse production `DATABASE_URL` or other production secrets.

## Suggested environment variables

### ERP API
- `DATABASE_URL`
- `ALLOWED_ORIGIN`
- `CUSTOMER_PORTAL_SECRET` (or allow the existing system-secret bootstrap on a new database)
- any existing Cloudinary/email variables required by the application

### Maintenance API
- `DATABASE_URL`
- `APP_ORIGIN`
- authentication/email variables from `maintenance/server/.env.example`

### Maintenance frontend
- `VITE_API_URL`

## Verification before real-data migration

- [ ] ERP login and permissions
- [ ] Shipment creation/editing
- [ ] Manifest workflow
- [ ] Dashboard and reports
- [ ] HR employee functions and leave workflow
- [ ] Customer Portal
- [ ] Maintenance login
- [ ] Vehicles
- [ ] Expenses
- [ ] Maintenance reports
- [ ] Cross-browser testing
- [ ] Database backup and migration rehearsal
