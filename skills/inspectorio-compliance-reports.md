---
name: Retrieve compliance assessments and reports
description: Search and retrieve Responsible Sourcing & Compliance assessments and report data via the RSC API.
api: openapi/inspectorio-rsc-openapi.json
operations: [searchAssessmentsV1, getAssessmentV1, listReportsV2, getReportV2, getStepExecution]
---

# Retrieve compliance assessments and reports

Pull Responsible Sourcing & Compliance data from the RSC API
(`https://rise-integration.inspectorio.com`).

## Auth
Organization API key in the `apiKey` header (created under
`My Organization -> API Key`).

## Steps
1. **Search assessments** — `POST /api/v1/assessments/search`
   (`searchAssessmentsV1`). Filter by `assessment_type`, date ranges,
   `capa_status`, and status; page with `limit`/`offset`.
2. **Get an assessment** — `GET /api/v1/assessments/{assessment_id}`
   (`getAssessmentV1`).
3. **List reports (V2)** — `GET /api/v2/reports` (`listReportsV2`); **get a
   report** — `GET /api/v2/reports/{report_id}` (`getReportV2`). Use
   `capa_details` and `include_step_questions` to expand.
4. **Get a step execution** — `GET /api/v1/reports/{report_id}/steps/{step_id}`
   (`getStepExecution`).

## Conventions
- Pagination `limit`/`offset`; error envelope `{ errorCode, message, errors? }`.
- See `conventions/inspectorio-conventions.yml` and
  `errors/inspectorio-problem-types.yml`.
