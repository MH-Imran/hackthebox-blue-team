# HTB Sherlock: Brutus (DFIR) — Case Notes (Non-Spoiler)

> **Type:** Blue-team / DFIR investigation challenge (Sherlock)  
> **Focus:** Authentication evidence + session validation + timeline building  
> **Goal (my view):** Reconstruct what happened, prove it with artifacts, and summarize it like a SOC handoff.

---

## What this case is about (high level)
This Sherlock felt like a classic **“access attempt → successful authentication → session activity”** investigation.  
The main work is correlating **authentication events** with **actual interactive sessions** so you can confidently say *when access truly happened*.

---

## Evidence / Artifacts I worked with
- Linux authentication logs (ex: `auth.log`)
- Session history artifacts (ex: `wtmp` / login records)
- Supporting context from the challenge prompts/hints

*(No flags, answers, or raw logs are shared here.)*

---

## My investigation workflow (SOC-style)
1) **Define the question clearly**
   - “When did access happen?” and “Was it interactive or just authentication events?”

2) **Start with authentication evidence**
   - Find the pattern of access attempts and confirm successful authentication.

3) **Validate with session evidence**
   - Confirm the moment it becomes a **real session** (interactive login evidence), not just an auth timestamp.

4) **Build a timeline**
   - Convert key events into a short sequence: time → event → why it matters.

5) **Write a short incident-style summary**
   - Evidence bullets + assessment + next steps.

---

## The real struggle I had (and what it taught me)
I got stuck trying to find the **manual/interactive login time** of the attacker.

### What confused me
I kept mixing up:
- **Authentication time** (a success event in auth logs)
vs
- **Manual/interactive session time** (a real login session record)

At first, I treated “authentication success” as “manual login happened.”  
But that can be misleading — because an authentication success doesn’t always equal a confirmed interactive session.

### How I corrected my thinking
I forced myself to separate the questions:

- **Question A:** “When did authentication succeed?”  
  → answer from auth logs  
- **Question B:** “When did an interactive session start?”  
  → confirm with session artifacts (ex: `wtmp` / login records)

That separation instantly made my timeline cleaner and more defensible.

---

## High-level timeline (non-spoiler)
- T0: Suspicious authentication activity begins (pattern suggests automated attempts)
- T1: Successful authentication is observed
- T2: Interactive session is confirmed via session artifacts
- T3: Post-access activity is reviewed and summarized
- T4: Final assessment + recommended response actions

---

## Key takeaways (SOC L1 friendly)
- Don’t treat “auth success” as “hands-on access” until a session artifact confirms it.
- Always **correlate**: auth events + session records + time window.
- A clean investigation is basically: **evidence → validation → timeline → report**.

---

## Detection ideas (how I’d catch this in a SOC)
- Alert on **failed-login bursts** followed by a success (same account or same source)
- Alert on **first-time source IPs** accessing SSH for a user/host
- Alert on **logins at unusual times** compared to baseline
- Add severity when “auth success” is followed by confirmed **interactive session evidence**
- Hunt across other hosts for the same source / username pattern

---

## Mini SOC Ticket (sample structure)
**Title:** Suspected unauthorized remote access (SSH)  
**Time window:** [redacted]  
**Host/User:** [redacted]  

**Evidence:**
- Authentication anomalies observed (high failure volume)
- Successful authentication event detected
- Interactive session confirmed via session artifacts
- Post-access activity reviewed for impact

**Assessment:** Suspicious → Escalate  
**Next steps:**
- Reset affected credentials / rotate keys
- Block/monitor source infrastructure
- Review other systems for similar access attempts
