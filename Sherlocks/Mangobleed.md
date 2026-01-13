# HTB Sherlock: MangoBleed (DFIR) — Case Notes (Non-Spoiler)

> **Type:** Blue-team / DFIR investigation challenge (Sherlock)  
> **Focus:** Finding the *true* moment of interactive access using the right artifact  
> **Goal (my view):** Prove “when access became hands-on” and document it clearly.

---

## What this case is about (high level)
This Sherlock pushed me to be precise about **where evidence lives**.

In investigations, it’s easy to chase the wrong file because the scenario *sounds* like it should be there.  
This case reminded me: **the best evidence is often in the most boring place** — authentication logs.

---

## Evidence / Artifacts I worked with
- Linux authentication logs (ex: `auth.log`)
- Other provided files relevant to the scenario (ex: database-related artifacts)
- Challenge hints (used as a learning nudge, not a shortcut)

*(No flags, answers, or raw logs are shared here.)*

---

## My investigation workflow (SOC-style)
1) Identify what “success” means for this question  
   - Not “a service shows activity,” but “attacker gained interactive access.”

2) Collect candidate timestamps from likely artifacts  
   - (I initially looked in the wrong place.)

3) Validate the access moment using authentication evidence  
   - Confirm successful login and align it with the time window.

4) Build a short timeline and summarize as a ticket/report

---

## The real struggle I had (and what it taught me)
I struggled to find the **exact time when the attacker gained interactive hands-on remote access**.

### What I did wrong at first
I kept searching for the “access time” inside a **MongoDB-related file**, assuming the service data would reveal the moment of access.

That led to confusion because:
- service/database artifacts can show activity
- but they don’t always clearly prove *interactive remote access*

### The turning point
After checking a hint, I realized the correct approach:
- The definitive timestamp for interactive access was in **`auth.log`**, not in the MongoDB file.

### What I learned (the important part)
When the question is “When did the attacker log in and get hands-on access?”  
**Authentication logs are the source of truth**.

Database/service files can support the story, but they’re not always the primary proof.

---

## High-level timeline (non-spoiler)
- T0: Suspicious access-related activity is detected (initial indicators)
- T1: Authentication evidence shows successful access
- T2: Interactive remote access is confirmed using the correct log source
- T3: Follow-on activity reviewed for scope/impact
- T4: Final assessment + response recommendations

---

## Key takeaways (SOC L1 friendly)
- Always match the **question** to the **best evidence source**:
  - “login/access time” → auth logs first
  - “what did they do in the app/db” → service/db artifacts second
- If you feel stuck, your first fix is often: **wrong artifact, not low skill**.
- Hints are useful when they teach you *where to look*, not just the answer.

---

## Detection ideas (how I’d catch similar behavior)
- Alert on successful logins after abnormal failures (burst → success)
- Alert on new/rare source IPs for remote access
- Correlate remote login with unusual service/database activity right after
- Add severity when access occurs outside baseline hours or from unusual geo/ASN (if available)
- Hunt for repeat patterns on other hosts/accounts

---

## Mini SOC Ticket (sample structure)
**Title:** Suspected interactive remote access leading to service activity  
**Time window:** [redacted]  
**Host/User:** [redacted]  

**Evidence:**
- Authentication logs confirm successful remote access time
- Supporting artifacts suggest follow-on activity after access
- Timeline built to correlate access → actions → impact

**Assessment:** Suspicious → Escalate  
**Next steps:**
- Reset credentials / review remote access controls
- Review additional hosts for same access source/pattern
- Confirm persistence or lateral movement indicators
