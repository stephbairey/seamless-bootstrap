# Email System Extraction

**Extracted:** 2026-02-27
**Phase:** 1 (Technical Systems)
**Primary sources:**
- `sources/system-snapshots/GmailFilters.xml` (system snapshot, exported 2026-02-28)
- `sources/operator-notes/email-send-as-config.md` (operator note, 2026-02-27)

**Supporting sources:**
- `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md`
- `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`

---

## 1. Gmail Account and Owner

- **Claim:** The primary Gmail account is stephbairey@gmail.com, owned by "Steph Bairey" (Maya's legal name identity). This single account serves as the hub for all email sending across every identity.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (author element); `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Email automation (SL); any automated sending must route through this account
- **Last verified:** 2026-02-27

---

## 2. Send-As Identities (16 Total)

Maya sends from 16 different addresses through the single stephbairey@gmail.com Gmail account. All outbound email originates from Gmail regardless of the from-address displayed.

### 2a. Gmail-Native Addresses (No External Mail Server)

| # | From Address | Display Name | Reply-To | Notes |
|---|---|---|---|---|
| 1 | stephbairey@gmail.com | Steph Bairey | stephbairey@gmail.com | Default sending address |
| 2 | grannynewsletter@gmail.com | PRG Newsletter | (default) | PRG newsletter distribution |
| 3 | mjbairey@gmail.com | Maya Bairey | mjbairey@gmail.com | Explicit reply-to set |
| 4 | pdxraginggrannies@gmail.com | Portland Raging Grannies | (default) | PRG organizational identity |
| 5 | scb.zombie@gmail.com | Steph Bairey | scb.zombie@gmail.com | Explicit reply-to set |
| 6 | webgranny@gmail.com | Steph Bairey | (default) | |

**Fact records:**

- **Claim:** stephbairey@gmail.com is the default sending address with display name "Steph Bairey."
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Email automation -- default identity for personal correspondence
- **Last verified:** 2026-02-27

- **Claim:** mjbairey@gmail.com uses display name "Maya Bairey" and has an explicit reply-to of mjbairey@gmail.com.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Identity routing -- this is the "Maya" personal address as distinct from the "Steph" default
- **Last verified:** 2026-02-27

- **Claim:** scb.zombie@gmail.com uses display name "Steph Bairey" and has an explicit reply-to of scb.zombie@gmail.com. It is also the Microsoft account login for the upstairs dev machine (Windows username: scbzo).
- **Source:** `sources/operator-notes/email-send-as-config.md`; `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** Identity routing; dev machine credential mapping
- **Last verified:** 2026-02-27

- **Claim:** grannynewsletter@gmail.com is used for PRG newsletter distribution, with display name "PRG Newsletter."
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** PRG newsletter automation
- **Last verified:** 2026-02-27

- **Claim:** pdxraginggrannies@gmail.com is the PRG organizational identity, with display name "Portland Raging Grannies."
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** PRG organizational email automation
- **Last verified:** 2026-02-27

- **Claim:** webgranny@gmail.com uses display name "Steph Bairey."
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** PRG web-related correspondence
- **Last verified:** 2026-02-27
- [VERIFY: What is webgranny@gmail.com actually used for? It parallels webgranny@bairey.com but the use case is unclear.]

### 2b. bairey.com Domain Addresses

| # | From Address | Display Name | Mail Server | Notes |
|---|---|---|---|---|
| 7 | maya@bairey.com | Maya Bairey | mail.bairey.com (SSL 465) | Explicitly "Not an alias" |
| 8 | steph@bairey.com | Steph Bairey | mail.bairey.com (SSL 465) | |
| 9 | webgranny@bairey.com | Steph Bairey | mail.bairey.com (SSL 465) | |

**Fact records:**

- **Claim:** maya@bairey.com is explicitly marked "Not an alias" in Maya's notes, distinguishing it from other send-as addresses. It is a separate identity, not just a display-name alias.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Identity routing -- this is a structurally distinct identity, not interchangeable with other "Maya Bairey" addresses
- **Last verified:** 2026-02-27
- [VERIFY: What makes maya@bairey.com "not an alias" -- does it have its own mailbox? Does mail sent TO this address arrive separately from stephbairey@gmail.com?]

- **Claim:** steph@bairey.com and webgranny@bairey.com both use display name "Steph Bairey" and route through mail.bairey.com on SSL port 465.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Domain email infrastructure; identity routing
- **Last verified:** 2026-02-27

### 2c. linguaink.com Domain Addresses

| # | From Address | Display Name | Mail Server | Notes |
|---|---|---|---|---|
| 10 | info@linguaink.com | Lingua Ink | dfw-s07.nixihost.com (SSL 465) | Business identity |
| 11 | maya@linguaink.com | Maya Bairey | mail.linguaink.com (SSL 465) | |
| 12 | steph@linguaink.com | Steph Bairey | dfw-s07.nixihost.com (SSL 465) | |

**Fact records:**

- **Claim:** info@linguaink.com uses display name "Lingua Ink" (not a personal name) and routes through nixihost (dfw-s07). This is the business-facing identity.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Business email automation; client communication identity
- **Last verified:** 2026-02-27

- **Claim:** maya@linguaink.com uses display name "Maya Bairey" but routes through mail.linguaink.com (SSL 465), a different server than info@ and steph@ which use dfw-s07.nixihost.com.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Mail infrastructure -- different SMTP servers for addresses on the same domain
- **Last verified:** 2026-02-27
- [DISCREPANCY: maya@linguaink.com routes through mail.linguaink.com while info@linguaink.com and steph@linguaink.com route through dfw-s07.nixihost.com. This may indicate separate hosting or a DNS configuration difference.]

### 2d. linguainkmedia.com Domain Address

| # | From Address | Display Name | Mail Server | Notes |
|---|---|---|---|---|
| 13 | steph@linguainkmedia.com | Steph Bairey | mail.linguainkmedia.com (SSL 465) | |

**Fact record:**

- **Claim:** steph@linguainkmedia.com is a send-as address on the linguainkmedia.com domain, routed through mail.linguainkmedia.com (SSL 465).
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Brand identity -- linguainkmedia.com is distinct from linguaink.com; plugin authorship uses linguainkmedia.com URL
- **Last verified:** 2026-02-27
- [VERIFY: What is the relationship between linguaink.com and linguainkmedia.com? Are they the same entity with two domains, or do they serve different purposes?]

### 2e. tomahawkdestiny.com Domain Addresses

| # | From Address | Display Name | Mail Server | Notes |
|---|---|---|---|---|
| 14 | arc@tomahawkdestiny.com | ARC | mail.tomahawkdestiny.com (SSL 465) | ARC organizational identity |
| 15 | steph.bairey.arc@tomahawkdestiny.com | Steph Bairey (ARC) | mail.tomahawkdestiny.com (SSL 465) | Personal within org |
| 16 | webmaster@tomahawkdestiny.com | Webmaster | iah-s01.nixihost.com (TLS 587) | Different server than other TDA addresses |

**Fact records:**

- **Claim:** arc@tomahawkdestiny.com is the ARC organizational identity (display name "ARC"), while steph.bairey.arc@tomahawkdestiny.com is Maya's personal-within-org identity (display name "Steph Bairey (ARC)"). This is a deliberate split between organizational and personal roles within the same organization.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Identity routing -- organizational vs. personal communication within TDA/ARC
- **Last verified:** 2026-02-27

- **Claim:** webmaster@tomahawkdestiny.com routes through a different mail server (iah-s01.nixihost.com, TLS 587) than the other TDA addresses (mail.tomahawkdestiny.com, SSL 465).
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Mail infrastructure -- the webmaster role may have been set up separately or hosted differently
- **Last verified:** 2026-02-27

### 2f. lynnahaller.com Domain Address

| # | From Address | Display Name | Mail Server | Notes |
|---|---|---|---|---|
| - | doorknobs@lynnahaller.com | Maya Bairey | mail.lynnahaller.com (SSL 465) | |

**Fact record:**

- **Claim:** doorknobs@lynnahaller.com is a send-as address on a client domain (Lynn Haller), with display name "Maya Bairey." This is likely related to the "Hallway of Doorknobs" book project mentioned in the daily processes handoff.
- **Source:** `sources/operator-notes/email-send-as-config.md`; `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (mentions "Hallway of Doorknobs")
- **Confidence:** CONFIRMED (address exists); LIKELY (connection to Doorknobs book)
- **Impact:** Client email; publishing operations for Lynn Haller
- **Last verified:** 2026-02-27

---

## 3. Identity Routing Summary

Maya operates across multiple identity contexts. This section maps which email addresses serve which identity.

### "Steph Bairey" (Legal Name Identity)
- stephbairey@gmail.com (default)
- scb.zombie@gmail.com
- steph@bairey.com
- steph@linguaink.com
- steph@linguainkmedia.com
- steph.bairey.arc@tomahawkdestiny.com (personal-within-org for ARC)
- webgranny@bairey.com
- webgranny@gmail.com

### "Maya Bairey" (Preferred Name Identity)
- mjbairey@gmail.com
- maya@bairey.com (explicitly "not an alias")
- maya@linguaink.com
- doorknobs@lynnahaller.com

### "Lingua Ink" (Business Entity Identity)
- info@linguaink.com (display name: "Lingua Ink")

### "PRG" (Portland Raging Grannies Organizational Identity)
- pdxraginggrannies@gmail.com (display name: "Portland Raging Grannies")
- grannynewsletter@gmail.com (display name: "PRG Newsletter")

### "ARC/TDA" (Tomahawk Destiny Association Organizational Identity)
- arc@tomahawkdestiny.com (display name: "ARC")
- webmaster@tomahawkdestiny.com (display name: "Webmaster")

### Key Observations

- **Claim:** The "Steph" vs. "Maya" identity split is structural, not incidental. Legal/administrative contexts use "Steph Bairey" (8 addresses), while personal/creative contexts use "Maya Bairey" (4 addresses). The business entity "Lingua Ink" has its own identity distinct from either personal name.
- **Source:** `sources/operator-notes/email-send-as-config.md` (all 16 addresses and display names)
- **Confidence:** CONFIRMED (address-to-display-name mapping); LIKELY (the structural interpretation of the split)
- **Impact:** SL automation must preserve identity routing -- sending from the wrong identity in the wrong context would be a significant error
- **Last verified:** 2026-02-27

- **Claim:** The audit report (prior work) described a "4-address model" which significantly understates the actual complexity: there are 16 send-as identities across 6 domains, with 3+ distinct mail servers.
- **Source:** `sources/operator-notes/email-send-as-config.md` (observation note)
- **Confidence:** CONFIRMED
- **Impact:** Any SL email automation design based on the audit report's model would be inadequate
- **Last verified:** 2026-02-27

[UNKNOWN: Which address does Maya use when sending client emails day-to-day? The handoff mentions "Client email at steph@linguaink.com" but the send-as config shows info@linguaink.com, maya@linguaink.com, and steph@linguaink.com all exist. The selection rules for which Lingua Ink address to use in which client context are not documented.]

[UNKNOWN: Signature content per identity. None of the sources document what signatures are configured for each send-as address. This matters for automation that generates or sends emails.]

---

## 4. Mail Servers and Infrastructure

### Distinct Mail Servers

- **Claim:** Eight distinct mail server endpoints are used across the 16 send-as identities:
  1. **Gmail native** -- stephbairey@gmail.com, grannynewsletter@gmail.com, mjbairey@gmail.com, pdxraginggrannies@gmail.com, scb.zombie@gmail.com, webgranny@gmail.com
  2. **mail.bairey.com** (SSL 465) -- maya@bairey.com, steph@bairey.com, webgranny@bairey.com
  3. **mail.tomahawkdestiny.com** (SSL 465) -- arc@tomahawkdestiny.com, steph.bairey.arc@tomahawkdestiny.com
  4. **dfw-s07.nixihost.com** (SSL 465) -- info@linguaink.com, steph@linguaink.com
  5. **mail.linguaink.com** (SSL 465) -- maya@linguaink.com
  6. **mail.linguainkmedia.com** (SSL 465) -- steph@linguainkmedia.com
  7. **mail.lynnahaller.com** (SSL 465) -- doorknobs@lynnahaller.com
  8. **iah-s01.nixihost.com** (TLS 587) -- webmaster@tomahawkdestiny.com
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Mail infrastructure; monitoring/alerting for server health; credential management across multiple SMTP servers
- **Last verified:** 2026-02-27

- **Claim:** Two Nixihost servers are in use: dfw-s07 (Dallas, SSL 465) and iah-s01 (Houston, TLS 587). The webmaster@tomahawkdestiny.com address is the only one using TLS 587 instead of SSL 465.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** Infrastructure -- different security protocols may require different handling
- **Last verified:** 2026-02-27

### Domains Involved

- **Claim:** Six domains are used for email: gmail.com, bairey.com, linguaink.com, linguainkmedia.com, tomahawkdestiny.com, lynnahaller.com.
- **Source:** `sources/operator-notes/email-send-as-config.md`
- **Confidence:** CONFIRMED
- **Impact:** DNS and domain management; renewal tracking; SPF/DKIM configuration
- **Last verified:** 2026-02-27

[UNKNOWN: SPF, DKIM, and DMARC records for non-Gmail domains. For send-as to work reliably without being flagged as spam, these DNS records need to be properly configured. Current configuration status is undocumented.]

---

## 5. Gmail Filters: Complete Inventory

Extracted from `sources/system-snapshots/GmailFilters.xml`. The export contains 48 filter entries total. The filters are organized below by functional category.

### 5a. Smart Label Overrides

**Filter 1: Catch-all personal label**
- **Criteria:** From: `(*)`
- **Action:** Apply smart label: `^smartlabel_personal`
- **Claim:** A catch-all filter applies the Gmail smart label "Personal" to all incoming email matching `(*)`. This likely overrides Gmail's automatic categorization to ensure all email is treated as personal.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED (filter exists); LIKELY (interpretation of purpose)
- **Impact:** Email categorization -- Gmail tabs/categories may be overridden by this filter
- **Last verified:** 2026-02-28 (XML export timestamp)

### 5b. People Filters (Individual Contact Labels)

These filters label emails from or to specific individuals. Most have paired from/to filters (label incoming AND outgoing messages to that person).

**Filter 2: Nicole (FROM)**
- **Criteria:** From: `nicole@daltonlawoffice.net OR shellie@daltonlawoffice.net OR coral@daltonlawoffice.net OR ndaltonlaw@gmail.com`
- **Action:** Label: `Nicole`

**Filter 33: Nicole (TO)**
- **Criteria:** To: `nicole@daltonlawoffice.net OR shellie@daltonlawoffice.net OR coral@daltonlawoffice.net OR ndaltonlaw@gmail.com`
- **Action:** Label: `Nicole`

- **Claim:** Emails from or to Nicole Dalton (4 addresses across daltonlawoffice.net and ndaltonlaw@gmail.com) are labeled "Nicole." Nicole appears to be a lawyer (law office domain). Both incoming and outgoing messages are labeled.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Contact management; label-based email organization
- **Last verified:** 2026-02-28

**Filter 3: Daniela (FROM)**
- **Criteria:** From: `danielamorescalchi@gmail.com`
- **Action:** Label: `Daniela`

**Filter 34: Daniela (TO)**
- **Criteria:** To: `danielamorescalchi@gmail.com`
- **Action:** Label: `Daniela`

- **Claim:** Emails from or to Daniela Morescalchi are labeled "Daniela."
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Contact management
- **Last verified:** 2026-02-28

**Filter 4: Lynn (FROM)**
- **Criteria:** From: `lynnahaller@gmail.com OR *@lynnahaller.com`
- **Action:** Label: `Lynn`

**Filter 35: Lynn (TO)**
- **Criteria:** To: `lynnahaller@gmail.com`
- **Action:** Label: `Lynn`

- **Claim:** Emails from Lynn Haller (personal gmail AND any address at lynnahaller.com domain) are labeled "Lynn." Outgoing filter only matches the gmail address.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Client email tracking (Lynn Haller is an active client per daily processes handoff)
- **Last verified:** 2026-02-28
- [DISCREPANCY: The FROM filter catches `*@lynnahaller.com` but the TO filter only catches `lynnahaller@gmail.com`. Outgoing messages sent to addresses at lynnahaller.com would not be labeled "Lynn" unless caught by another filter.]

**Filter 5: Carolyn (FROM)**
- **Criteria:** From: `portlandpoet@gmail.com`
- **Action:** Label: `Carolyn`

**Filter 36: Carolyn (TO)**
- **Criteria:** To: `portlandpoet@gmail.com`
- **Action:** Label: `Carolyn`

- **Claim:** Emails from or to portlandpoet@gmail.com are labeled "Carolyn." This is Carolyn Martin, a poet and Lingua Ink author (referenced in the "New order" filter).
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Client/author email tracking
- **Last verified:** 2026-02-28

**Filter 6: Sulima (FROM)**
- **Criteria:** From: `sulimama@gmail.com OR sulima@sulimamalzin.net`
- **Action:** Label: `Sulima`

**Filter 37: Sulima (TO)**
- **Criteria:** To: `sulimama@gmail.com OR sulima@sulimamalzin.net`
- **Action:** Label: `Sulima`

- **Claim:** Emails from or to Sulima Malzin (2 addresses) are labeled "Sulima." Sulima is described in handoffs as Maya's most important client and someone she loves. She is 86 years old.
- **Source:** `sources/system-snapshots/GmailFilters.xml`; `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** High-priority client email tracking
- **Last verified:** 2026-02-28

**Filter 46: Devon (FROM)**
- **Criteria:** From: `devonervin2010@gmail.com`
- **Action:** Label: `Devon`

- **Claim:** Emails from Devon Ervin are labeled "Devon." Devon is an active client (website build with seminar event management). No corresponding TO filter exists for Devon.
- **Source:** `sources/system-snapshots/GmailFilters.xml`; `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** Client email tracking
- **Last verified:** 2026-02-28

### 5c. Group/Role Filters

**Filter 7: Lingua Ink (TO)**
- **Criteria:** To: `*@linguaink.com`
- **Action:** Label: `Lingua Ink`

- **Claim:** Any email sent TO any address at linguaink.com is labeled "Lingua Ink." This captures all inbound business email regardless of which specific linguaink.com address was used.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Business email routing; confirms linguaink.com addresses forward to Gmail
- **Last verified:** 2026-02-28

**Filter 8: Authors (FROM)**
- **Criteria:** From: `sulimama@gmail.com OR sulima@sulimamalzin.net OR portlandpoet@gmail.com OR danielamorescalchi@gmail.com OR lynnahaller@gmail.com OR nd@drwendyleighwhite.com OR suzanne@suzannemanserphd.com OR pnschoof@comcast.net`
- **Action:** Label: `Authors`

**Filter 38: Authors (TO)**
- **Criteria:** To: `sulimama@gmail.com OR sulima@sulimamalzin.net OR portlandpoet@gmail.com OR danielamorescalchi@gmail.com OR lynnahaller@gmail.com OR nd@drwendyleighwhite.com OR suzanne@suzannemanserphd.com`
- **Action:** Label: `Authors`

- **Claim:** The "Authors" label captures emails from/to Maya's author clients. The complete author list is:
  - Sulima Malzin (sulimama@gmail.com, sulima@sulimamalzin.net)
  - Carolyn Martin (portlandpoet@gmail.com)
  - Daniela Morescalchi (danielamorescalchi@gmail.com)
  - Lynn Haller (lynnahaller@gmail.com)
  - Dr. Wendy Leigh White (nd@drwendyleighwhite.com)
  - Suzanne Manser (suzanne@suzannemanserphd.com)
  - Pat Schoof (pnschoof@comcast.net) -- FROM filter only, not in TO filter
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Author/client relationship mapping; business operations
- **Last verified:** 2026-02-28
- [DISCREPANCY: Pat Schoof (pnschoof@comcast.net) appears in the FROM Authors filter but not in the TO Authors filter. This may mean Pat is a newer addition or the TO filter predates Pat's inclusion.]

**Filter 9: Cohort (FROM)**
- **Criteria:** From: `lynnahaller@gmail.com OR jkhamilton11@gmail.com OR Ayamewrites@gmail.com OR bbuckman@outlook.com OR maurad7@msn.com OR krezbywrites@gmail.com OR devonervin2010@gmail.com OR jill@legendarykeynotes.com`
- **Action:** Label: `Cohort`

**Filter 39: Cohort (TO)**
- **Criteria:** To: `lynnahaller@gmail.com OR jkhamilton11@gmail.com OR Ayamewrites@gmail.com OR bbuckman@outlook.com OR maurad7@msn.com OR krezbywrites@gmail.com OR devonervin2010@gmail.com OR jill@legendarykeynotes.com`
- **Action:** Label: `Cohort`

- **Claim:** The "Cohort" label captures a group of 8 contacts. Lynn Haller and Devon Ervin are also in this list (and in Authors/Devon labels respectively), suggesting "Cohort" is a peer/writing group that overlaps with but is distinct from the author-client relationship.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED (filter exists); LIKELY (interpretation as writing peer group)
- **Impact:** Relationship mapping; community communication
- **Last verified:** 2026-02-28
- Cohort members: Lynn Haller, JK Hamilton, Ayame, B Buckman, Maura D, Krezby, Devon Ervin, Jill (Legendary Keynotes)

### 5d. PRG (Portland Raging Grannies) Filters

The PRG filter structure is the most complex in the system, with 13 distinct filters handling incoming email, outgoing email, gaggle.email list traffic, newsletter traffic, administrative noise, and webgranny correspondence.

**Filter 10: PRG Newsletter (FROM)**
- **Criteria:** From: `grannynewsletter@gmail.com`
- **Action:** Label: `PRG/Newsletter`

**Filter 47: PRG Newsletter (TO)**
- **Criteria:** To: `grannynewsletter@gmail.com OR granny-newsletter@gaggle.email`
- **Action:** Label: `PRG/Newsletter`

- **Claim:** The PRG newsletter has a nested label (`PRG/Newsletter`) and is associated with two addresses: grannynewsletter@gmail.com and granny-newsletter@gaggle.email (a Gaggle mailing list address).
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** PRG newsletter automation
- **Last verified:** 2026-02-28

**Filter 11: PRG Gaggle Lists (FROM)**
- **Criteria:** From: `(("prg-members" OR "prg-enviro-team" OR "prg-gender-team" OR "prg-rij-team" OR "prg-social-team" OR "prg-gagh") AND gaggle.email)` excluding `grannynewsletter+admins@gaggle.email` and `notification@gaggle.email`
- **Action:** Label: `PRG`

**Filter 40: PRG Gaggle Lists (TO)**
- **Criteria:** To: same Gaggle list pattern as Filter 11
- **Action:** Label: `PRG`

- **Claim:** PRG uses Gaggle (gaggle.email) as its mailing list platform, with 6 distinct mailing lists:
  1. prg-members (general membership)
  2. prg-enviro-team (environmental team)
  3. prg-gender-team (gender team)
  4. prg-rij-team (racial/injustice team)
  5. prg-social-team (social team)
  6. prg-gagh (purpose unclear -- possibly "Grannies Against Gun Hate" or similar)
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED (lists exist); UNCERTAIN (prg-gagh expansion)
- **Impact:** PRG organizational structure mapping; mailing list management
- **Last verified:** 2026-02-28
- [VERIFY: What does "prg-gagh" stand for?]

**Filter 20: PRG PayPal**
- **Criteria:** From: `noreply@service.paypal.com` AND To: `pdxraginggrannies@gmail.com`
- **Action:** Label: `PRG`, mark as read, archive

- **Claim:** PayPal notifications sent to the PRG organizational email are labeled PRG, automatically read, and archived.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** PRG financial tracking; donation notifications
- **Last verified:** 2026-02-28

**Filter 21: PRG general (TO pdxraginggrannies)**
- **Criteria:** To: `pdxraginggrannies@gmail.com`
- **Action:** Label: `PRG`, archive

- **Claim:** All email sent to the PRG organizational address (pdxraginggrannies@gmail.com) is labeled PRG and archived (removed from inbox). This means PRG organizational email does not appear in the main inbox view.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Inbox management -- PRG mail is accessible via label but does not clutter the inbox
- **Last verified:** 2026-02-28

**Filters 22-25: PRG Individual Members (FROM, split across 4 filters)**

These filters identify email from ~45+ individual PRG members and label them "PRG." They are split across 4 filter entries due to Gmail's character limits on filter criteria. All exclude messages with subjects containing `[prgfyi]`, "E-Vine", "messages awaiting moderation", or "events in the last 24 hours", and exclude admin notifications from Gaggle.

- **Claim:** Maya has individual-level email filtering for approximately 45+ PRG members. Emails from these individuals that are NOT list digests or admin notifications get the "PRG" label. This means Maya can see direct PRG member correspondence in the PRG label while bulk list traffic is handled separately.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (filters 22-25)
- **Confidence:** CONFIRMED
- **Impact:** PRG communication management; member directory
- **Last verified:** 2026-02-28

**Filters 41-44: PRG Individual Members (TO, split across 4 filters)**

Mirror filters of 22-25 but matching on the TO field instead of FROM. Labels outgoing messages to PRG members as "PRG."

- **Claim:** The PRG member filters exist in paired FROM/TO configurations, ensuring both incoming and outgoing PRG member correspondence is labeled. This pattern is consistent across the entire filter system.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (filters 41-44)
- **Confidence:** CONFIRMED
- **Impact:** Complete email threading for PRG correspondence
- **Last verified:** 2026-02-28

**Filter 26: PRG Bumpf (Admin Noise)**
- **Criteria:** From: `grannynewsletter+admins@gaggle.email OR notification@gaggle.email`
- **Action:** Label: `PRG/PRG Bumpf`, mark as read, archive

**Filter 27: PRG Bumpf (Subject-Based)**
- **Criteria:** Subject contains: `[prgfyi]`, "E-Vine", "messages awaiting moderation", or "events in the last 24 hours"
- **Action:** Label: `PRG/PRG Bumpf`, mark as read, archive

- **Claim:** PRG administrative noise (Gaggle admin notifications, FYI digests, moderation alerts, and daily event summaries) is routed to a nested label "PRG/PRG Bumpf," automatically marked as read, and archived. "Bumpf" is Maya's term for administrative noise that needs to be kept but not actively read.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Inbox noise management; PRG label hierarchy design
- **Last verified:** 2026-02-28

**Filter 48: Webgranny (TO)**
- **Criteria:** To: `webgranny@bairey.com`
- **Action:** Label: `PRG/Webgranny`

- **Claim:** Email sent to webgranny@bairey.com gets the nested label "PRG/Webgranny," indicating the webgranny role is specifically associated with PRG webmaster duties.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** PRG web administration tracking; confirms webgranny@bairey.com receives PRG-related correspondence
- **Last verified:** 2026-02-28

### 5e. TDA/ARC (Tomahawk Destiny Association) Filters

**Filter 12: Tomahawk (FROM)**
- **Criteria:** From: a large list of ~60+ addresses including `*@tomahawkdestiny.com`, `Messenger@associationvoice.com`, `tdamoorage@gmail.com`, organizational role addresses (bookkeeper, president, secretary, treasurer, vicepresident, security, webmaster, arc), and many individual member addresses.
- **Action:** Label: `Tomahawk`

**Filter 42: Tomahawk (TO)**
- **Criteria:** To: same list as Filter 12
- **Action:** Label: `Tomahawk`

- **Claim:** The "Tomahawk" label captures correspondence with TDA members and organizational addresses. The filter includes ~60+ individual email addresses and uses AssociationVoice (Messenger@associationvoice.com) as a communication platform. TDA has organizational role addresses for: bookkeeper, president, secretary, treasurer, vice president, security, webmaster, and ARC.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** TDA organizational communication; role mapping
- **Last verified:** 2026-02-28

**Filter 13: ARC (FROM)**
- **Criteria:** From: `arc@tomahawkdestiny.com OR *.arc@tomahawkdestiny.com OR mike.duncan.pdx@gmail.com OR teresalawwill@gmail.com OR k_delleney@hotmail.com OR slydavids2@yahoo.com`
- **Action:** Label: `ARC`

**Filter 43: ARC (TO)**
- **Criteria:** To: same list as Filter 13
- **Action:** Label: `ARC`

- **Claim:** The "ARC" label is a subset of Tomahawk correspondence, specifically filtering for the ARC committee. The ARC committee members (beyond Maya) include: Mike Duncan, Teresa, K Delleney, and Sly Davids. The wildcard `*.arc@tomahawkdestiny.com` captures all personal ARC addresses (like Maya's own steph.bairey.arc@).
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** ARC committee communication tracking
- **Last verified:** 2026-02-28

### 5f. Commercial/Service Filters

**Filter 14: Amazon**
- **Criteria:** From: `*@amazon.com`
- **Action:** Label: `Amazon`, archive, never spam

- **Claim:** All Amazon email is labeled "Amazon," archived (removed from inbox), and marked never-spam.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** E-commerce tracking; the Amazon delivery tracking n8n workflow references this label (label ID `Label_6582208580953641436` per daily processes handoff)
- **Last verified:** 2026-02-28

**Filter 15: Substack/Sulima Trash**
- **Criteria:** From: `*@substack.com` AND To: `*sulimamalzin.net`
- **Action:** Mark as read, trash

- **Claim:** Substack emails addressed to any sulimamalzin.net address are automatically trashed and marked read. This suggests Substack notifications forwarded from Sulima's domain are unwanted duplicates.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED (filter exists); LIKELY (interpretation as duplicate suppression)
- **Impact:** Sulima client workflow; Substack management
- **Last verified:** 2026-02-28
- [VERIFY: Why are Substack emails to sulimamalzin.net being trashed? Is Maya receiving forwarded copies of Sulima's Substack notifications that she doesn't need?]

**Filter 16: Substack (General)**
- **Criteria:** From: `*@substack.com`
- **Action:** Label: `Substack`, archive

- **Claim:** All remaining Substack email (after the Sulima-specific trash filter) is labeled "Substack" and archived. Substack content is kept but does not appear in the inbox.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Content consumption management
- **Last verified:** 2026-02-28

**Filter 17: Patreon (Most)**
- **Criteria:** From: `*@patreon.com` EXCLUDING messages from "SalvoG" (bingo@patreon.com) and excluding subject "SalvoG replied to your comment"
- **Action:** Mark as read, archive

- **Claim:** Most Patreon notifications are automatically read and archived. The exception is content from "SalvoG" (bingo@patreon.com) and SalvoG comment replies, which are allowed through to the inbox.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Content consumption; SalvoG appears to be a Patreon creator Maya actively follows
- **Last verified:** 2026-02-28

### 5g. Auto-Silence Filters (Noise Suppression)

**Filter 18: Plugin Updates / Google Play Receipts**
- **Criteria:** Subject: "Some plugins were automatically updated" OR "Your Google Play Order Receipt"
- **Action:** Mark as read, archive, never spam, never mark as important

- **Claim:** WordPress plugin auto-update notifications and Google Play receipts are silenced (read, archived, never important, never spam).
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** WordPress maintenance awareness; noise suppression
- **Last verified:** 2026-02-28

**Filter 28: Failed Plugin Updates**
- **Criteria:** Subject: "Some plugins have failed to update"
- **Action:** Trash

- **Claim:** Failed WordPress plugin update notifications are trashed entirely.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** WordPress maintenance -- failed updates are not being tracked. This is a potential operational blind spot.
- **Last verified:** 2026-02-28
- [VERIFY: Is trashing failed plugin update notifications intentional? These may indicate sites that need manual attention.]

### 5h. Business/Order Filters

**Filter 19: Lingua Ink / Author New Orders**
- **Criteria:** Has the words: "Carolyn Martin Poet New order" OR "Lingua Ink Books New order" OR "Sulima MalzinNew order"
- **Action:** Label: `Lingua Ink`, star

- **Claim:** New WooCommerce orders from author storefronts (Carolyn Martin Poet, Lingua Ink Books, Sulima Malzin) are labeled "Lingua Ink" and starred for attention. These appear to be WooCommerce "New order" email notifications.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** E-commerce order tracking; revenue monitoring; book sales
- **Last verified:** 2026-02-28
- [DISCREPANCY: "Sulima MalzinNew order" appears to be missing a space before "New." This is likely how the WooCommerce notification actually reads, not a filter error.]

### 5i. Jobs Filter

**Filter 29: Jobs (Dani Napier Harrison)**
- **Criteria:** Has the words: "Dani Napier Harrison" OR "dani@consultdnh.com"
- **Action:** Label: `Jobs`, mark as read, archive

- **Claim:** Emails mentioning Dani Napier Harrison or from dani@consultdnh.com are labeled "Jobs," marked as read, and archived. This suggests a recruiter or job search contact whose messages are tracked but not actively reviewed.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED
- **Impact:** Job search tracking
- **Last verified:** 2026-02-28

**Filter 30: Jobs (FROM, multiple contacts)**
- **Criteria:** From: various personal gmail addresses plus `*@unity3d.com`
- **Action:** Label: `Jobs`

**Filter 31: Jobs (TO, same contacts)**
- **Criteria:** To: same list as Filter 30
- **Action:** Label: `Jobs`

- **Claim:** The "Jobs" label captures correspondence with ~10 specific contacts and Unity3D. The inclusion of `*@unity3d.com` suggests Maya has had employment-related contact with Unity Technologies.
- **Source:** `sources/system-snapshots/GmailFilters.xml`
- **Confidence:** CONFIRMED (filter exists); LIKELY (interpretation as job search contacts)
- **Impact:** Job search tracking; career context
- **Last verified:** 2026-02-28

---

## 6. Complete Label Hierarchy

Derived from all filters in the Gmail export:

```
Amazon
ARC
Authors
Carolyn
Cohort
Daniela
Devon
Jobs
Lingua Ink
Lynn
Nicole
PRG/
  PRG (top level)
  PRG/Newsletter
  PRG/PRG Bumpf
  PRG/Webgranny
Substack
Sulima
Tomahawk
```

- **Claim:** The Gmail label structure uses flat labels for most categories, with nested labels only for PRG (4 sub-labels). The PRG nesting reflects the complexity of Maya's PRG involvement: general PRG correspondence, newsletter-specific, admin noise ("bumpf"), and webmaster duties.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (all label references)
- **Confidence:** CONFIRMED
- **Impact:** Label design for SL email automation; inbox organization
- **Last verified:** 2026-02-28

[UNKNOWN: The Gmail export only contains filter-created labels. There may be additional manually-created labels in Gmail that have no associated filters. A full label export would be needed to confirm the complete label set.]

---

## 7. Filter Design Patterns

### Paired FROM/TO Filters

- **Claim:** The dominant filter design pattern is paired FROM/TO filters that label both incoming and outgoing correspondence with the same label. This appears for: Nicole, Daniela, Lynn, Carolyn, Sulima, Authors, Cohort, PRG members (4 filter pairs), PRG Gaggle lists, Tomahawk, ARC, and Jobs contacts.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (systematic observation)
- **Confidence:** CONFIRMED
- **Impact:** Any email automation must understand that labels represent conversations/relationships, not just incoming mail
- **Last verified:** 2026-02-28

### Multi-Label Application

- **Claim:** Individual emails can receive multiple labels simultaneously. For example, an email from sulimama@gmail.com would receive both "Sulima" (individual filter) and "Authors" (group filter). An email from devonervin2010@gmail.com would receive both "Devon" and "Cohort."
- **Source:** `sources/system-snapshots/GmailFilters.xml` (overlapping filter criteria)
- **Confidence:** CONFIRMED
- **Impact:** Label semantics -- labels are not mutually exclusive; they represent multiple facets of a relationship
- **Last verified:** 2026-02-28

### Archive-by-Default for Low-Priority Streams

- **Claim:** Several categories are archived by default (removed from inbox): Amazon, Substack, most Patreon, PRG organizational email (to pdxraginggrannies@gmail.com), PRG bumpf, PRG PayPal notifications, WordPress plugin updates, Jobs (Dani Napier Harrison). The inbox is curated to show only email that requires active attention.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (shouldArchive = true)
- **Confidence:** CONFIRMED
- **Impact:** Inbox zero strategy; automation should respect which streams Maya wants to see vs. track silently
- **Last verified:** 2026-02-28

### Noise Hierarchy: Archive vs. Trash

- **Claim:** Maya distinguishes between "keep but don't show" (archive) and "discard" (trash). Archived items: Amazon orders, Substack, most Patreon, PRG bumpf, plugin auto-updates. Trashed items: Substack-to-Sulima duplicates, failed plugin update notifications.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (shouldArchive vs. shouldTrash)
- **Confidence:** CONFIRMED
- **Impact:** Data retention policy; understanding what Maya considers disposable vs. archival
- **Last verified:** 2026-02-28

---

## 8. Forwarding Rules

- **Claim:** No forwarding rules are present in the Gmail filter export. The XML does not contain any `forwardTo` properties.
- **Source:** `sources/system-snapshots/GmailFilters.xml` (absence of forwardTo in all entries)
- **Confidence:** CONFIRMED (for filter-based forwarding)
- **Impact:** Email routing
- **Last verified:** 2026-02-28

[UNKNOWN: Gmail also supports account-level forwarding (Settings > Forwarding) which would not appear in the filter export. There may be forwarding rules configured at the account level that are not captured here.]

[UNKNOWN: Several non-Gmail addresses (linguaink.com, bairey.com, tomahawkdestiny.com, lynnahaller.com) appear in filter TO: criteria and in the send-as config. These domain mailboxes likely forward TO stephbairey@gmail.com (otherwise the filters matching on TO: would not fire). The forwarding configuration on those mail servers is not documented in any source.]

---

## 9. Gmail as Operational Hub

- **Claim:** Maya's Gmail is described as her "operational nervous system" -- she searches it constantly to reconstruct history, locate commitments, and find prior explanations she has already given clients. It serves as a de facto CRM, project history, and institutional memory system.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** Email search and retrieval is a core automation target; any SL system must preserve or improve on this capability
- **Last verified:** 2026-02-27

- **Claim:** Maya's email system uses the Amazon label (Gmail label ID `Label_6582208580953641436`) as a trigger source for n8n delivery tracking automation.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** n8n integration; Gmail API label access
- **Last verified:** 2026-02-27

- **Claim:** Maya manages a ~600-subscriber email list via MailPoet (WordPress plugin), separate from the Gmail filter system.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** CONFIRMED
- **Impact:** Email marketing automation; distinct from transactional/personal email
- **Last verified:** 2026-02-27

---

## 10. Gaps and Open Questions Summary

### Gaps ([UNKNOWN])

1. **Signatures per identity:** No source documents what email signatures are configured for each of the 16 send-as addresses. This matters for any automation that drafts or sends email.

2. **Client email address selection rules:** Which Lingua Ink address (info@, maya@, steph@) is used in which client context? The rules for this choice are not documented.

3. **Domain forwarding configuration:** How do non-Gmail domain mailboxes (linguaink.com, bairey.com, tomahawkdestiny.com, lynnahaller.com) route inbound mail to stephbairey@gmail.com? The mail server forwarding configuration is not in any source.

4. **Account-level forwarding:** Gmail account-level forwarding settings are not captured in the filter XML export.

5. **Complete label set:** The filter export only reveals labels created by filters. Manually-created labels without associated filters are not captured.

6. **SPF/DKIM/DMARC records:** DNS email authentication records for non-Gmail domains are not documented. These affect deliverability when sending as those identities.

7. **Reply behavior per identity:** When Maya replies to email received at a particular address, does Gmail automatically select the correct send-as identity? Or does she manually choose?

### Verification Questions ([VERIFY])

1. What is webgranny@gmail.com actually used for? It parallels webgranny@bairey.com but the use case is unclear.

2. What makes maya@bairey.com "not an alias" -- does it have its own mailbox? Does mail sent TO this address arrive separately?

3. What is the relationship between linguaink.com and linguainkmedia.com? Same entity, two domains? Different purposes?

4. Why are Substack emails to sulimamalzin.net being trashed? Duplicate suppression?

5. Is trashing failed plugin update notifications intentional? These may indicate sites needing manual attention.

6. What does "prg-gagh" stand for in the Gaggle mailing list names?

### Discrepancies ([DISCREPANCY])

1. The Lynn FROM filter catches `*@lynnahaller.com` but the TO filter only catches `lynnahaller@gmail.com`.

2. maya@linguaink.com routes through mail.linguaink.com while info@ and steph@linguaink.com route through dfw-s07.nixihost.com.

3. Pat Schoof (pnschoof@comcast.net) appears in the FROM Authors filter but not the TO Authors filter.

4. "Sulima MalzinNew order" in the WooCommerce filter appears to have a missing space before "New." This is likely how the WooCommerce notification actually reads, not a filter error.
