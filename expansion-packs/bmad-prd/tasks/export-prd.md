# Export Fetched PRD Task (Non-Interactive)

## Purpose

Export previously fetched PRD content from the **current conversation history only** into one or more markdown files using the `fetched-prd-tmpl.yaml` template, ready for SM/Dev/QA agents.

## Constraints

- **ONLY** use fetched content present in this conversation history.
- **DO NOT** access external sources or other chats.
- **MUST** render via template: `{root}/templates/fetched-prd-tmpl.yaml`.
- **Output path:** `docs/fetched-prds/{{optional_id}}_{{task_or_feature_name}}.md`.
- **No prompts/confirmations.** Execute and export deterministically.

## Preconditions (Hard Gate)

1. Scan conversation history for outputs from `*fetch-prd` or `*auto-fetch-prd` (including any structured PRD payloads and metadata).
2. **If none found → HALT** and output:

```markdown
❌ No fetched PRD content detected in this conversation.
Use `*fetch-prd {source} {detail/key}` or `*auto-fetch-prd` first, then rerun `*export-prd`.
```

## Execution Steps

1. **Collect Fetched Items**
   - Gather all PRD payloads with minimal metadata:
     - `source_system` (e.g., Jira, Confluence, GitHub)
     - `source_url`/`original_id`
     - `fetched_at`, `last_updated`, `confidence/completeness`
     - `feature_name` or title/epic/story grouping hints
     - requirement bodies (functional, non-functional, acceptance, etc.)

2. **Normalize & Group by Feature**
   - Determine `task_or_feature_name` per item:
     - Prefer explicit `feature_name`.
     - Else use main title/epic; fallback to best available label.

   - Create a **slug** (lowercase, hyphenated, alnum only).
   - Group items sharing the same feature slug.

3. **Determine `optional_id`**
   - For each feature group, set `optional_id`:
     - Prefer an available stable ID (e.g., common epic key).
     - Else `YYYYMMDDHHmm` (UTC) timestamp.

4. **Multi-Source Merge (Same Feature)**
   - If a feature group has items from **multiple sources or tasks**, **export a single file** for that feature.
   - Within that file, create separate **sections per source/task** preserving traceability.

5. **Populate Template Variables (per feature group)**
   - Load `{root}/templates/fetched-prd-tmpl.yaml`.
   - Provide variables (aggregate where appropriate):

     ```yaml
     task_or_feature_name: "<slug>"
     optional_id: "<derived_optional_id>"
     sources:
       - system: "<source_system>"
         original_id: "<id>"
         source_url: "<url>"
         fetch_timestamp: "<fetched_at>"
         last_updated: "<last_updated>"
         confidence_level: "<High|Medium|Low>"
         item_count: <n>
     quality:
       completeness_percent: <0-100>
       notes: "<short assessment>"
     ```

   - Map requirements into numbered lists:
     - Functional → FR#
     - UI/UX → UI#
     - Data → DR#
     - Integrations → IR#
     - Performance/Security/Reliability → PR#/SR#/RR#
     - Business Rules → BR#
     - Acceptance Criteria → AC#

   - Preserve original wording where possible; normalize to clear, testable statements.

6. **Render & Write Files**
   - Render the template once **per feature group** to `docs/fetched-prds/{{optional_id}}_{{task_or_feature_name}}.md`

   - Ensure `docs/fetched-prds/` exists (create if missing).

7. **Validation (per file)**
   - File exists and is non-empty.
   - Metadata block present with all sources listed.
   - All requirement categories populated when available.
   - Acceptance criteria present if any were fetched.
   - Source references (URL/ID) included for traceability.

8. **Completion Summary (Non-Interactive Output)**
   - Print a compact summary for **each** exported file:

     ```markdown
     ✅ Exported: docs/fetched-prds/{optional*id}*{task_or_feature_name}.md
     Sources: {systems...} • FR:{n} UI:{n} DR:{n} IR:{n} NFR:{n} AC:{n} BR:{n}
     Quality: {completeness_percent}% • Generated: {timestamp}
     ```

   - If multiple distinct features detected, **export all** in separate files and list each line as above.

## Notes & Rules

- If multiple **features** are present → **multiple files** (one per feature).
- If one feature spans **multiple sources/tasks** → **one file**, with per-source sections.
- No user prompts; the task must infer names/IDs from fetched data and proceed.
- All content must originate strictly from the current conversation’s fetched PRD data.

---
