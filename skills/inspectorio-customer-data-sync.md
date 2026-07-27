---
name: Sync product, item, material and BOM data
description: Upsert products/items/materials, read them back, and manage bills of materials in the Quality Risk Management customer-data API.
api: openapi/inspectorio-qrm-openapi.json
operations: [upsertItems, listProductIntegration, getProductIntegrationDetail, createBom, listBoms, getBomDetails, getSynchronization]
---

# Sync product, item, material and BOM data

Keep Inspectorio's product graph in sync with your PLM/ERP via the QRM
customer-data endpoints (`https://sight.inspectorio.com`).

## Auth
Organization API key in the `apiKey` header.

## Steps
1. **Upsert products/items/materials** — `PUT /api/v1/customer-data/products`
   (`upsertItems`). Idempotent by `custom_id` — safe to resend.
2. **Check sync status** — `GET /api/v1/customer-data/synchronization/{entity_type}/{id}`
   (`getSynchronization`).
3. **List entities** — `GET /api/v1/customer-data/{entity_type}`
   (`listProductIntegration`); **get one** — `GET /api/v1/customer-data/{entity_type}/{custom_id}`
   (`getProductIntegrationDetail`).
4. **Create a BOM** — `POST /api/v1/customer-data/boms` (`createBom`); **list**
   for an entity — `GET /api/v1/customer-data/{entity_type}/{entity_custom_id}/boms`
   (`listBoms`); **detail** — `GET .../boms/{bom_custom_id}` (`getBomDetails`).
   BOM lines carry `countryOfOrigin` and `attribute` fields.

## Conventions
- Upsert is entity-level idempotent by `custom_id` (there is no HTTP
  Idempotency-Key header).
- Validation failures return field-keyed messages in the `errors` object
  (see `errors/inspectorio-problem-types.yml`).
