# Domain Plan: File Management

## Purpose
Automate file routing from Google Drive intake folders to destination folders based on TagSpaces filename tags. Replace the current n8n matrix-based system with something that scales beyond 3 clients without requiring manually encoded Excel matrices.

## Inputs
- knowledge/conventions.md — TagSpaces format, symmetry rule, client tag behavior
- knowledge/tools.md — n8n workflow details, TagSpaces description, Google Drive structure
- data/file-routing.yaml — Tag vocabulary, 3 active workflows with IDs, routing pipeline description
- data/client-registry.yaml — Clients with file routing (Lynn, Maya, Sulima) and those without

## System Overview
**Pipeline:** TagSpaces → Google Drive intake folder → n8n hourly trigger → tag-pair matrix lookup → destination folder (or Unsorted).

**Tagging:** Files are tagged in TagSpaces with up to 2 bracketed tags appended to the filename (e.g., `document[Cover Painting-Celia].pdf`). Tags are visible everywhere — Drive, search, n8n string parsing. No metadata storage.

**Routing logic:** n8n parses the filename, extracts tag pairs, alphabetically sorts them (symmetry rule — `[Cover Painting-Celia]` and `[Painting-Celia Cover]` route identically), then looks up the sorted pair in a hardcoded matrix to find the destination folder ID. Client tags (Lynn, Maya, Sulima) are stripped from the routing key because the intake folder already encodes client identity.

**Current state:** 3 active file sort workflows (Lynn, Maya, Sulima), running hourly. The routing matrices are manually encoded into n8n workflow code from Excel source-of-truth spreadsheets. No automated sync between Excel and n8n.

**Graceful degradation:** Files with unrecognized tag pairs route to a client-specific Unsorted folder. This folder also serves a psychological function — it's reassurance that nothing is lost.

**Scaling barrier:** Adding a new client requires building a new matrix in Excel, manually encoding it into a new n8n workflow, and maintaining both. Maya wants a system where adding a client doesn't require this manual matrix work. All clients already have Google Drive folders.

**Tag vocabulary:** 31 total tags across 3 clients — 3 client tags, 17 universal content tags, 1 partial tag (B-Roll, present in Lynn/Maya but not Sulima), and project-specific tags per client (3 for Lynn, 3 for Maya, 4 for Sulima).
