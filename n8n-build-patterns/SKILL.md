---
name: "n8n-build-patterns"
description: "Proactive n8n technical patterns, gotchas, native features, and a JavaScript opportunity map for non-coders. Surfaces automatically whenever building, debugging, scoping, or reviewing an n8n workflow. Fires before the build so you don't hand-roll what n8n ships natively or miss a one-line JS snippet that unlocks power."
---

# n8n Build Patterns

Use this skill PROACTIVELY whenever you are building, scoping, debugging, documenting, or reviewing an n8n workflow. The point is to surface the native n8n feature, the known gotcha, OR the one-line JavaScript snippet BEFORE writing custom code, dragging a whole new node, or burning time on trial-and-error.

Not every pattern applies to every build. Scan the list, flag the 1-3 that match the current workflow, skip the rest. Never dump the whole list at once.

Written for non-coders. Treat JavaScript as a lever, not a skill test. Flag one-line snippets with context ("paste this in the expression editor, done") rather than teaching syntax.

---

## Core pattern checklist

### 1. API pagination — use HTTP Request native Pagination, not Code node loops

If the build fetches data from an API that returns paginated results (nextPageToken, next URL, offset, cursor), do NOT write JavaScript to loop manually.

- n8n HTTP Request node → Options → Pagination → set Pagination Type
- Supply where the token sits in the response (e.g. nextPageToken) and which query param carries it (e.g. pageToken)
- Add a hard page cap (e.g. 20 pages max) to prevent runaway cost
- Catches APIs like YouTube Data API v3, Firecrawl, Apollo, OpenAI Batch

Flag this the moment a build involves "get all comments", "get all users", "get all pages", "loop through records".

### 2. Credentials from Stage 2, not Stage 3

Wire all API credentials in the n8n credential store during Stage 2 (Localize), not Stage 3. Saves backward edits every time.

### 3. Query Auth allowed domains — use wildcard or exact subdomain

For APIs served from a subdomain like www.googleapis.com, setting the allowed domain to the bare root googleapis.com fails. Use *.googleapis.com wildcard or exact subdomain.

### 4. Code node sandbox blocks require('crypto')

n8n's Code node sandbox blocks the Node crypto module. Any SHA / MD5 / HMAC call fails.

- For author ID or record anonymization, use pure JS djb2 hash (non-cryptographic, one-way, stable).
- For actual cryptography, do it outside n8n.

### 5. Code node Mode — "Run Once for Each Item" vs "Run Once for All Items"

Default is "Run Once for All Items". If the Code node is meant to process per-row, the default silently runs on item 0 only and discards the rest. Switch to "Run Once for Each Item".

### 6. Google Sheets tab binding — pick from live list, not typed string

Google Sheets Append / Update nodes bind the sheet by gid, not by tab name string. Always click into the dropdown and pick from the live "From list" picker.

### 7. OpenAI API keys now expire

OpenAI removed the "Never expire" option in 2025. Keys default to a 1-year expiry. Add a calendar reminder for the key's expiry date.

### 8. Retry On Fail + On Error pattern

For every external API node:
- Settings → Retry On Fail: ON, Max Tries 3, Wait 2000-5000 ms
- On Error per node type:
  - Core data-fetch nodes → Stop Workflow
  - Classification / enrichment / append nodes → Continue (using error output)

### 9. OAuth token refresh mid-run

Google (Sheets / Drive / Gmail / Calendar) OAuth tokens expire every few weeks of inactivity. Refresh before a critical run.

### 10. Free-tier daily quota tracking

Every external AI API has a free-tier daily cap that kills workflows mid-run without warning. Before stub test, verify balance + daily counter. Before scaling, project monthly cost at target volume.

### 11. Cost ceiling guardrails for AI nodes at scale

When pagination or batch patterns unlock 10x-50x more data, the AI cost multiplies too. Before shipping upgrades:
- Project monthly cost at new volume
- Add a hard page or row cap
- Set an alert at X% of budget

### 12. Test ONE Switch branch first

Before executing a full workflow with Switch router or multi-branch, run just one branch end-to-end first.

### 13. Pinned test data for development

Pin test data on the trigger or an early node so re-execution doesn't re-fetch from the API. Saves quota during iteration.

### 14. Workflow Publish is not the same as Node Activation

Schedule trigger node must be enabled AND the workflow itself must be Published / Active (top-right toggle). Both required.

### 15. Pre-flight check before Stage 4 stub test

Verify before the first live test:
- OpenAI balance > $2 and key not expired
- API keys for all data sources alive
- Google OAuth freshness < 30 days
- Sheet tabs exist with correct schema
- Credential store has all 5+ credentials

---

## JavaScript opportunity map (for non-coders)

The skill is pattern recognition, not JS fluency. Flag opportunities with the exact snippet to paste.

### Where JS lives in n8n (6 places)

1. Expression fields `{{ }}` — ANY node parameter field can hold a JS expression.
2. Code node — full JS or Python.
3. IF node condition — accepts expressions.
4. Switch node routing — route by expression value.
5. Set node value — assign a new or reshaped field.
6. HTTP Request body / query params — dynamic JSON via expressions.

### 10 opportunities where a snippet beats dragging a node

**1. Date and time math.**
```
{{ new Date(Date.now() - 7 * 24 * 60 * 60 * 1000).toISOString() }}
```

**2. String cleanup.**
```
{{ $json.comment.trim().toLowerCase().slice(0, 500) }}
```

**3. Default fallback for missing fields.**
```
{{ $json.author_name || 'Anonymous' }}
```

**4. Array filtering and counting.**
```
{{ $json.items.filter(i => i.classification === 'objection').length }}
```

**5. Conditional field assignment.**
```
{{ $json.likes > 50 ? 'high-engagement' : 'normal' }}
```

**6. Safe nested JSON path.**
```
{{ $json?.snippet?.topLevelComment?.snippet?.textOriginal || '' }}
```

**7. Dynamic API body.**
```
{ "query": "{{ $json.brand }}", "limit": 50, "country": "IN" }
```

**8. Hash or anonymize a field.** Pure JS djb2 in a Code node.
```javascript
function hash8(s) {
  let h = 5381;
  for (let i = 0; i < s.length; i++) h = ((h << 5) + h) + s.charCodeAt(i);
  return Math.abs(h).toString(16).padStart(8, '0').slice(0, 8);
}
return { json: { ...$input.item.json, author_hash: hash8($input.item.json.author_id || 'anon') } };
```

**9. Reshape API response into clean rows.**
```javascript
return $input.all().flatMap(item =>
  item.json.results.map(r => ({ json: { title: r.title, url: r.url, score: r.score } }))
);
```

**10. De-duplicate by a key.**
```javascript
const seen = new Set();
return $input.all().filter(item => {
  const key = `${item.json.video_id}_${item.json.author_hash}`;
  if (seen.has(key)) return false;
  seen.add(key);
  return true;
});
```

### When to use JS vs stay with native nodes

Use JS when:
- A native node needs 3+ clicks to do a 1-line transform
- You're chaining 3+ nodes to do what one expression could
- You need conditional logic inside a field
- You need to reshape an API response
- You need a value computed FROM another field

Stay with native nodes when:
- The logic is 10+ lines
- The node is 1 config step away
- The data flow is multi-branch (visual IF/Switch is readable)
- Teammates may touch the workflow and won't know JS

---

## Source

All 15 patterns and 10 JS opportunities come from real n8n builds shipped between Oct and Nov 2026: Competitor Intel Agent, FB Ad Spy, Label Lens, MR Field Companion, YouTube Comment Miner v1 and v1.1, Outreach Engine. Pattern 1 (HTTP Request native pagination) was flagged by an AI Automation Society Plus community member reviewing YouTube Comment Miner v1.1 on 13 Nov 2026.

## License

MIT. Use it, fork it, extend it.

## Author

Tron (Noel Gomes) — building AI automation tools for Consumer Health, OTC, and pharma in India.
- GitHub: [technoelogy](https://github.com/technoelogy)
- LinkedIn: [gomesnoel](https://www.linkedin.com/in/gomesnoel/)
