# Domain Plan: Email Triage

## Purpose
Automate email classification, labeling, and routing in Maya's Gmail hub. Build on the existing 48-filter foundation to handle messages that currently require manual sorting, and support identity-aware reply drafting.

## Inputs
- knowledge/conventions.md — Identity routing (two-axis model), email label hierarchy, communication style
- knowledge/tools.md — Gmail hub architecture, Send-As configuration, filter system
- data/email-identities.yaml — 17 Send-As identities with routing rules, 27 labels, hub account details
- data/client-registry.yaml — Client names mapped to email contexts

## System Overview
**Hub model:** stephbairey@gmail.com is the single inbox of truth. All domain email (bairey.com, linguaink.com, linguainkmedia.com, tomahawkdestiny.com, lynnahaller.com) forwards at the hosting level. One inbox, 17 Send-As identities, 27 labels, 48 filters.

**Identity routing (two-axis model):**
- **Name axis:** Steph = business, operations, technical, government-name contexts. Maya = creative, author, writing community.
- **Domain axis:** Which organization. bairey.com (personal), linguaink.com (publishing), linguainkmedia.com (marketing/coding), tomahawkdestiny.com (moorage), lynnahaller.com (client), raginggrannies (PRG/IRG).

**Reply behavior:** Gmail auto-sends from whichever address received the inbound message. No manual switching for replies. For new compositions, the decision is "what hat am I wearing?" — but relationship history can override strict role logic.

**Existing filter system:** 48 filters organized across 9 categories handle automatic labeling, archiving, and noise management. These are the current automated triage layer.

**Manual triage:** Messages that don't match existing filters require Maya to label and potentially route them. Client emails often need identity-aware context (which name does this person know Maya by?).

**Label structure:** 27 labels organized by function — Client/relationship (Amazon, Authors with sub-labels, Lynn, Nicole, Sulima), Organizational (ARC, PRG with sub-labels, Tomahawk), Business (Business with sub-labels, Jobs, Lingua Ink, Taxes), Content/reference (Articles, KEEPERS, Substack), Personal (My Travel, Snoozed).

**Communication style constraints:** Warm but not sycophantic, professional but not corporate. No em-dashes. No AI-tell markers. Match Maya's energy — concise when quick, deep when architectural. Any draft must sound like a specific human, not a generic AI.
