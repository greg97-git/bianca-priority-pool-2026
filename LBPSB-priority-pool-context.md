# LBPSB Priority Pool — Project Context (Bianca)
> Reference document for Claude sessions working on Bianca's priority pool planning tool.
> Last updated: June 2026

---

## What This Is

The Lester B. Pearson School Board (LBPSB) runs an annual **Priority Pool Selection** process where teachers without a permanent contract pick available posts in strict seniority order. This document explains the rules, Bianca's specific situation, and the tools built to help her prepare.

---

## The Selection Process

### Seniority Format
Teachers are ranked by a priority number in `YY-DDD` format:
- `YY` = last two digits of hire year
- `DDD` = day of the year they were hired
- **Lower number = more senior = picks earlier**
- Example: `01-195` = hired in 2001, day 195 of that year

### How Selection Day Works
1. Teachers are called in seniority order
2. When it's your turn, you can pick any available eligible post (see eligibility below)
3. Once picked, the post is removed from the pool
4. You can also pick a **combination** of posts (see combination rules below)
5. If you pass on an eligible post ≥50%, you must formally invoke **Right of Refusal**

---

## Bianca's Profile

| Field | Value |
|---|---|
| Name | Bianca Chabot |
| Priority number | 01-195 |
| French-qualified | NON (not French-qualified) |
| Main (visible) category | **3403** — English Generalist Cycle 1-3 |
| Secondary category | **3404** — French |
| Days of experience | ~195 days |
| Teachers ahead of her | TBD — check PriorityList2026.pdf |

> **Note:** Bianca picks earlier than Sofia (01-195 vs 02-118 — lower number is more senior). She has a meaningfully better shot at the higher-value posts.

---

## Category Codes

| Code | Subject |
|---|---|
| 3403 | English Generalist Cycle 1-3 |
| 3404 | French (Français langue 2e primaire) |
| 3400 | Elementary Resource (remedial) |
| 3402 | Kindergarten |
| 3405 | Physical Education |
| 3406 | Art |
| 3438 | Other subjects (confirm with current year's job list) |

### Visible vs. Secondary Categories
- Bianca's **main** category is 3403. This is where she has first right of refusal.
- Her **secondary** category is 3404 French. She is eligible to pick 3404 posts, but 3404-primary teachers are prioritized first.
- When parsing a job list, include posts where the category matches **3403 or 3404**.

---

## Contract Types

| Code | Name | Description |
|---|---|---|
| E1 | Real year-round | Permanent-equivalent. Runs July 1 – June 30. Leads to tenure. Treat same as E2 for priority. |
| E2 | Real year-round | Best standard contract. Runs July 1 – June 30. Leads to tenure. Prioritize these. |
| E3 | Partial real | Partial-time with a guaranteed end date. Better than E8. |
| E4 | Partial real <34% | Same as E3 but very small percentage. |
| E8 | Replacement | No guaranteed end date — can end early if the permanent teacher returns. Riskiest. |

> Bianca's job list includes both **E1 and E2** real year-round posts. The app stats bar tracks them together as "E1/E2 Real available."

---

## Right of Refusal

If a post **≥50% in Bianca's main category (3403)** is available at her turn, she cannot silently skip it. She must either:
1. **Claim it**, or
2. **Formally invoke Right of Refusal** — declaring she refuses it on the record. The post stays in the pool for the next teacher.

Failing to formally refuse when a qualifying post is available has administrative consequences. This is why ≥50% posts are flagged with `ror: true` in the tool.

---

## Combination Rules

A teacher can combine **two or more posts** into a single contract. Key rules:

1. **The largest single post must be in the teacher's main category (3403)**. The other posts can be in any category (including 3404 French).
2. **Experience thresholds:**
   - E8 combinations: need **100 days** of experience (Bianca has ~195 days ✓)
   - E3 combinations that create a 100% vacancy: need **200 days** of experience (Bianca has ~195 days — just below this threshold, verify before committing)
3. **Natural combo pattern for Bianca:** 3403 English majority + 3404 French minority. Many bilingual posts at LBPSB are split 50/50 (English half = 3403, French half = 3404) — these pair naturally.
4. Posts flagged `cv` in the tool have confirmed valid combo partners listed. Posts flagged `ci` have potential combos that need percentage verification before committing.

### Confirmed Combo Opportunities for Bianca

| Anchor Post | Anchor % | Partners | Combined Total | Type |
|---|---|---|---|---|
| 8615 Birchwood (3403) | 50% | 6301 (3404 50%) | **100%** | E3 |
| 10765 Verdun (3403) | 55% | 6088 (3400 10%) + 10766 (3405 10%) + 10767 (3406 9%) | **84%** | E3 |
| 1404 Allion (3403) | 50% | 1404-FR (3404 50%) | **100%** | E8 |
| 3473 Clearpoint (3403) | 50% | 3473-FR (3404 50%) | **100%** | E8 |
| 5652 St. John Fisher Jr (3404) | 80% | 5652-20 (3404 20%) | **100%** | E8 |
| 1453 St. Anthony (3404) | 50% | 1533 (3404 20%) | **70%** | E8 |

> **E3 combo note:** Bianca has ~195 days experience, just below the 200-day threshold for E3 combos that create a 100% vacancy. Verify exact day count before committing to the Birchwood or Verdun combos.

---

## Parsing the Job List PDF

When a new JOBLIST PDF is provided, here is how to identify eligible posts for Bianca:

1. **Filter by category code:** Include any post with code **3403 or 3404** (her main and secondary categories).
2. **Extract per post:**
   - Post code (numeric ID)
   - Category code
   - Percentage (%)
   - Contract type (E1/E2/E3/E4/E8)
   - Grade/Cycle description
   - School name
   - Location/borough
   - Start time (Early Start / Late Start — refers to school calendar zone)
   - Start and end dates
   - Post description (includes language program info: Bilingual, French Plus, French Immersion, etc.)
3. **Flag ROR:** Mark `ror: true` for any post ≥50% in category 3403 (her main category).
4. **Identify combos:** The most common pattern is bilingual posts where the 3403 English half and 3404 French half share the same base code (e.g., `1404` and `1404-FR`). Also look for same-school posts where 3403 is the largest.
5. **Flag potential combos for verification:** If a combo looks possible but percentages need confirming, add a `ci` (combo investigate) note rather than asserting it as valid.

### Field Extraction Rules

**`grade` field:**
- If the PDF shows "Other - Specify Under Description" → store `"See description"`
- If the grade/cycle section is blank or missing → store `"Unknown"`
- Otherwise → store verbatim as it appears in the PDF

**`desc` field** — build as: `[Contract prefix]. [Program]. [Full verbatim PDF description paragraph].`
- Contract prefix: `"Real year-round"` for E1/E2, `"Partial real"` for E3/E4, `"Replacement"` for E8
- Program: the language program keyword from the post (e.g. Bilingual, French Plus, French Immersion, Regular French, etc.)
- Full paragraph: paste the complete description text verbatim from the PDF — do not summarize or paraphrase. Preserve typos exactly as they appear.
- If the post has no description paragraph, use just the contract prefix and program.

**All other fields** (`code`, `cat`, `pct`, `ctype`, `school`, `location`, `start_time`, `s`, `e`, `cv`, `ci`, `ror`) — extract verbatim. Do not infer or guess missing values.

### School Name Aliases
The job list and school info sheets sometimes use slightly different names. Common ones encountered:
- "St. Charles" ↔ "St-Charles"
- "Allion Elementary" ↔ "Allion"
- "Verdun Elementary" ↔ "Verdun"
- "Children's World Academy" ↔ "Children's World"

---

## The Tool

### Files
| File | Description |
|---|---|
| `index.html` | The full single-file web app (HTML + CSS + JS) |
| `JOBLIST2026V1.pdf` | Source job vacancy list used to populate the app |
| `PriorityList2026.pdf` | Full ranked list of priority pool teachers |
| `TEMPLATE-Priority Pool line up 2026.xlsx` | Original LBPSB Excel template |
| `TEMPLATE-GUIDE.md` | Step-by-step guide for adapting the app to a new teacher |

### GitHub Repo
`github.com/greg97-git/bianca-priority-pool-2026` *(confirm repo name)*
Live at: `https://greg97-git.github.io/bianca-priority-pool-2026/` *(confirm once deployed)*

### App Architecture (index.html)
- **No framework, no build step.** Plain HTML + CSS + Vanilla JS, single file.
- All job data is in a `JOBS` array (hardcoded in the `<script>` block).
- All combo data is in a `COMBOS` array.
- State is managed with two JS objects: `displayOrder` (array of codes in preference order) and `taken` (object of taken codes).
- Bianca's app includes an **E1 contract type** (in addition to E2–E8) because her job list contains E1 real year-round posts. The stats bar counts E1 and E2 together.

### localStorage Keys
| Key | What it stores |
|---|---|
| `bianca2026_order` | JSON array of job codes in her preference order |
| `bianca2026_taken` | JSON object of taken/claimed post codes |
| `bianca2026_colorder` | Column arrangement |

On load, the app merges saved state with the current JOBS array: saved order is preserved, any new jobs not in the saved order are appended at the bottom sorted by default (E1/E2→E3→E4→E8, pct desc).

### Key Fields in the JOBS Array
```js
{
  code: "10843",       // Post code from job list
  cat: "3403",         // Category code
  pct: 100,            // Percentage (integer)
  ctype: "E2",         // Contract type
  grade: "Cycle 1-3",  // Grade/cycle description
  school: "Birchwood", // School name
  location: "St-Lazare", // Borough/city
  start_time: "Late Start", // or "Early Start" or ""
  desc: "Real year-round. French Plus.", // Free-text description
  s: "2026-07-01",     // Start date
  e: "2027-06-30",     // End date ("Open" for E8)
  cv: "",              // Confirmed valid combo string (empty if none)
  ci: "",              // Combo to investigate (needs % verification)
  ror: true            // Right of Refusal applies (pct >= 50, cat 3403)
}
```

### Update Workflow (When New Job List Arrives)
1. User shares the new JOBLIST PDF (and this context file) with Claude in a new session
2. Claude reads the PDF in chunks — max 20 pages per Read call, so 3 reads for a 44-page file. Read all pages before writing any code.
3. Claude extracts all 3403 + 3404 posts using the **Field Extraction Rules** above, flags ROR, identifies combos
4. Claude performs a **surgical diff** against the current `JOBS` array using `code` as the unique key:
   - **New codes** (in PDF but not in current JOBS) → append at the bottom
   - **Removed codes** (in current JOBS but absent from new PDF) → delete the entry
   - **Changed fields** (same code, different values) → update only those fields; never reassign `code`
5. User pushes updated `index.html` to GitHub
6. GitHub Pages redeploys in ~60 seconds
7. Bianca's localStorage preference order is preserved; new jobs appear at the bottom of her list

---

## Source Documents
- **PriorityList2026.pdf** — Full ranked list of priority pool teachers. Used to count competitors ahead of Bianca and gauge her odds.
- **JOBLIST2026V1.pdf** — Job vacancy list. All 3403 + 3404 eligible posts were extracted from this.
- **TEMPLATE-Priority Pool line up 2026.xlsx** — Original Excel template from LBPSB. Contains school info (principals, locations) useful for cross-referencing.
- **TEMPLATE-GUIDE.md** — Developer guide for adapting the app to a new teacher.

---

## Differences vs. Sofia's Tool

| Feature | Bianca | Sofia |
|---|---|---|
| Priority number | 01-195 (picks earlier) | 02-118 |
| Main category | 3403 English Generalist | 3403 English Generalist |
| Secondary category | 3404 French | 3402 Kindergarten |
| Total posts | 97 | 46 |
| Contract types | E1, E2, E3, E4, E8 | E2, E3, E4, E8 |
| localStorage prefix | `bianca2026_` | `sofia2026_` |
| Row colours | Green (3403) + Pink (3404) | Green (3403) + Blue (3402) |
