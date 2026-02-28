# File Management System Extraction

Extracted: 2026-02-27
Phase: 1 (Technical Systems)
Status: DRAFT -- awaiting Maya review

---

## Table of Contents

1. [System Overview](#1-system-overview)
2. [Tag Vocabulary](#2-tag-vocabulary)
3. [n8n Workflow Documentation](#3-n8n-workflow-documentation)
4. [Routing Matrix Rules](#4-routing-matrix-rules)
5. [Google Drive Folder Structure](#5-google-drive-folder-structure)
6. [Client-to-Folder Mapping](#6-client-to-folder-mapping)
7. [Amazon Delivery Tracking Workflows](#7-amazon-delivery-tracking-workflows)
8. [Design Principles](#8-design-principles)
9. [Known Gaps and Uncertainties](#9-known-gaps-and-uncertainties)

---

## 1. System Overview

- **Claim:** Maya's file management system is a TagSpaces-to-Google-Drive-to-n8n pipeline for automatic file organization. Files are tagged locally via filename brackets, dropped into client intake folders in Google Drive, and n8n workflows route them to destination folders based on a tag-pair lookup matrix.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2, "The File System"); all three Sort workflow JSON files
- **Confidence:** CONFIRMED
- **Impact:** File management automation domain; foundational to all content production workflows
- **Last verified:** 2026-02-27

- **Claim:** The system philosophy is "describe what a thing IS, let the system figure out where it GOES." Maya offloads the cognitive cost of remembering folder structures onto a lookup table.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2)
- **Confidence:** CONFIRMED
- **Impact:** Design philosophy for all file-related automation
- **Last verified:** 2026-02-27

### Pipeline Steps

1. Maya uses **TagSpaces** to tag files in her local Downloads folder by appending bracketed tags to filenames (e.g., `[Cover Painting-Celia]`).
2. She drags tagged files into a **client-specific intake folder** in Google Drive (e.g., `/MAYA`, `/LYNN`, `/SULIMA`).
3. **n8n watches those intake folders** on an hourly schedule trigger.
4. n8n extracts bracketed tags from the filename, removes the client tag, sorts remaining tags alphabetically to create a canonical key ("symmetry rule"), and looks up the destination folder ID in an embedded matrix.
5. If a match is found, the file moves to the target folder. If no match, the file moves to a client-specific **Unsorted folder** (graceful degradation, not failure).

---

## 2. Tag Vocabulary

### 2.1 Client Tags (Persona/Identity Tags)

These tags identify which client a file belongs to. They are stripped from the routing key because the intake folder already encodes client identity.

| Client Tag | Workflow | Source |
|---|---|---|
| `Lynn` | Sort LYNN files | `sources/system-snapshots/Sort LYNN files.json` |
| `Maya` | Sort MAYA files | `sources/system-snapshots/Sort MAYA files.json` |
| `Sulima` | Sort SULIMA files | `sources/system-snapshots/Sort SULIMA files.json` |

- **Confidence:** CONFIRMED
- **Impact:** File routing automation
- **Last verified:** 2026-02-27

[UNKNOWN: Are there intake folders and sort workflows for other clients (Devon Ervin, Pat Schoof, Raging Grannies, etc.)? The handoff mentions Maya hasn't created matrices for all clients yet.]

### 2.2 Content Type Tags

These tags describe what the file IS. They are the core vocabulary used across client matrices.

**Tags shared across all three client matrices (Lynn, Maya, Sulima):**

| Tag | Apparent Purpose |
|---|---|
| `Admin` | Administrative documents (contracts, invoices, correspondence) |
| `Asset` | General creative assets |
| `Backup` | Backup copies of files |
| `Copy` | Written text content (blog posts, web copy, manuscripts) |
| `Cover` | Book cover designs or cover images |
| `Design` | Design files (layouts, mockups, graphics) |
| `Featured-image` | Featured/hero images for blog posts or web pages |
| `Headshot` | Portrait/headshot photography |
| `Info` | Reference/informational documents |
| `Inspo` | Inspiration material (mood boards, reference images) |
| `Interior` | Book interior design/layout files |
| `Marketing` | Marketing materials and collateral |
| `Newsletter` | Newsletter content and assets |
| `OLD` | Archived/superseded files |
| `PSD` | Photoshop source files |
| `Social-image` | Social media image assets |
| `Source` | Source/raw material files |
| `Video` | Video files |

Total shared content-type tags: **18**

- **Source:** `sources/system-snapshots/Sort LYNN files.json`, `Sort MAYA files.json`, `Sort SULIMA files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

**Tag present in Lynn and Maya matrices only (NOT in Sulima):**

| Tag | Apparent Purpose | Present In |
|---|---|---|
| `B-Roll` | Supplementary video/image footage for content production | Lynn, Maya |

- **Claim:** The `B-Roll` tag appears in the Lynn and Maya routing matrices but is absent from the Sulima matrix. Sulima's work is poetry/prose books, which may not generate B-Roll footage.
- **Source:** Grep search across all three Sort workflow JSON files
- **Confidence:** CONFIRMED
- **Impact:** Tag vocabulary is not fully uniform across clients; Sulima has 18 content tags, Lynn and Maya have 19.
- **Last verified:** 2026-02-27

### 2.3 Project-Specific Tags (Per-Client)

These tags identify specific projects or works within a client's portfolio.

#### Lynn Haller Projects

| Tag | Project |
|---|---|
| `Hallway-of-Doorknobs` | Book: *Hallway of Doorknobs* |
| `Untitled-Libby` | Book: Untitled Libby project |
| `Workbook` | Workbook companion to a Lynn Haller book |

- **Source:** `sources/system-snapshots/Sort LYNN files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

#### Maya (Self) Projects

| Tag | Project |
|---|---|
| `Painting-Celia` | Painting project related to Celia |
| `Sailor's-Code` | Novel: *Sailor's Code* |
| `Untitled-Kelsey` | Book: Untitled Kelsey project |

- **Source:** `sources/system-snapshots/Sort MAYA files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

[VERIFY: What is "Painting-Celia"? Is this a painting for Sulima's salon or a separate creative project?]

[VERIFY: What is "Untitled-Kelsey"? Is this a client book project or Maya's own work?]

#### Sulima Malzin Projects

| Tag | Project |
|---|---|
| `All-in-the-Soup` | Book: *All in the Soup Together* |
| `Arms-Filled-with-Bittersweet` | Book: *Arms Filled with Bittersweet* |
| `Tributaries` | Book: *Tributaries* |
| `Words-That-Dance` | Book: *Words That Dance* |

- **Source:** `sources/system-snapshots/Sort SULIMA files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

### 2.4 Complete Tag Vocabulary Summary

Total unique tags across all workflows: **31**

- 3 client tags: `Lynn`, `Maya`, `Sulima`
- 18 shared content-type tags (present in all three matrices)
- 1 partially shared content-type tag: `B-Roll` (Lynn and Maya only)
- 3 Lynn-specific project tags
- 3 Maya-specific project tags
- 4 Sulima-specific project tags

Per-client tag totals (non-client tags used in routing):
- Lynn: 22 tags (3 project + 19 content including B-Roll)
- Maya: 22 tags (3 project + 19 content including B-Roll)
- Sulima: 22 tags (4 project + 18 content, no B-Roll)

---

## 3. n8n Workflow Documentation

### 3.1 Sort LYNN Files

- **Workflow ID:** `1MzJgJLu4bfYWJyi`
- **Status:** Active
- **Source:** `sources/system-snapshots/Sort LYNN files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** File management automation (Lynn Haller client)

**Trigger:** Schedule Trigger -- runs every hour

**Flow:**
1. **Schedule Trigger** -- hourly interval
2. **list files in /LYNN** -- Google Drive query: `'1IXaRX3SbkmKT6iXoSECXn54qDOOp6lWI' in parents and trashed = false and mimeType != 'application/vnd.google-apps.folder'`. Returns all non-folder, non-trashed files in the Lynn intake folder.
3. **Parse tags** -- JavaScript Code node (n8n-nodes-base.code, typeVersion 2):
   - Sets `CLIENT_TAG = "Lynn"`
   - Extracts bracketed tags from filename via regex `/\[(.*?)\]/`
   - Splits tag string on whitespace to get individual tags
   - Filters out the client tag (case-insensitive comparison)
   - If 1 non-client tag remains: creates key as `Tag|Tag` (self-pair)
   - If 2+ non-client tags remain: takes first two, sorts alphabetically, creates key as `TagA|TagB`
   - Looks up key in embedded MATRIX constant (tag-pair to folder-ID map)
   - Sets `routingStatus` to `"ok"` or one of four unsorted statuses
4. **If routing okay** -- branches on `routingStatus === "ok"`
   - TRUE path: **Move to target** -- moves file to `targetFolderId` via Google Drive move operation (My Drive)
   - FALSE path: **Move to unsorted** -- moves file to folder `1tp5aFpswfMYtgc_L4jUzXybzxgwJf2_t`

**Error handling statuses:**
- `unsorted-no-brackets` -- filename has no `[...]` tags
- `unsorted-empty-brackets` -- filename has `[]` with nothing inside
- `unsorted-not-enough-tags` -- only the client tag is present, no routing tags
- `unsorted-no-matrix-match` -- tag pair not found in matrix

**Credentials:** Google Drive OAuth2 (ID: `6doKwKDUpt5uiNS6`, name: "Google Drive account")

**n8n instance ID:** `62bd52f8b4ece52a843742601d712f5bb7b30c651ead50c15d3765df46d28374`

### 3.2 Sort MAYA Files

- **Workflow ID:** `d71g649FL1aXowtA`
- **Status:** Active
- **Source:** `sources/system-snapshots/Sort MAYA files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** File management automation (Maya's own files)

**Trigger:** Schedule Trigger -- runs every hour

**Flow:** Identical node structure and code logic to Sort LYNN files, differing only in:
- `CLIENT_TAG = "Maya"`
- Intake folder query targets: `1jAZkSF-w0eaCJxC0iHv4Zyih8bUYcsTj` (the /MAYA folder)
- Unsorted destination: `1ykOtB1Lzao_-YY5kILRep2J-yduW-yvd`
- MATRIX contents reflect Maya-specific project tags (Painting-Celia, Sailor's-Code, Untitled-Kelsey) and folder IDs

**Credentials:** Same Google Drive OAuth2 (ID: `6doKwKDUpt5uiNS6`)

### 3.3 Sort SULIMA Files

- **Workflow ID:** `9Yd0G8URL3yPqXNJ`
- **Status:** Active
- **Source:** `sources/system-snapshots/Sort SULIMA files.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** File management automation (Sulima Malzin client)

**Trigger:** Schedule Trigger -- runs every hour

**Flow:** Identical node structure and code logic to Sort LYNN files, differing only in:
- `CLIENT_TAG = "Sulima"`
- Intake folder query targets: `18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_` (the /SULIMA folder)
- Unsorted destination: `1R0aAzfFYL8pB08eBBG09IYcExjLDE6S1`
- MATRIX contents reflect Sulima-specific project tags (book titles) and folder IDs
- No `B-Roll` tag entries (unlike Lynn and Maya)

**Credentials:** Same Google Drive OAuth2 (ID: `6doKwKDUpt5uiNS6`)

### 3.4 Get Google Folder IDs

- **Workflow ID:** `0ncFxpPpLWYisZ7D`
- **Status:** Inactive (manual trigger only)
- **Source:** `sources/system-snapshots/Get Google Folder IDs.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** Utility workflow for discovering folder IDs to build routing matrices

**Trigger:** Manual ("When clicking 'Execute workflow'")

**Flow:**
1. **When clicking 'Execute workflow'** -- manual trigger
2. **Search files and folders** -- finds all folders that are direct children of `18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_` (the /SULIMA root). Query: `mimeType = 'application/vnd.google-apps.folder' and '[ID]' in parents and trashed = false`, requesting all fields.
3. **Loop Over Items** -- iterates through level-1 folders in batches of 50
4. **Search files and folders1** -- finds subfolders of each level-1 folder (level 2). Always outputs data (alwaysOutputData: true).
5. **Loop Over Items1** -- iterates through level-2 folders in batches of 50
6. **Search files and folders2** -- finds subfolders of each level-2 folder (level 3)
7. **Merge** -- 3-input merge combining results from all three folder depth levels
8. **Edit Fields** -- extracts three fields per folder: `name`, `id`, and `parents[0]`

**Purpose:** This is a utility/discovery workflow used to enumerate the Google Drive folder hierarchy for building the routing matrix. The pinned output data on the "Edit Fields" node captures 21 folders across 3 levels of the Sulima tree (12 level-1, 7 level-2, 2 level-3).

**Credentials:** Same Google Drive OAuth2 (ID: `6doKwKDUpt5uiNS6`)

[VERIFY: Was this workflow also run against other client roots (Lynn, Maya), or only Sulima? The query string is hardcoded to Sulima's root folder ID.]

### 3.5 Amazon Deliveries - Workflow 1 Shipped

- **Workflow ID:** `X6g71NgalPNjSTdH`
- **Status:** Active
- **Source:** `sources/system-snapshots/Amazon Deliveries - Workflow 1 Shipped.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** Personal logistics automation; delivery tracking dashboard

(Full documentation in [Section 7](#7-amazon-delivery-tracking-workflows).)

### 3.6 Amazon Deliveries - Workflow 2 Delivered

- **Workflow ID:** `akXjxGhl5XRGKndy`
- **Status:** Active
- **Source:** `sources/system-snapshots/Amazon Deliveries - Workflow 2 Delivered.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** Personal logistics automation; delivery tracking dashboard

(Full documentation in [Section 7](#7-amazon-delivery-tracking-workflows).)

### 3.7 Shared Workflow Architecture Pattern

- **Claim:** All three Sort workflows share identical code structure, node layout, and logic. They differ only in: CLIENT_TAG value, intake folder ID, unsorted destination folder ID, and MATRIX contents (and B-Roll presence/absence).
- **Source:** Comparison of all three Sort JSON files
- **Confidence:** CONFIRMED
- **Impact:** Any improvements to the routing logic could be applied uniformly; a single parameterized workflow could potentially replace all three
- **Last verified:** 2026-02-27

- **Claim:** All six workflows (3 Sort + Get Folder IDs + 2 Amazon) run on the same n8n instance (instance ID: `62bd52f8b4ece52a843742601d712f5bb7b30c651ead50c15d3765df46d28374`). n8n runs locally in Docker.
- **Source:** `meta.instanceId` field in all workflow JSON files; `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 3, "n8n (Docker, local)")
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

### 3.8 n8n Credential Summary

| Credential | ID | Type | Used By |
|---|---|---|---|
| Google Drive account | `6doKwKDUpt5uiNS6` | googleDriveOAuth2Api | Sort LYNN, Sort MAYA, Sort SULIMA, Get Google Folder IDs |
| Gmail account | `lBw1pGp8GyPaziPM` | gmailOAuth2 | Amazon Shipped, Amazon Delivered |
| OpenAi account | `GgiQA0uPLDlBVqmp` | openAiApi | Amazon Shipped (product name shortening) |
| Google Sheets account | `0cYjI4TjKF2BwA7G` | googleSheetsOAuth2Api | Amazon Shipped, Amazon Delivered |

- **Source:** credentials fields in all workflow JSON files
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

---

## 4. Routing Matrix Rules

### 4.1 The Symmetry Rule

- **Claim:** Tag pairs are sorted alphabetically before matrix lookup, so `[Cover Painting-Celia]` and `[Painting-Celia Cover]` resolve to the same key (`Cover|Painting-Celia`) and route to the same folder. Maya calls this the "symmetry rule."
- **Source:** All three Sort workflow JSON files (the `sortedPair` logic in Parse tags node); `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2)
- **Confidence:** CONFIRMED
- **Impact:** File routing automation -- ensures tag order in the filename doesn't matter
- **Last verified:** 2026-02-27

### 4.2 Matrix Key Construction Rules

1. Extract the content inside `[...]` brackets from the filename using regex `/\[(.*?)\]/`.
2. Split on whitespace to get individual tags.
3. Filter out the client tag (case-insensitive match against CLIENT_TAG constant).
4. If exactly **one** non-client tag remains: the key is `Tag|Tag` (self-pair). Example: `[Lynn Copy]` produces key `Copy|Copy`.
5. If **two or more** non-client tags remain: take the first two (by position in the filename), sort them alphabetically, join with `|` to form `TagA|TagB`.
6. If **zero** non-client tags remain (file has only the client tag or no tags): route to Unsorted (`unsorted-not-enough-tags`).
7. If no brackets are found at all: route to Unsorted (`unsorted-no-brackets`).
8. If brackets are empty: route to Unsorted (`unsorted-empty-brackets`).
9. If the constructed key has no match in the MATRIX: route to Unsorted (`unsorted-no-matrix-match`).

- **Source:** Parse tags code node in all three Sort workflow JSON files (identical logic)
- **Confidence:** CONFIRMED
- **Impact:** Tag parsing and routing logic
- **Last verified:** 2026-02-27

[VERIFY: If a file has 3+ non-client tags, only the first two (in filename order before alphabetical sort) are used. Is this intentional or a simplification? Could relevant routing information be lost in the third tag?]

### 4.3 Matrix Comprehensiveness

- **Claim:** Each client's matrix contains entries for every possible ordered pair (and self-pair) of its non-client tags. For N tags, this is C(N,2) + N = N*(N+1)/2 entries.
- **Source:** Pattern analysis of all three MATRIX objects
- **Confidence:** CONFIRMED (verified by inspection that self-pairs and all cross-pairs are present in each matrix)
- **Impact:** No valid two-tag combination should produce an `unsorted-no-matrix-match` status -- the matrices are complete for known tags. The only way a file hits Unsorted is with unrecognized tags, missing tags, or format errors.
- **Last verified:** 2026-02-27

Per-client matrix sizes:
- **Lynn:** 22 non-client tags -> 22*23/2 = **253 entries**, mapping to **14 unique destination folder IDs**
- **Maya:** 22 non-client tags -> 22*23/2 = **253 entries**, mapping to **18 unique destination folder IDs**
- **Sulima:** 22 non-client tags -> 22*23/2 = **253 entries**, mapping to **16 unique destination folder IDs**

[DISCREPANCY: All three clients have 22 non-client tags each, but the tag sets differ. Lynn and Maya share B-Roll but not each other's project tags. Sulima lacks B-Roll but has 4 project tags instead of 3.]

### 4.4 How Tag Pairs Map to Folders -- General Patterns

The matrix is comprehensive. The routing logic follows observable priority patterns:

**Dominant tags (override most pairings):**
- `Admin` -- almost always routes to the client's Admin folder, regardless of the second tag (exceptions: `Admin|Backup` and `Admin|OLD` route to archive; `Admin|Source` routes to Source; `Admin|PSD` routes to PSD)
- `OLD` / `Backup` -- route to archive/old folder in nearly all combinations
- `Source` -- routes to the Source files folder in most combinations
- `PSD` -- routes to a PSD-specific folder in most combinations
- `Headshot` -- routes to a dedicated Headshot folder in most combinations
- `Video` -- routes to a Video/media folder in most combinations

**Project tags dominate content-type tags:**
- When a project tag (e.g., `Hallway-of-Doorknobs`, `Sailor's-Code`, `All-in-the-Soup`) is paired with a generic content tag (e.g., `Copy`, `Design`, `Asset`), the file typically routes to the project folder. This means "what project is this for" takes precedence over "what kind of file is this."
- Exceptions: `Marketing` and `Newsletter` paired with a project tag often route to the Marketing/Newsletter folder rather than the project folder (the marketing context wins).

**Content-type self-pairs route to category folders:**
- `Copy|Copy` -> client's general Copy folder
- `Design|Design` -> client's general Design folder
- `Marketing|Marketing` -> client's general Marketing folder

**Cross-project pairs:**
- When two project tags are combined (e.g., `Hallway-of-Doorknobs|Untitled-Libby`), they route to a shared/general workspace folder -- typically the Unsorted or general catch-all folder.

- **Source:** Pattern analysis of all three MATRIX objects
- **Confidence:** LIKELY (patterns inferred from data; individual entries are CONFIRMED)
- **Impact:** Understanding routing logic for matrix maintenance and future AI-classification work
- **Last verified:** 2026-02-27

### 4.5 Matrix Maintenance

- **Claim:** The matrix is maintained in Excel as the source of truth, then manually encoded into the n8n workflow's JavaScript Code node. Changes to the Excel do not automatically propagate to n8n.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 6, "Decision: Matrix encoded in n8n as code")
- **Confidence:** CONFIRMED
- **Impact:** Maintenance burden; fragility; sync gap between Excel and n8n
- **Last verified:** 2026-02-27

- **Claim:** The `Google Drive ID Matrix.xlsx` file in system-snapshots is the Excel source of truth for the routing matrices.
- **Source:** `sources/system-snapshots/Google Drive ID Matrix.xlsx` (file exists but is binary; could not be read programmatically in this session)
- **Confidence:** LIKELY
- **Impact:** Source-of-truth document for all routing matrices
- **Last verified:** 2026-02-27

[UNKNOWN: The xlsx file could not be read in this extraction session. Its contents should be cross-referenced against the n8n-embedded matrices to verify they match. If they diverge, the n8n code is the operationally active version (per source-handling rules: system snapshots outrank undated documents).]

---

## 5. Google Drive Folder Structure

### 5.1 Client Intake Folders (Root Level)

| Client | Intake Folder Name | Folder ID | Source |
|---|---|---|---|
| Lynn | /LYNN | `1IXaRX3SbkmKT6iXoSECXn54qDOOp6lWI` | Sort LYNN files.json |
| Maya | /MAYA | `1jAZkSF-w0eaCJxC0iHv4Zyih8bUYcsTj` | Sort MAYA files.json |
| Sulima | /SULIMA | `18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_` | Sort SULIMA files.json |

- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

### 5.2 Sulima Folder Tree (from Get Google Folder IDs pinned data)

The Get Google Folder IDs workflow has pinned output capturing the Sulima folder hierarchy. This is the only client for which we have actual folder names (not just IDs).

Root: `/SULIMA` (`18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_`)

#### Level 1 (Direct children of /SULIMA root)

| Folder Name | Folder ID | Purpose |
|---|---|---|
| BOOK - All in the Soup Together | `1wXYsN253TZTVcBPueU0Ayy595L3WR3SH` | Book project folder |
| BOOK - Tributaries | `1yF_yKsQkQwSwIIPflP8B1nITKy_4MrH1` | Book project folder |
| BOOK - Words That Dance | `1XVA06M6iqqw1tnHE74sTIg-4I-kQXmaC` | Book project folder |
| BOOK - Arms Filled with Bittersweet | `1z-sFkqO7SWcgnPRxaJAk1jziLahxBLWo` | Book project folder |
| Source files | `1oa1DjYEEwdm9wJQW8XDZUDk4jrqlG5QB` | Raw/source material |
| PSDs | `1D4VHUORJN08hK49qS1ZCEZ0CwV7aMR_h` | Photoshop files |
| Admin | `1Wwn62wgXvWL4xPfCsCRGLl2nGC6yMHnn` | Administrative docs |
| SHARED | `1nNs4IL7Vrx_xuRxmKE-kCqmBizvBMgcV` | Shared/collaborative files |
| ~old | `1ASTrMyT8BoZ1R3JFTD4faPJqC2wAwo-Z` | Archive |
| Unsorted | `1R0aAzfFYL8pB08eBBG09IYcExjLDE6S1` | Catch basin for unroutable files |
| Website | `1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_` | Website-related files |
| Marketing | `1D4BOx2y0gJ6IaGCUqBoJ6lOROpoXeUL7` | Marketing materials |

#### Level 2 (Subfolders)

| Folder Name | Folder ID | Parent Folder | Parent ID |
|---|---|---|---|
| Master | `1K9TPBa4lpwe68-HcLdtSPkCvSAq1NpiD` | BOOK - All in the Soup Together | `1wXYsN253TZTVcBPueU0Ayy595L3WR3SH` |
| Master | `1gsjBBx9eGQhjyLE8wL2lONLQNUy5reeX` | BOOK - Tributaries | `1yF_yKsQkQwSwIIPflP8B1nITKy_4MrH1` |
| Master | `1IMsYiNNUoUZFAp_H6uP80d_Az1XCjckc` | BOOK - Words That Dance | `1XVA06M6iqqw1tnHE74sTIg-4I-kQXmaC` |
| Master | `1PL6nLdN9Jc7QmcXAjkMqnieR9R_tY8l3` | BOOK - Arms Filled with Bittersweet | `1z-sFkqO7SWcgnPRxaJAk1jziLahxBLWo` |
| Copy | `1jibhxXBXsZUgsTYiudGBCjD7cdAILiiA` | Website | `1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_` |
| Design | `1Wxi1Qx2VmUJJRXaACsUpIwCwLL-MeLSh` | Website | `1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_` |
| Assets | `17eP1Ps9zdVPnVgQdYS3YuaFMui4sbtPi` | Website | `1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_` |
| Social images | `1NT5GSrqVKJwtOsn6fTB5iZOyxdGqUWbh` | Marketing | `1D4BOx2y0gJ6IaGCUqBoJ6lOROpoXeUL7` |
| Video | `1UfyROSb-qREBTQ_q5guiyyroA3ikYYbB` | Marketing | `1D4BOx2y0gJ6IaGCUqBoJ6lOROpoXeUL7` |

#### Level 3 (Sub-subfolders)

| Folder Name | Folder ID | Parent Folder | Parent ID |
|---|---|---|---|
| Featured images | `1ugMOJqdYEXN530v90JNVR1Jm4CtWtFz5` | Assets (under Website) | `17eP1Ps9zdVPnVgQdYS3YuaFMui4sbtPi` |

- **Source:** `sources/system-snapshots/Get Google Folder IDs.json` (pinned data in "Edit Fields" node)
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

**Sulima folder tree (visual):**
```
/SULIMA (18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_)
  +-- BOOK - All in the Soup Together (1wXYsN...)
  |     +-- Master (1K9TPB...)
  +-- BOOK - Tributaries (1yF_yK...)
  |     +-- Master (1gsjBB...)
  +-- BOOK - Words That Dance (1XVA06...)
  |     +-- Master (1IMsYi...)
  +-- BOOK - Arms Filled with Bittersweet (1z-sFk...)
  |     +-- Master (1PL6nL...)
  +-- Source files (1oa1Dj...)
  +-- PSDs (1D4VHU...)
  +-- Admin (1Wwn62...)
  +-- SHARED (1nNs4I...)
  +-- ~old (1ASTrM...)
  +-- Unsorted (1R0aAz...)
  +-- Website (1kaBTX...)
  |     +-- Copy (1jibhx...)
  |     +-- Design (1Wxi1Q...)
  |     +-- Assets (17eP1P...)
  |           +-- Featured images (1ugMOJ...)
  +-- Marketing (1D4BOx...)
        +-- Social images (1NT5GS...)
        +-- Video (1UfyRO...)
```

Note: The routing matrix routes files to leaf folders within this tree. For example, the tag `Copy` routes to `1jibhxXBXsZUgsTYiudGBCjD7cdAILiiA` which is `Website > Copy`, not a top-level Copy folder.

### 5.3 Sulima Tag-to-Folder ID Cross-Reference

This table maps Sulima routing matrix folder IDs to their confirmed folder names from the Get Google Folder IDs pinned data.

| Folder ID | Confirmed Name | Level | Parent |
|---|---|---|---|
| `1wXYsN253TZTVcBPueU0Ayy595L3WR3SH` | BOOK - All in the Soup Together | 1 | /SULIMA |
| `1yF_yKsQkQwSwIIPflP8B1nITKy_4MrH1` | BOOK - Tributaries | 1 | /SULIMA |
| `1XVA06M6iqqw1tnHE74sTIg-4I-kQXmaC` | BOOK - Words That Dance | 1 | /SULIMA |
| `1z-sFkqO7SWcgnPRxaJAk1jziLahxBLWo` | BOOK - Arms Filled with Bittersweet | 1 | /SULIMA |
| `1oa1DjYEEwdm9wJQW8XDZUDk4jrqlG5QB` | Source files | 1 | /SULIMA |
| `1D4VHUORJN08hK49qS1ZCEZ0CwV7aMR_h` | PSDs | 1 | /SULIMA |
| `1Wwn62wgXvWL4xPfCsCRGLl2nGC6yMHnn` | Admin | 1 | /SULIMA |
| `1ASTrMyT8BoZ1R3JFTD4faPJqC2wAwo-Z` | ~old | 1 | /SULIMA |
| `1R0aAzfFYL8pB08eBBG09IYcExjLDE6S1` | Unsorted | 1 | /SULIMA |
| `1D4BOx2y0gJ6IaGCUqBoJ6lOROpoXeUL7` | Marketing | 1 | /SULIMA |
| `1jibhxXBXsZUgsTYiudGBCjD7cdAILiiA` | Copy | 2 | Website |
| `1Wxi1Qx2VmUJJRXaACsUpIwCwLL-MeLSh` | Design | 2 | Website |
| `17eP1Ps9zdVPnVgQdYS3YuaFMui4sbtPi` | Assets | 2 | Website |
| `1NT5GSrqVKJwtOsn6fTB5iZOyxdGqUWbh` | Social images | 2 | Marketing |
| `1ugMOJqdYEXN530v90JNVR1Jm4CtWtFz5` | Featured images | 3 | Assets |

Note: `1nNs4IL7Vrx_xuRxmKE-kCqmBizvBMgcV` (SHARED) and `1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_` (Website) appear in the folder tree but do NOT appear as routing destinations in the Sulima matrix. Files are routed to their subfolders, not to these parent containers.

### 5.4 Lynn Destination Folders (Inferred from Matrix)

The following unique folder IDs appear as routing destinations in the Lynn matrix. Actual folder names are not available from any source -- names below are inferred from routing patterns.

| Folder ID | Inferred Purpose | Key Evidence |
|---|---|---|
| `1pvum72Gav0Uo8l2Gv7XqWLHAcp7ebOav` | Hallway of Doorknobs project folder | Target for `Hallway-of-Doorknobs|Hallway-of-Doorknobs` self-pair and most HoD + content pairs |
| `1i6YgttRUxsS8eDzNreRHS1kLyFjc8Vbm` | Untitled Libby project folder | Target for `Untitled-Libby|Untitled-Libby` self-pair and most UL + content pairs |
| `1_8XrgWpWpUec4gny3ZkWdj64jT2GJa9c` | Workbook project folder | Target for `Workbook|Workbook` self-pair and most Workbook + content pairs |
| `1tp5aFpswfMYtgc_L4jUzXybzxgwJf2_t` | General/Unsorted folder | Also the "Move to unsorted" destination; target for `Inspo|Inspo`, `Cover|Cover`, `Info|Info`, `Interior|Interior`, and cross-project pairs |
| `1I_HVTZQRAf_MjuUMOLp5geQoy-HQGOs5` | Source files folder | Target for all `Source|*` pairs (except `OLD|Source` which goes to archive) |
| `1nuzqw-fwBX5MyYFA7SCpoxlQ8wv3TzCW` | Marketing/Newsletter folder | Target for `Marketing|Marketing`, `Newsletter|Newsletter`, and all Marketing/Newsletter pairs with non-dominant tags |
| `1h1RSiSTe8nrUgL9drpkfcOyaHLW0Vmr5` | Admin folder | Target for all `Admin|*` pairs (except Admin+Backup/OLD which go to archive, Admin+PSD which goes to PSD, Admin+Source which goes to Source) |
| `1WJLQaqCT-dbigvaPr0qwSqfWa2okmQuj` | Old/Archive folder | Target for all `OLD|*` and `Backup|*` pairs |
| `1hy21y43nwHZaLegDb93aDROu37Vp1JTn` | Headshot folder | Target for all `Headshot|*` pairs (except Headshot+OLD/Backup, Headshot+Video) |
| `1eErACYiOk3jQ2x4SoXSaidAA-qkmTaCG` | Video folder | Target for `Video|Video` self-pair and video-related pairs |
| `1fVOTDgQc_VukLst1Vj82KytYqi_ziha0` | PSD folder | Target for `PSD|PSD` and most PSD-paired combinations |
| `14uCOjuWxxahpyW0J5tCTsPM_LD3cvxyr` | Assets/Media folder | Target for `Asset|Asset`, `Featured-image|*`, `Social-image|*`, `B-Roll|*`, and `Asset|*` content pairs |
| `1TlC1fMx-wUCxZY1xZiY0DEtoBfOgTShm` | Copy folder | Target for `Copy|Copy` and most Copy + non-dominant tag pairs |
| `1Vcm6nyosh52PWrXYbZw0z1hhlfD5bNIo` | Design folder | Target for `Design|Design` and most Design + non-dominant tag pairs |

- **Source:** `sources/system-snapshots/Sort LYNN files.json` (MATRIX object)
- **Confidence:** Folder IDs CONFIRMED; folder names LIKELY (inferred from routing patterns)
- **Last verified:** 2026-02-27

### 5.5 Maya Destination Folders (Inferred from Matrix)

| Folder ID | Inferred Purpose | Key Evidence |
|---|---|---|
| `1Uzt32vdzpwWtCvlMdeebxtAKYtcWjuqg` | Admin folder | Target for all `Admin|*` pairs (except Admin+Backup/OLD, Admin+Source, Admin+PSD) |
| `1I8Dez0rhnfK1BdJs4O_7ZALuUN5bIurm` | General Asset/Info folder | Target for `Asset|Asset`, `Info|Info`, `Asset|Info`, `Asset|Marketing` |
| `19dJbRq6GVwGrt9mZJ3NegsuriQ7G57vt` | Video/B-Roll folder | Target for `Video|Video` and most Video-paired combinations, `B-Roll|Marketing`, `Asset|B-Roll` |
| `1FPVSF11YWp7DV9SCG-6uUx43KYfhn84i` | Old/Backup/Archive folder | Target for all `OLD|*` and most `Backup|*` pairs |
| `1ykOtB1Lzao_-YY5kILRep2J-yduW-yvd` | General workspace / Unsorted | Also the "Move to unsorted" destination; target for many generic pairs and cross-project pairs |
| `1R-P27joAfrXZ_BAAoXefChIegp_RFoFW` | Featured images folder | Target for `Featured-image|Featured-image` and most Featured-image pairs |
| `1zeczUMlzYUAQv6t1ZFF7jlnsLiPswUow` | Headshot folder | Target for `Headshot|Headshot` and most Headshot pairs |
| `1qUXWXlXls6AuziR3mRgM2QESSlalhpSF` | Social images folder | Target for `Social-image|Social-image` and most Social-image pairs |
| `121Q8rdnvAjNHDkawLfHg1IAV8Ay02DxJ` | Source files folder | Target for `Source|Source` and most Source pairs |
| `1RTlmvtOz279OOwW6rzsKi07hzWmbIFdE` | Untitled Kelsey project folder | Target for `Untitled-Kelsey|Untitled-Kelsey` and Untitled-Kelsey + content pairs |
| `1jxC5-kXTYEthBsr18OtKpgTbs3XTKHfV` | Copy folder | Target for `Copy|Copy`, `Copy|Info`, `Copy|Marketing` |
| `1R6_DoZSY0HqNG3atkRihKyjnXlXM-qLn` | Design folder | Target for `Design|Design`, `Design|Info`, `Design|Marketing` |
| `1liZVn5ML72uIAoAhHkp-gcvV2PUbMxIC` | Marketing folder | Target for `Marketing|Marketing`, `Cover|Marketing`, `Info|Marketing`, `Interior|Marketing`, `Inspo|Marketing`, and project + Marketing pairs |
| `1Ge-0kbMlbbq3Mm6u9ueKITY5H0oFxbXU` | Newsletter folder | Target for `Newsletter|Newsletter` and most Newsletter-paired combinations |
| `1HYgKE8KHG3aHa5yssRP5QkYSCkixs6Iv` | Painting-Celia project folder | Target for `Painting-Celia|Painting-Celia` and most Painting-Celia + content pairs; also B-Roll + various tags |
| `1tZYdQCEeHiMObOUF-vn2Zx_IAgH-pQe2` | Sailor's Code project folder | Target for `Sailor's-Code|Sailor's-Code` and Sailor's-Code + content pairs |

**Maya PSD sub-folders (granular routing):**

Maya's PSD routing is more granular than other clients. Multiple distinct PSD folder IDs appear depending on the paired content type. All IDs share a common prefix `1epreGeMwReI4rZGEjathYmZXj34jDL` with incrementing 2-digit suffixes:

| Folder ID suffix | Routed from these tag pairs |
|---|---|
| `...jDL67` | `Asset|PSD`, `Copy|PSD`, `Cover|PSD`, `Design|PSD`, `PSD|PSD`, `PSD|Video` |
| `...jDL73` | `Marketing|PSD` |
| `...jDL74` | `Newsletter|PSD` |
| `...jDL75` | `Inspo|PSD` |
| `...jDL76` | `Admin|PSD`, `B-Roll|PSD`, `Featured-image|PSD`, `PSD|Social-image` |
| `...jDL78` | `Info|PSD` |
| `...jDL80` | `Headshot|PSD` |
| `...jDL81` | `Interior|PSD` |
| `...jDL84` | `Painting-Celia|PSD`, `PSD|Sailor's-Code`, `PSD|Untitled-Kelsey` |

[VERIFY: Are these 9 distinct folders? The incrementing ID suffix pattern suggests they were created in sequence, possibly as sub-folders within a PSD parent. Is this intentional sub-categorization of PSDs by content type?]

- **Source:** `sources/system-snapshots/Sort MAYA files.json` (MATRIX object)
- **Confidence:** Folder IDs CONFIRMED; folder names LIKELY (inferred)
- **Last verified:** 2026-02-27

### 5.6 Unsorted Folder Mapping

| Client | Unsorted Folder ID | Source |
|---|---|---|
| Lynn | `1tp5aFpswfMYtgc_L4jUzXybzxgwJf2_t` | Sort LYNN files.json ("Move to unsorted" node, line 100) |
| Maya | `1ykOtB1Lzao_-YY5kILRep2J-yduW-yvd` | Sort MAYA files.json ("Move to unsorted" node, line 100) |
| Sulima | `1R0aAzfFYL8pB08eBBG09IYcExjLDE6S1` | Sort SULIMA files.json ("Move to unsorted" node, line 100); confirmed as "Unsorted" in Get Google Folder IDs pinned data |

- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

Note: For Lynn and Maya, the Unsorted folder ID is also used as the matrix destination for several "generic" tag pairs (e.g., `Inspo|Inspo`, cross-project pairs). This means some files route to Unsorted intentionally via the matrix, not just as a fallback.

---

## 6. Client-to-Folder Mapping

### 6.1 Summary Table

| Client | Intake Folder | Root Folder ID | n8n Workflow | Workflow ID | Project Tags | Content Tags |
|---|---|---|---|---|---|---|
| Lynn Haller | /LYNN | `1IXaRX3SbkmKT6iXoSECXn54qDOOp6lWI` | Sort LYNN files | `1MzJgJLu4bfYWJyi` | Hallway-of-Doorknobs, Untitled-Libby, Workbook | 19 (includes B-Roll) |
| Maya (self) | /MAYA | `1jAZkSF-w0eaCJxC0iHv4Zyih8bUYcsTj` | Sort MAYA files | `d71g649FL1aXowtA` | Painting-Celia, Sailor's-Code, Untitled-Kelsey | 19 (includes B-Roll) |
| Sulima Malzin | /SULIMA | `18fqDFp35Upth9zKnrzgDAWGWfmTjLJJ_` | Sort SULIMA files | `9Yd0G8URL3yPqXNJ` | All-in-the-Soup, Arms-Filled-with-Bittersweet, Tributaries, Words-That-Dance | 18 (no B-Roll) |

- **Source:** All three Sort workflow JSON files
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

### 6.2 Clients Without Routing Workflows

- **Claim:** Only three clients (Lynn, Maya, Sulima) have active n8n sort workflows. Other known clients and organizations do not have automated file routing.
- **Source:** Absence from system snapshot files; `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` stating Maya "has yet to create the complicated (and hard to update) matrices for all clients"
- **Confidence:** LIKELY
- **Impact:** File routing coverage gap; scaling challenge
- **Last verified:** 2026-02-27

Known clients/entities mentioned in the handoff that lack routing workflows:
- Devon Ervin
- Pat Schoof
- Portland Raging Grannies (PRG)
- International Raging Grannies (IRG)

[VERIFY: Does Maya have Google Drive intake folders for other clients even without n8n workflows? Or do those clients' files follow a different organizational pattern entirely?]

---

## 7. Amazon Delivery Tracking Workflows

These are not file-routing workflows but are part of the broader n8n automation system. They route structured data from email into a Google Sheet.

### 7.1 Amazon Deliveries - Workflow 1 Shipped

- **Workflow ID:** `X6g71NgalPNjSTdH`
- **Status:** Active
- **Source:** `sources/system-snapshots/Amazon Deliveries - Workflow 1 Shipped.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** Personal logistics automation; delivery tracking dashboard

**Trigger:** Gmail Trigger -- polls every hour at minute :01, filter: `label:Amazon newer_than:1d`

**Flow:**
1. **Gmail Trigger** -- hourly poll for Amazon-labeled emails from last 24 hours
2. **Filter: Amazon Shipped Senders** -- keeps only emails where `From` contains `shipment-tracking@amazon.com`
3. **Filter: Shipped Subjects Only** -- keeps only subjects matching regex `^Shipped:` OR containing "Your order has shipped" (pharmacy variant)
4. **Get a message** -- fetches full email body via Gmail API (simple: false, gets full MIME)
5. **Parse Email Body** -- JavaScript code node handling two distinct email formats:
   - **Standard Amazon (from shipment-tracking@amazon.com):**
     - Extracts order number via regex: `Order\s*#\s*\n?\s*([\d-]+)`
     - Extracts items via regex: `^\* (.+?)\n\s*Quantity:\s*(\d+)` (product name + quantity)
     - Extracts delivery date from "Arriving [date]" -- parses "today", "tomorrow", full month names, and 3-letter month abbreviations relative to email date
   - **Amazon Pharmacy (from no-reply@pharmacy.amazon.com):**
     - Generates synthetic order number: `PHARM-[emailTimestamp]`
     - Extracts item name from "Your order for X has shipped"
     - Extracts date from "will arrive by [date]"
6. **Build OpenAI Prompt** -- constructs a GPT-4o-mini API request to shorten product names to 2-4 word human-friendly labels. Prompt: "You are a product name shortener. Given a list of Amazon product names, return a JSON array of short, human-friendly labels (2-4 words, no brand names, no dimensions, no model numbers)."
7. **OpenAI: Clean Item Names** -- HTTP POST to `https://api.openai.com/v1/chat/completions` using predefined OpenAI credential
8. **Merge Pretty Names & Explode Rows** -- parses OpenAI JSON response, falls back to raw names on parse failure. Creates one row per item with fields: order_number, item_name, pretty_name, quantity, expected_date, status ("pending"), delivered_date ("")
9. **Google Sheets: Append Row** -- appendOrUpdate operation to Google Sheet, matching on order_number + item_name

**Target Sheet:** `1NwqF3wKZU951okxNrNXOzvs_tPxf-hZIm3WZOJ-0V4U`, sheet name "Amazon Deliveries"

**Credentials:**
- Gmail OAuth2 (ID: `lBw1pGp8GyPaziPM`, name: "Gmail account")
- OpenAI API (ID: `GgiQA0uPLDlBVqmp`, name: "OpenAi account")
- Google Sheets OAuth2 (ID: `0cYjI4TjKF2BwA7G`, name: "Google Sheets account")

**Settings:** Timezone: America/Los_Angeles; callerPolicy: workflowsFromSameOwner; MCP availability: disabled

### 7.2 Amazon Deliveries - Workflow 2 Delivered

- **Workflow ID:** `akXjxGhl5XRGKndy`
- **Status:** Active
- **Source:** `sources/system-snapshots/Amazon Deliveries - Workflow 2 Delivered.json`
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27
- **Impact:** Personal logistics automation; delivery tracking dashboard

**Trigger:** Gmail Trigger -- polls every hour at minute :05, filter: `label:Amazon subject:Delivered`

**Flow:**
1. **Gmail Trigger** -- hourly poll for Amazon delivery confirmation emails
2. **Filter: Delivered Senders** -- keeps only emails where `From` contains `order-update@amazon.com`
3. **Filter: Delivered Subjects Only** -- keeps only subjects matching regex `^Delivered:`
4. **Get a message** -- fetches full email body via Gmail API (simple: false)
5. **Parse Delivered Email** -- extracts order number via regex `Order\s*#\s*\n?\s*([\d-]+)`. Sets delivered_date to today's date (YYYY-MM-DD format).
6. **Sheets: Find Pending Rows** -- reads from same Google Sheet, filtering by order_number match
7. **Sheets: Update to Delivered** -- updates matching rows: sets `status = "delivered"`, sets `delivered_date` from Parse Delivered Email node. Match key: order_number + item_name.

**Credentials:** Same Gmail and Google Sheets credentials as Workflow 1.

### 7.3 Amazon Delivery Tracking Data Schema

The Google Sheet "Amazon Deliveries" (document ID: `1NwqF3wKZU951okxNrNXOzvs_tPxf-hZIm3WZOJ-0V4U`) has these columns:

| Column | Type | Set by | Purpose |
|---|---|---|---|
| order_number | string | Workflow 1 | Amazon order ID or synthetic `PHARM-[timestamp]` |
| item_name | string | Workflow 1 | Full Amazon product name |
| pretty_name | string | Workflow 1 | AI-shortened human-friendly name (2-4 words via GPT-4o-mini) |
| quantity | number | Workflow 1 | Item quantity |
| expected_date | string (YYYY-MM-DD) | Workflow 1 | Expected delivery date |
| status | string | Both | `"pending"` (set by Workflow 1) or `"delivered"` (updated by Workflow 2) |
| delivered_date | string (YYYY-MM-DD) | Workflow 2 | Actual delivery date; empty until delivered |

- **Source:** Google Sheets node column schemas in both Amazon workflow JSON files
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

### 7.4 Amazon Workflow Design Notes

- **Claim:** The two workflows are deliberately separated (Shipped vs. Delivered) rather than combined into one, because they trigger on different email senders and subjects, and have different processing logic.
- **Source:** Structural analysis of both workflow JSON files
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

- **Claim:** The Gmail label `Amazon` (internal ID: `Label_6582208580953641436`) pre-filters Amazon emails, reducing the search scope for both workflows.
- **Source:** `sources/system-snapshots/Amazon Deliveries - Workflow 1 Shipped.json` (Gmail Trigger filter); `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 3)
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

- **Claim:** The Shipped workflow uses `newer_than:1d` in the Gmail query to only process recent emails, preventing reprocessing of old shipment notifications. The appendOrUpdate operation in Google Sheets (matching on order_number + item_name) provides idempotency -- re-processing the same email won't create duplicates.
- **Source:** Gmail Trigger node config and Google Sheets node config in Workflow 1
- **Confidence:** CONFIRMED
- **Last verified:** 2026-02-27

---

## 8. Design Principles

These are architectural choices Maya has made that should inform any future automation work.

### 8.1 Graceful Degradation over Hard Failure

- **Claim:** Files that cannot be routed go to an Unsorted folder rather than failing or staying in the intake folder. The Unsorted folder is "a deliberate catch basin, not a failure state."
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2 and Section 6); confirmed by "Move to unsorted" node in all three Sort workflow JSON files
- **Confidence:** CONFIRMED
- **Impact:** Design principle for all file management automation
- **Last verified:** 2026-02-27

### 8.2 Describe-What-It-Is, Not Where-It-Goes

- **Claim:** Maya's tagging philosophy is to describe the nature of a file (content type + project), not its destination. The system handles placement. "The reason this works so well for me is that I never have to remember where things go."
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 6)
- **Confidence:** CONFIRMED
- **Impact:** Core design philosophy for file management
- **Last verified:** 2026-02-27

### 8.3 Tags in Filenames, Not Metadata

- **Claim:** Tags are embedded in filenames using square brackets (TagSpaces convention), not stored as file metadata. This makes them visible everywhere -- in Drive, in search results, in n8n string parsing -- and portable across systems.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 6); regex `/\[(.*?)\]/` in all Sort workflow Parse tags nodes
- **Confidence:** CONFIRMED
- **Impact:** Tag extraction logic; file naming conventions; cross-system portability
- **Last verified:** 2026-02-27

### 8.4 Persistence and Autonomy

- **Claim:** Maya prefers systems that operate without her active involvement. She chose n8n (Docker, runs in background) over tools requiring a desktop app to be open (e.g., she explicitly chose n8n over Cowork for the delivery tracking automation because Cowork requires keeping a desktop app open).
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 6, "Decision: n8n over Cowork")
- **Confidence:** CONFIRMED
- **Impact:** Architecture choices for all automation; preference for background/server processes over desktop-dependent tools
- **Last verified:** 2026-02-27

### 8.5 Hourly Batch Processing (Not Real-Time)

- **Claim:** All active n8n workflows use hourly schedule triggers, not real-time file-watch or webhook triggers. Files sit in intake folders until the next hourly cycle processes them.
- **Source:** Schedule Trigger nodes in all three Sort workflows (interval: hours); Gmail Trigger nodes in Amazon workflows (everyHour at minute :01 and :05)
- **Confidence:** CONFIRMED
- **Impact:** Latency expectation: files and emails are processed within 0-60 minutes of arrival, not instantly
- **Last verified:** 2026-02-27

---

## 9. Known Gaps and Uncertainties

### Questions for Maya [VERIFY]

1. **Painting-Celia project:** What is this? Is it a painting for Sulima's salon, a separate creative project, or something else?
2. **Untitled-Kelsey project:** What is this? A client book or Maya's own work?
3. **Three-tag files:** When a file has 3+ non-client tags, only the first two are used for routing. Is this intentional or a simplification? Could important routing information be lost?
4. **Get Google Folder IDs scope:** Was this utility workflow run against Lynn and Maya roots too, or only Sulima? (The query is hardcoded to Sulima's root folder.)
5. **Maya PSD sub-folders:** The Maya matrix routes to 9 distinct PSD folder IDs with incrementing suffixes. Are these intentionally separate sub-categorized PSD folders?
6. **Other clients:** Do Devon Ervin, Pat Schoof, Raging Grannies, etc. have Google Drive intake folders even without n8n workflows?
7. **Excel-to-n8n sync:** When was the last time the Excel matrix was synced to n8n? Are the current n8n matrices up to date with the Excel source?
8. **B-Roll absence in Sulima:** Is the absence of the B-Roll tag in Sulima's matrix intentional (Sulima doesn't produce video footage), or was it an oversight when building the matrix?

### Data Gaps [UNKNOWN]

1. **Google Drive ID Matrix.xlsx contents:** The binary xlsx file could not be read programmatically. Its contents should be cross-referenced against the n8n-embedded matrices for discrepancies. If they diverge, the n8n code is the operationally active version.
2. **Full Lynn folder tree:** Only folder IDs are known from the matrix; actual folder names and hierarchy are not captured in any readable source.
3. **Full Maya folder tree:** Same as Lynn -- only IDs and inferred names from routing patterns.
4. **Other client folder structures:** No data available for Devon, Pat, PRG, IRG, or other clients.
5. **TagSpaces configuration:** No source file captures TagSpaces settings, tag groups, or color coding. [UNKNOWN: Does Maya use TagSpaces tag groups or color coding beyond the bracket-in-filename convention?]
6. **Workflow error/execution history:** No data on how often files hit Unsorted, what the most common unroutable patterns are, or workflow execution success rates.
7. **Matrix update frequency:** No data on how often the matrix is updated or when it was last changed.
8. **Folders in tree not in matrix:** The Sulima folder tree includes `SHARED` (`1nNs4IL7Vrx_xuRxmKE-kCqmBizvBMgcV`) and `Website` (`1kaBTXf2AfKiaRQFJ4NWqKNYwltwwp0M_`) as parent folders, but no matrix entries route directly to them. Their children receive files. Also, the `Master` subfolders within each book folder are not routing targets. [UNKNOWN: What is the SHARED folder used for? How are Master subfolders populated?]

### Known Pain Points (from Handoff)

- **Matrix maintenance is manual and fragile:** Excel is source of truth, JavaScript code in n8n is the operational copy, no sync mechanism exists between them.
- **Not all clients have workflows:** Scaling to new clients requires building new matrices from scratch. Maya described this as a barrier.
- **Downloads folder accumulation:** Tagged files don't get moved until Maya clears her downloads folder into Drive -- this is a manual step before the automation kicks in.
- **Maya wants smarter routing:** AI-based classification (send filename to Claude API, get tag suggestions), automatic matrix gap detection (when a file hits Unsorted, query AI for routing suggestion), and cascading actions (file landing triggers downstream tasks like ClickUp task creation).
- **The ambition-implementation gap:** Maya envisions auto-tagging, blog QA checkpoints, client email drafting, comment reply automation -- none of which are built yet. The gap between vision and available time is "a recurring source of low-grade frustration."

---

*Extracted from system snapshots (highest-fidelity source per source-handling rules) and prior work (cross-verified against snapshots where possible). No corrections found in maya-corrections.md. Extraction date: 2026-02-27.*
