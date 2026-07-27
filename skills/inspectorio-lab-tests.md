---
name: Manage Inspectorio lab tests
description: Create lab tests, list and retrieve them, run bulk actions, and pull CPSC eFiling data via the Quality Risk Management API.
api: openapi/inspectorio-qrm-openapi.json
operations: [CreateLabTest, ListLabTest, GetLabTestPackageDetail, BulkActionLabTest, CPSCEfiling]
---

# Manage Inspectorio lab tests

Use the Quality Risk Management API (`https://sight.inspectorio.com`) to
initiate and track lab tests on behalf of brands, retailers, and laboratories.

## Auth
Send your organization API key in the `apiKey` header on every request. Keys are
created under `Configuration -> API Keys` and do not expire unless revoked.

## Steps
1. **Create a lab test** — `POST /api/v1/lab-tests` (`CreateLabTest`). Submit a
   New, Draft, or Submitted lab test.
2. **List lab tests** — `GET /api/v1/lab-tests` (`ListLabTest`). Page with
   `limit`/`offset`; filter by `created_from`/`created_to`,
   `updated_from`/`updated_to`, and `status`. Tests can be searched by short
   10-letter Test ID.
3. **Get a test package** — `GET /api/v1/lab-tests/test-packages/{package_id}`
   (`GetLabTestPackageDetail`).
4. **Bulk actions** — `POST /api/v1/lab-tests/bulk-actions/{action}`
   (`BulkActionLabTest`).
5. **CPSC eFiling** — `POST /api/v1/lab-tests/efiling` (`CPSCEfiling`) returns
   compliance-ready certificate data for completed tests.

## Conventions
- Pagination: `limit`/`offset` (see `conventions/inspectorio-conventions.yml`).
- Errors: custom `{ errorCode, message, errors? }` JSON envelope; retry 5xx after
  1 min then 3 min (see `errors/inspectorio-problem-types.yml`).
- Rate limiting surfaces as HTTP 429.
