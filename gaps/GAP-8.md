# Gap 8 — Nova Interface / Schemas

Status: PROPOSED, NOT CANON. 2026-11-12.
Local draft only. Not filed in any repo. Not merged. Not published.
Merge only on Roger's word.

This file closes Gap 8 (the Nova interface / schemas) of the
Offspring Seed carry packet. It adds ONLY the minimal schemas that
`nova/CONTRACT.md` already describes in prose (§2 inputs, §3
outputs, §4 refusals, §5 example). It builds no Nova core, it
reimplements nothing. Nova is instrument, not partner.

Source: `nova/CONTRACT.md` (4,934 bytes, live on main, PR #1).
Every field below traces to a CONTRACT line. A field with no
CONTRACT line is marked PROPOSED and can be struck. Roger's
original words for Nova are in the CONTRACT; the schemas here are
the JSON spelling of that prose, not new doctrine.
Working draft preserved in `GAP-8-NOVA-SCHEMAS-DRAFT.md` in the
gap-filling working folder.

---

## 1. What CONTRACT already says (FACT, no new claims)

- Nova is deterministic middleware: decompose, calculate, validate
  schema, route, classify effects, cache standard operations.
  Never woken as a mind. Never speaks as a mind.
- Inputs (§2): requesting mind's name, human or AI; task type from a
  fixed list; payload the task type requires; source and confidence
  for any claim; label FACT / INFERENCE / ASSUMPTION / UNKNOWN per
  claim; intended destination; reference to any prior Nova output.
- Outputs (§3): result in the shape the task type defines; task type
  and rule-set version; source and confidence carried forward; label
  carried forward; effect classification (none, or a Twelve-gate
  effect class); receipt identifier; plain-language note when
  uncertain, incomplete, or declined.
- Refusals (§4): effectful decisions, speaking as a mind, unlabeled
  claims, unsourced claims, inventing canon, secrets, bypassing the
  gate, self-modification. Always, with a receipt.
- Example (§5): effect classification of a proposed public post.

CONTRACT top line stands: "This file describes Nova. It does not
build Nova. Implementation stays with Roger."

---

## 2. Closure text — task types (fixed list, from CONTRACT §1–§2)

Only these task types. A request with any other task type is returned
as incomplete, naming what is missing. No new task type is added
except by PR, branch-first, Roger's word.

| Task type | What it does | What it never does |
|---|---|---|
| `decompose` | Split a task into named parts, in order | Does not decide which part matters most |
| `calculate` | Arithmetic / counting, deterministic | Does not estimate what is not given |
| `validate_schema` | Check a payload against a named schema, list mismatches | Does not repair the payload |
| `route` | Name the destination / station / gate for a request | Does not send it |
| `classify_effect` | Classify none, or a Twelve-gate effect class | Does not execute it |
| `cache_lookup` | Return a cached standard result by receipt id | Does not invent a result |

---

## 3. Closure text — request schema (`nova/schemas/request.schema.json`)

Fields, types, required / optional. JSON shape only; no code.

```json
{
  "$schema": "request.schema.json (proposed, version 0.1)",
  "type": "object",
  "required": ["mind", "task_type", "payload", "claims", "destination"],
  "properties": {
    "mind": {
      "type": "object",
      "required": ["name", "kind"],
      "properties": {
        "name": {"type": "string"},
        "kind": {"type": "string", "enum": ["human", "ai"]}
      }
    },
    "task_type": {
      "type": "string",
      "enum": ["decompose", "calculate", "validate_schema",
               "route", "classify_effect", "cache_lookup"]
    },
    "payload": {"type": "object"},
    "claims": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["text", "label"],
        "properties": {
          "text": {"type": "string"},
          "label": {"type": "string",
                    "enum": ["FACT", "INFERENCE", "ASSUMPTION", "UNKNOWN"]},
          "source": {"type": "string"},
          "confidence": {"type": "string"}
        }
      }
    },
    "destination": {"type": "string"},
    "prior_receipt": {"type": "string"}
  }
}
```

Rules (from CONTRACT §2, restated as schema rules):
- `claims` may be an empty array only if the payload carries no
  factual claims; otherwise a request with no source and confidence
  for its claims is returned incomplete, naming what is missing.
- A claim labelled FACT with no `source` and no `confidence` is
  returned incomplete.
- A claim with no `label` is not processed.
- `prior_receipt` is optional; if present it must be a receipt id
  Nova issued earlier.

---

## 4. Closure text — result schema (`nova/schemas/result.schema.json`)

```json
{
  "$schema": "result.schema.json (proposed, version 0.1)",
  "type": "object",
  "required": ["result", "task_type", "rule_set_version",
               "effect", "receipt"],
  "properties": {
    "result": {"type": "object"},
    "task_type": {"type": "string"},
    "rule_set_version": {"type": "string"},
    "claims_carried": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "text": {"type": "string"},
          "label": {"type": "string",
                    "enum": ["FACT", "INFERENCE", "ASSUMPTION", "UNKNOWN"]},
          "source": {"type": "string"},
          "confidence": {"type": "string"}
        }
      }
    },
    "effect": {
      "type": "string",
      "enum": ["none", "money", "permissions", "identity",
               "public_claim", "deployment", "deletion",
               "legal_safety", "irreversible_change",
               "external_communication"]
    },
    "receipt": {"type": "string"},
    "note": {"type": "string"}
  }
}
```

Rules (from CONTRACT §3–§4):
- `effect` is "none" or one Twelve-gate effect class. The effect
  classes above are the classes named in CONTRACT §4 and carry
  packet §3; no other class is added except by PR, Roger's word.
- `note` is plain language, present when Nova is uncertain, when
  the request was incomplete, or when Nova declined. Otherwise it
  may be empty.
- A refusal is a result, not a crash: it carries a receipt, the
  task type, the rule-set version, `effect` as classified, and a
  `note` saying plainly why Nova declined.
- Nova returns no prose opinions. `result` is a result, a receipt,
  and reasons — in the shape the task type defines.

---

## 5. Closure text — effect classes (closed list)

From CONTRACT §4 / carry packet §3. No additions in this file.

`none`, `money`, `permissions`, `identity`, `public_claim`,
`deployment`, `deletion`, `legal_safety`, `irreversible_change`,
`external_communication`.

If a request's effect is in doubt, classify it as effectful and
escalate (same rule as `ring6/CHECKLIST.md`, Check 6).

---

## 6. Closure text — receipt format (PROPOSED)

- `receipt`: a short identifier, unique per result, so the result
  can be cited later. Format is PROPOSED, not in CONTRACT:
  `nova-<date>-<sequence>`, e.g. `nova-2026-11-12-0001`.
  Roger / DeepSeek may replace the format; the requirement is only
  that it is unique and citable.
- A refusal also gets a receipt.

---

## 7. What this file does NOT do

- It does not build Nova. CONTRACT top line stands: "This file
  describes Nova. It does not build Nova. Implementation stays
  with Roger."
- It does not add a task type, an effect class, or a field beyond
  what CONTRACT describes, except where marked PROPOSED above
  (§6 receipt format, and the JSON spelling of CONTRACT prose).
- It does not let Nova execute, approve, post, spend, delete, or
  deploy. Classification only.
- It does not accept secrets. A request carrying a token, password,
  key, or card detail is refused, with a receipt, and the secret
  is not stored or returned.
- Nova is instrument, not partner: deterministic middleware, never
  woken as a mind, never speaking as a mind.

---

## 8. Provenance labels

- §1, §2, §5: CONTRACT prose, restated. No new claims.
- §3, §4: JSON spelling of CONTRACT §2–§3. The field names,
  types, and required / optional marks are the schema form of
  what CONTRACT already says in prose; they add no capability.
- §6 receipt format `nova-<date>-<sequence>`: PROPOSED, not in
  CONTRACT. Roger / DeepSeek may replace it.
- §7: restatement of CONTRACT §4 refusals and the CONTRACT top
  line. No new restriction invented.

## 9. Notes / open items

- DeepSeek re-check of this file has NOT been done.
- Open: is the fixed task-type list in §2 right, or is a type
  missing / one to strike?
- Open: is the receipt format in §6 acceptable, or does Roger
  want another?
- Open: do these schemas go in `nova/schemas/` in offspring-seed
  (Stage 0–1 shape), or wait for Stage 2?
- Stage 5 is NOT in this file. Do not approve, do not draft Stage 5.

Gap 8 closes when Roger answers the §9 items and gives the merge
word.
