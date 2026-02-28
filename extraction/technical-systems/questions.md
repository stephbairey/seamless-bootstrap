# Phase 1 Questions for Maya

Consolidated from all extraction files. Grouped by topic, not by source. Each item includes enough context for Maya to answer without re-reading the extraction files.

---

## ClickUp

1. **What are the ClickUp statuses and their transitions?** The clickup-fields.json export only contained custom field definitions, not status workflow. What statuses exist in the Master Task List (e.g., Open, In Progress, Done, Closed)? Are there different statuses for different lists?
A: Same status, as there is only one list (Master Task List). Statuses are Not Started, On Hold, Waiting, Begun, Scratch, Complete.

2. **What are the workspace/space/list IDs?** The export didn't include structural IDs (workspace, space, list). SL automation will need: Workspace ID, Space ID, and the List ID for "Master Task List." Can you share these from ClickUp settings? 
A: Workspace ID: 90132317650 - Space ID: 90139879792 (Task Dashboard) - List ID: 901318968458 (Master Task List)

3. **Is Daniela Morescalchi a current client?** She appears in the ClickUp Project dropdown but isn't mentioned in any handoff as an active relationship.
A. Yes, she is an author whose books I will be publishing. They are being edited right now. Client lists may be incomplete to start but we will fill them out as we go.

4. **What distinguishes "Free Cohort" from "Lingua Ink Cohorts"?** Both are ClickUp Project options. What's the operational difference?
A. I intended to begin charging people for cohorts I would lead. I have not done that yet. The cohort I lead now (since Sept 2024) is free. I created the project options to distinguish time spent on each.

5. **What's the distinction between "Indirect" and "Passive" revenue?** Revenue field has: None, Indirect, Passive, Direct Low, Direct High. Can you give an example of Indirect vs. Passive? 
A. Passive usually means book royalties. The work has been done, for the most part, and money accrues without much work from me. Indirect would mean a task with income potential, like marketing or meeting a new client.

6. **Are there naming conventions beyond "lowercase verb first"?** The handoff confirms task names start with a lowercase verb and due dates are mandatory. Any other rules about task naming, description format, or checklist usage? I prefer short actionable task names. If I do fill out description, it often contains notes I want to remember about the exact task or meeting, like a zoom link or address or actual notes from the meeting after it's held. Checklists are too granular for me at this point so I don't use them, though you may have seen a few aspirartional attempts.

7. **Is ClickUp a daily work driver or primarily for capture?** One handoff describes usage as "inconsistent" [INFERRED], another calls it "meticulous." Which is closer to reality? Do you work from ClickUp daily or use it more for periodic capture and review? I use it almost daily, though sometimes let a few days go by before marking items completed. That's the only inconsistent thing about my ClickUp use. 

---

## Email

8. **Which of the 16 Send-As identities are actively used?** The extraction found 16 addresses configured. Some may be legacy. Which ones do you actually send from regularly?
A: All are in active use or serve a standing purpose except two legacy addresses: webgranny@bairey.com (predates inbox access to webgranny@gmail.com) and scb.zombie@gmail.com (should be retired but is tied to too many signups). The remaining addresses are used regularly or on-demand for their designated roles.

9. **What are the routing rules for identity selection?** When composing email, how do you decide whether to send as Steph Bairey, Maya Bairey, Lingua Ink, PRG, or ARC/TDA? Is it based on recipient, topic, or context?
A: Identity selection is role-based, determined by two axes: name (Steph = business/operations, Maya = creative/author) and domain (which org context). The reply-from is automatic — Gmail sends from whichever address received the inbound message (all forward to stephbairey@gmail.com so there's one inbox of truth). For new compositions, the decision is "what hat am I wearing?" Some contacts know me as Maya first and stay on Maya addresses even for business work, so relationship history can override the strict role logic. The core routing:

maya@bairey.com — author identity
maya@linguaink.com — creative director / Lingua Ink editorial & design work
steph@linguaink.com — business/coder Lingua Ink Books
steph@linguainkmedia.com — business/coder Lingua Ink Media
steph@bairey.com — personal/formal/government-name contexts
stephbairey@gmail.com — default; personal/community; receives all forwards
mjbairey@gmail.com — Maya's Gmail (for Google-login-required contexts)
webmaster@tomahawkdestiny.com — TDA website role
steph.bairey.arc@tomahawkdestiny.com — personal ARC committee correspondence
arc@tomahawkdestiny.com — generic ARC distribution list
pdxraginggrannies@gmail.com — PRG official/external
grannynewsletter@gmail.com — PRG newsletter submissions & sends
webgranny@gmail.com — IRG work
doorknobs@lynnahaller.com — shared distribution list for Lynn/HoD book correspondence
info@linguaink.com — front-facing generic Lingua Ink contact

10. **Are signatures different per identity?** Gmail allows per-identity signatures. Are there distinct signatures for Steph vs. Maya vs. Lingua Ink vs. PRG?
A: yes, all have distinct signatures.

11. **Does domain-level email forwarding exist?** The filters show no filter-based forwarding, but do addresses like info@linguaink.com or maya@bairey.com auto-forward to stephbairey@gmail.com at the domain/hosting level?
A: yes, all forward to stephbairey@gmail.com

12. **Is there a complete label hierarchy?** The Gmail filters export shows 17 labels. Is this the full set, or are there additional labels not referenced by filters? 
A: All labels: Amazon, ARC, Articles, Business, Business/SEO, Business/Tools, Authors, Authors/Carolyn, Authors/Cohort, Authors/Daniela, Authors/Devon, Jobs, KEEPERS, Lingua Ink, Lynn, My Travel, Nicole, PRG, PRG/Newsletter, PRG/PRG Bumpf, PRG/PRG To Do, PRG/Webgranny, Snoozed, Substack, Sulima, Taxes, Tomahawk

13. **What is the purpose of the `webgranny@gmail.com` address?** It shows display name "Steph Bairey" — is this a personal identity for Raging Grannies work, or organizational?
A: it is a personal address for tech work I do for the International Raging Grannies

---

## Calendar

14. **Are all three calendars visible simultaneously?** Do you see linguainkmedia, mjbairey, and stephbairey calendars in a single Google Calendar view, or do you toggle between them?
A: Again, this operates on my axis. Example: if someone knows me as Maya, I send calendar invites from the mjbairey calendar. But yes, I view them all on the linguainkmedia@gmail.com calendar (another email I use for signups but don't send from).

15. **Is ClickUp-to-Calendar sync native or via n8n?** The ✅-prefixed events suggest ClickUp's built-in Google Calendar integration. Can you confirm?
A: that was ClickUp's native sync to calendar but it didn't work well so I abandoned it.

16. **What does "HoD" stand for?** It appears as "HoD meeting", "HoD Storyboarding", and "HoD meeting with Illustrator and Steph @ Lingua Ink." Is this a client project?
A: This is sforthand for Lynn's book, **The Hallway of Doorknobs**

17. **Is the stephbairey calendar still used for new events?** It's the largest calendar (going back to 2000) but also seems mostly historical. Do you still add new events to it, or has operational activity moved to linguainkmedia?
A: yes, it is very actively used, mostly for home things. Peter has access to it and adds his own events to it through Alexa, and it displays on my local dashboard.

18. **What generates the "Delivery:" events on stephbairey?** These look auto-generated from Amazon notifications (e.g., "Delivery: Cat flap"). Is this a Gmail/Calendar integration, an n8n workflow, or something else?
A: those are legacy, yes. I have a new way of tracking expected deliveries and don't put them on the calendar any more.

19. **Is the Writing Cohort on all three calendars intentional?** It appears on linguainkmedia, mjbairey, and stephbairey. Deliberate redundancy for visibility, or accidental duplication?
A: they should probably just be on mjbairey, but over time snuck onto other calendars via email confusion from other people.

20. **Is there a fourth calendar?** Are there shared calendars (e.g., Pete/family) or additional calendars not exported?
A: There are more but they are not relevant here. For instance, the scb.zombie@gmail.com calendar has family birthdays, recurring annually. They are not part of my regular processes.
---

## File Management

21. **Are Lynn, Maya, and Sulima the only clients with file routing?** The n8n workflows only cover these three. Do other clients (Devon, Nicole, Pat, etc.) have their own routing, or do their files go elsewhere?
A: They are the only three automations I have set up. I want/need to do them for all clients but the matrices are a barrier to starting that. I am very open to a new automated file routing system. All clients do have their own folders in Google Drive, some more organized than others.

22. **Is the Unsorted folder actively monitored?** The handoff describes it as a "catch basin" for unmatched tag pairs. Do you actually check it and update the matrix, or does it accumulate?
A: I do but it's not viewed often as most files sort well.

23. **What triggers a matrix update?** When you notice a gap (file in Unsorted), do you update the Excel matrix and then re-encode into n8n? How often does this happen?
A: I would do so, if I had time. It happens very rarely.

24. **Can you share the Google Drive ID Matrix spreadsheet content?** The .xlsx file couldn't be fully parsed as binary. If possible, export as CSV or share the folder hierarchy manually. This would complete the folder-to-ID mapping.
A: uploaded next to the xlsx as google_drive_id_matrix.json

25. **What happens with files that have 3 tags?** The routing uses tag-pair lookup (2 tags → canonical key). If a file has 3 tags, does the system handle it? Or is 2 tags the maximum?
A: 2 tags due to matrix size. It's sufficient.

26. **Is "Painting-Celia" and "Untitled-Kelsey" naming active?** These are project tags in Maya's routing matrix. Are these current projects or completed?
A: Yes. **Painting Celia** is my published book. **Untitled Kelsey** is another novel, still being written.

27. **What is the SHARED/Master folder?** Several routing entries point to what appears to be a shared or master folder for certain tag combinations. What is this?
A: I'm surprised anything points to a SHARED folder. Those are Google drive folders I share with clients for file sharing. I would rarely put files in there non-manually.

---

## Hosting & Domains

28. **Is Nixihost your hosting provider?** SMTP servers reference Nixihost. Can you confirm this is the hosting provider for linguainkmedia.com, linguaink.com, and bairey.com?
A: yes

29. **Is linguainkmedia.com live?** The handoff from January said it was "nearly complete" and "scheduled to go live after a Sunday final review." Did it go live?
A: yes, it is live

30. **Does linguainkmedia.com have GA4 tracking?** GA4 properties are confirmed for bairey.com, linguaink.com, sulimamalzin.net, and lynnahaller.com — but not linguainkmedia.com.
A: I do not remember. Probably not.

31. **Do you host client sites on your own hosting account?** Or do clients (Devon, Lynn, Sulima, Nicole) have their own hosting that you manage?
A: I host them on my own account, though this will haave to change if I keep adding clients.

32. **Why two WordPress accounts on linguaink.com?** You have both "maya" (maya@bairey.com) and "Maya Editor" (mjbairey@gmail.com). Is this intentional for different contexts, or a legacy artifact?
A: Lingua Ink posts (editor/publishing focused) are authored by 'Maya Editor'. Then, when I make a blog post on bairey.com (author focused), it automatically duplicates to linguaink.com under the name 'maya'. 

---

## Tool Integrations

33. **What Docker containers do you run besides n8n?** The "-arr stack" is mentioned but not detailed. What's the full list of self-hosted services?
A: bazarr, calibre-web, gluetun, hbbr, hbbs, jellyfin, lidarr, navidrome, nextcloud-app, nextcloud-db, nginx-proxy-manager, portainer, prowlarr, qbittorrent, radarr, sabnzbd, sonarr

34. **Is Granola used for all meetings or specific ones?** You mentioned using it with Pete and for Sulima salon discussions. Is it standard for all Zoom calls?
A: yes, I use it whenever I can.

35. **Is the "Writing with Maya" HeyGen channel active?** Is it publishing content, or still in planning/early stages?
A: still in planning stages.

36. **Which social platforms do you post to via Later?** Instagram, Facebook, LinkedIn, others?
A: facebook and instagram, though I could post to more from there. I have not been using it, as I have not been posting much. I have other channels that automatically update when I post a blog from bairey.com (pinterest, lnk,bio) and I post manually to facebook, instagram, and substack when I make a blog post. A list of all author socials: Bluesky - @mayabairey.bsky.social • Facebook - Maya Bairey, Author • Instagram - mayabairey • TikTok - @mayabairey  • Pinterest - mayabairey • Mastodon - mayabairey • Medium - Maya Bairey • Substack - Maya Bairey. Lingua Ink Books has a facebook, instagram, and linkedin. Steph Bairey has a linkedin.

37. **How is the MailPoet subscriber list structured?** Is the ~600 subscribers for Lingua Ink Books specifically? Are there separate lists for different audiences?
A: the subscribers are all for Maya Bairey, author. They have been gathered over time via marketing and subscriptions. I do not segment yet.

38. **Do you use Substack for anything beyond Sulima's Light Waves?** Or is it a single-client tool?
A: I post my own bairey.com blogs there.

---

## Priority Items

These three items are flagged as **minimum required review** in the project plan:

**A. ClickUp custom field option IDs** — All 42 option IDs have been extracted. Do these look current? Any fields or options added since the export?

**B. Email identity routing rules** — 16 Send-As identities documented. Which are active, and what determines which identity you send from?

**C. File routing matrix completeness** — Three client matrices (Lynn, Maya, Sulima) extracted. Are these the only three? Is the matrix current?
all three answered in terminal.