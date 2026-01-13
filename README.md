# Hack The Box — Blue Team Notes (SOC / DFIR Practice)

This repository is my **blue-team focused** learning log from Hack The Box.  
I’m building toward a **SOC Analyst (L1)** role, so I document my work like an analyst: **evidence → timeline → conclusion → next steps**.

✅ **Important:** This repo is **non-spoiler**.  
I do **not** share flags, exact answers, or step-by-step solutions. Everything here is written as **case-study notes** and learning reflections.

---

## What you’ll find here

- **DFIR case notes** from HTB Sherlocks (log/PCAP style investigations)
- **SOC-style writeups** (triage mindset, key artifacts, detection ideas)
- **Templates** I use for mini tickets and incident timelines
- **Learning notes** that focus on transferable skills (not walkthroughs)

---

## Repo Structure

```text
hackthebox-blue-team/
├── README.md
├── sherlocks/
│   ├── _template/
│   │   └── README.md
│   ├── brutus/
│   │   └── README.md
│   └── mangobleed/
│       └── README.md
├── notes/
│   ├── frameworks/
│   ├── logs/
│   └── network/
└── templates/
    ├── mini-soc-ticket.md
    └── investigation-timeline.md 
```




---

## How I write a “Blue Team” case study

Each Sherlock/case note follows this format:

- **Summary:** what the incident type was (high-level)
- **Artifacts:** logs/pcaps/files provided
- **Workflow:** how I investigated (steps, pivots)
- **Timeline:** key events (no sensitive exact details)
- **Findings:** what I concluded and why
- **Detection Ideas:** how to catch it in SIEM/EDR
- **Lessons Learned:** what improved my analyst mindset

---

## Mini SOC Ticket Template (My Format)

**Title:**  
**Time Window:**  
**Host/User:**  
**Summary (2–3 lines):**  

**Evidence (bullets):**
-  
-  
-  

**Assessment:** Benign / Suspicious / Escalate  
**Next Steps:**
-  
-  

---

## My Goal (SOC L1)

My focus is to build repeatable analyst skills:
- log analysis and correlation
- timeline building
- identifying key artifacts (network, auth, process behavior)
- writing clear notes and escalation-ready summaries

---

## Notes on Responsible Sharing

- No flags, no answers, no full walkthroughs
- No sensitive data (real IPs, usernames, tokens, etc.)
- Content is written to be safe and professional for public viewing

---

## Profile
GitHub: https://github.com/MH-Imran
