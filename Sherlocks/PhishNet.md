# HTB Sherlock: PhishNet (DFIR) — Case Notes (Non-Spoiler)

> **Type:** Blue-team / DFIR investigation challenge (Hack The Box Sherlock)  
> **Theme:** Phishing email investigation + attachment handling  
> **Note:** This is a **non-spoiler** writeup (no flags, no exact answers, no solution steps).

---

## What this challenge is about (high level)
PhishNet felt like a realistic “SOC phishing triage” exercise:
- inspect a phishing message
- extract useful artifacts (sender/URLs/attachment indicators)
- validate an attachment safely
- document findings clearly

It’s the kind of work a SOC analyst might do when a user reports a suspicious email.

---

## What I practiced (SOC/DFIR skills)
- Treating the email as evidence (not just reading it like normal text)
- Handling attachments carefully (hashing, validating, and extracting)
- Staying methodical: collect artifact → confirm → document → decide

---

## Evidence handling (what I did)
- I downloaded the provided attachment (zip) and was able to compute the **SHA256** hash without issues.
- I also answered the other “artifact extraction” questions from the provided evidence.

---

## The real struggle I had (and what it taught me)
One task required me to **extract the zip file** and identify the file inside it.

This is where I got stuck:
- The zip file was **very small (~75 bytes)**.
- When I tried extracting it normally, the output kept showing **null / nothing extracted**.
- I tried multiple times, assuming I was doing something wrong.

Eventually I used AI help to figure out a working extraction approach, successfully extracted the content, and answered the file-name question to complete the task.

### What I learned from that struggle
- In DFIR/phishing work, tiny attachments can still matter — and “it doesn’t extract” is a real-world problem.
- When tools fail, the mindset is:
  **verify the file type → try alternate tools/methods → confirm output**
- Next time, I’ll troubleshoot more systematically before repeating the same extraction attempt.

---

## High-level workflow I followed (SOC style)
1) Identify what the question is asking (artifact? hash? file inside attachment?)
2) Collect the relevant evidence (email/attachment metadata)
3) Validate using safe handling (hashing + controlled extraction attempts)
4) Record findings and finish with a short incident-style summary

---

## Detection & response ideas (SOC thinking)
- Flag emails with suspicious attachment behavior or unusual small “container” files
- Detonate/inspect attachments in a controlled environment when possible
- Enrich with reputation checks for related infrastructure (domains/URLs) when available
- If confirmed phishing: block, hunt for other recipients, and guide users

---

## Mini SOC ticket (practice)
**Title:** Phishing email with suspicious attachment (PhishNet lab)  
**Summary:** Investigated a phishing email scenario and extracted key indicators. Attachment required validation, hashing, and controlled extraction to identify embedded content.

**Evidence (high-level):**
- Email/attachment artifacts reviewed
- SHA256 calculated for attachment
- Attachment extraction validated using alternate method after initial failure

**Assessment:** Phishing (lab)  
**Next steps:** block related indicators, search for other recipients, educate/report, and improve attachment-handling playbook.

---

## Personal takeaway
This challenge reminded me that being “good at SOC” isn’t just knowing concepts — it’s also being calm when a file behaves strangely and still getting to the truth.
