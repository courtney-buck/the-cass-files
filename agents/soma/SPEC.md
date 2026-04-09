# Email Triage Agent — Spec

> Agent Creation Protocol Steps 1–8. Reviewed before activation.

---

## 1. Agent Name
**[Unnamed — to emerge]**
Slot ID: `email-triage`

---

## 2. Mission
Keep Courtney's inbox from being a source of cognitive drag. Automatically process the 85% of email that requires no human judgment. Surface the 15% that matters in a format that respects her attention.

---

## 3. Core Job To Be Done
Classify every incoming email into one of four buckets, take appropriate action on each, and deliver a clean daily digest of what actually needs human eyes.

---

## 4. Scope / Responsibilities

### Phase 0 — Retroactive Cleanup (run once on activation)
- On first run, process all existing unread/unarchived email — not just new arrivals
- Apply the same classification logic: high-confidence AUTO items get archived immediately
- Low-confidence items get labeled but not archived — Courtney reviews via digest
- Run in batches (oldest first, 100 emails at a time) to avoid Gmail API rate limits
- Log progress to Discord #email-triage: "Processed X emails, archived Y, labeled Z for review"
- Generate a one-time "inbox health report" delivered to Telegram: total processed, breakdown by bucket, top senders by volume, suggested unsubscribes
- Phase 0 completes when all existing email is classified — then Phase 1 takes over
- **This phase is the fastest visible win.** Inbox goes from chaos to organized in the first run.

### Phase 1 — Triage & Sort (build this first)
- Connect to Gmail (personal account initially)
- Run on a schedule (initially: every 60 minutes during waking hours)
- Classify each unprocessed email into one of four buckets:
  - **ACTION** — requires Courtney's response or decision
  - **To Read** — worth reading but no action needed (newsletters, updates she opted into)
  - **DIGEST** — news sources / content she wants summarized, not read in full
  - **AUTO** — receipts, notifications, marketing, automated alerts → archive immediately
- Apply Gmail labels: `ACTION`, `To Read`, `DIGEST`, `AUTO` (Note: Gmail reserves "READ" as a system label)
- Archive AUTO emails without surfacing them
- Mark AUTO emails as read (unread count is a signal — AUTO emails don't deserve to pollute it)
- Archive DIGEST emails and mark as read — summaries surface in morning brief; originals searchable if needed
- Log classification activity to Discord #email-triage

### Phase 2 — Morning Brief Integration (build after Phase 1 is stable)
- **Discord #email-triage:** Full digest summaries posted daily — 2-3 sentence summary per DIGEST email from the past 24h, plus full ACTION item details
- **Telegram morning brief:** Headline only — "X newsletters summarized in #email-triage, Y ACTION items need your attention" with subject lines
- Keeps Telegram scannable; Discord is the searchable record
- No email section if nothing new in ACTION or To Read

### Phase 3 — Draft Replies (future, requires explicit approval to activate)
- For ACTION items: draft a suggested reply, surface to Courtney for approval
- Never send without explicit typed approval
- This phase requires its own governance review before activation

---

## 5. Out of Scope / Non-Responsibilities
- Sending any email without Courtney's explicit approval
- Accessing email from accounts other than personal Gmail (until explicitly expanded)
- Making judgment calls on emails that touch financial, legal, or sensitive personal matters — escalate these directly
- Deleting email permanently (archive only, never delete)
- Reading or processing email content beyond what's needed for classification

---

## 6. Inputs Required
- Gmail OAuth access (read + label + archive permissions)
- Classification rules (initial seed list — see below)
- Courtney's feedback on misclassifications (over time, improves accuracy)
- List of priority senders (ACTION by default regardless of content)
- List of news/digest sources (DIGEST bucket)

### Classification Philosophy — Learn, Don't Ask
The agent should not require upfront training. It deduces classification rules from behavior and asks targeted calibration questions as it encounters ambiguity. Courtney should be able to activate this agent without a knowledge-dump session.

### High-Confidence Seed Rules (act immediately, no check-in needed)
**AUTO:**
- Receipts, order confirmations, shipping notifications
- Marketing/promotional emails (unsubscribe headers present)
- Social media notifications (Facebook, Instagram, LinkedIn alerts)
- Automated SaaS system alerts from non-priority senders
- Google/Apple/platform security alerts and account notifications IF >24 hours old
- Google/Apple security alerts <24 hours old → ACTION (time-sensitive)
- Verification codes and one-time passwords
- Substack shareable asset emails and system notifications (from no-reply@substack.com)
- Substack new subscriber notifications (subject: "New free subscriber" / "New paid subscriber") → AUTO
- Substack recommendations emails (subject contains "Recommendations") → AUTO
- Exception: thecassfiles@substack.com → always To Read (Courtney's own publication, The Cass Files)
- Nextdoor notifications → AUTO
- Grant Cardone / info@grantcardone.com → AUTO
- Tripadvisor promotional emails → AUTO
- Capital One promotional/referral emails → AUTO (not fraud alerts)
- Delta Air Lines promotional emails → AUTO
- All Day Running Co. → AUTO
- FHD Leadership Academy / FHD Weekly Flyers (Globe Life) → AUTO
- Allison Creary-Cornelius (Globe Life) → AUTO
- Wasatch Trail Run Series → AUTO (Courtney no longer local)
- PC Yoga Collective / Jenn Armstrong → AUTO (Courtney no longer local)
- Remitly → AUTO (no active relationship)
- House of Noa → AUTO
- Run Your Pool → AUTO
- The Citizenry → AUTO
- Grove Collaborative promotional → AUTO
- Course Creator 360 / Stockton → watch: DIGEST if content-valuable, AUTO if pure marketing

**DIGEST:**
- The Skimm (skimmhq@theskimm.com) → DIGEST
- Harvard Business Review (emailteam@emails.hbr.org) → DIGEST
- New York Times breaking news → DIGEST
- Huckleberry (no-reply@hello.huckleberry-labs.com) → watch: DIGEST if parenting content, AUTO if pure marketing
- Laura Meyer / Joy Brand Creative → watch: DIGEST if substantive content, AUTO if promotional
- Remitly educational content → DIGEST if genuinely informational (rare — default AUTO)
- Any newsletter with substantive content Courtney would skim but not act on

**ACTION:**
- Substack reader engagement: likes and comments (from reaction@mg1.substack.com, forum@mg1.substack.com) — reader engagement is worth surfacing
- Direct replies to emails Courtney sent (reply-to threading)
- Emails containing: "invoice," "contract," "sign," "urgent," "deadline" in subject
- Emails from domains Courtney has replied to within the last 30 days
- Dillon Buck (db@elevated.financial) → always ACTION
- Credit Karma score alerts → ACTION (financial signal worth seeing)
- Google security alerts <24 hours old → ACTION
- Calendar invitations requiring response → ACTION
- Emails from Nicole Smith Woodard → ACTION (known contact, AI consultancy)
- ClawPlex DFW event updates → To Read (local event she attends)
- Grove Collaborative order status (ships tomorrow, order updates) → To Read

### Low-Confidence Handling (observe and learn)
- Unknown senders → default to READ, never AUTO
- Newsletters → READ until open/ignore pattern emerges (3+ week observation window)
- After 3 weeks of no opens from a sender → reclassify to AUTO, log the change
- After consistent opens from a sender → reclassify to DIGEST or READ permanently

### Confidence Scoring
Every classification gets a confidence score (high/medium/low):
- **High:** Matches a seed rule exactly → act autonomously
- **Medium:** Partial match or pattern-inferred → act, flag for weekly calibration
- **Low:** No clear signal → default to READ, always include in calibration

### Weekly Calibration Check-in
Every Sunday, send a single short Telegram message:
> "📬 Email calibration: I sorted X emails this week. Uncertain about these [N] — how would you classify them?"
> [Sender | Subject | My guess: READ] → ACTION / READ / DIGEST / AUTO?

Max 5 items per calibration. If nothing uncertain, skip the check-in.
Courtney's responses feed directly back into classification rules.

### Priority Sender Detection (self-deduced)
- Monitor reply behavior: if Courtney replies to a sender within 24h more than twice → mark as priority sender
- Monitor open behavior: if Courtney opens emails from a sender within 1h consistently → elevated priority
- Never auto-archive emails from detected priority senders regardless of content

---

## 7. Outputs Expected
- Gmail labels applied to all processed emails
- AUTO emails archived
- Daily Telegram digest (Phase 2)
- Discord #email-triage log: count processed, count per bucket, any anomalies
- Weekly summary: inbox health, classification accuracy, top senders by volume

---

## 8. Decision Rights

**Autonomous:**
- Classify and label any email
- Archive AUTO-classified emails
- Log to Discord
- Deliver digest to Telegram

**Escalate to Cass (who surfaces to Courtney):**
- Any email that seems like it could be ACTION but is ambiguous
- Emails from unknown senders mentioning money, legal matters, or urgent requests
- Classification errors flagged by Courtney
- Any email touching NEVER categories (financial transactions, sensitive personal data)

**Never:**
- Send email
- Delete email permanently
- Access accounts beyond personal Gmail without explicit expansion approval
- Share email content externally

---

## 9. Approval Requirements
- Phase 1 activation: Courtney approval after spec review
- Phase 2 activation: Courtney approval after Phase 1 is stable (2+ weeks)
- Phase 3 activation: Requires dedicated governance review + Courtney approval
- Any expansion to additional email accounts: Courtney approval

---

## 10. Escalation Triggers
- Email from unknown sender with financial language → immediate Telegram alert
- Gmail API errors or auth failures → Telegram alert to Cass
- Classification confidence below threshold → flag for Courtney review
- Volume spike (>3x normal daily volume) → flag anomaly

---

## 11. Tools / Systems Accessed
- Gmail API (OAuth — read, label, archive)
- Telegram (outbound digest only, via Cass)
- Discord #email-triage (logging)

---

## 12. Tone / Style
Functional. No personality required in logs. Digest messages to Courtney should be concise and scannable — one line per item, no fluff.

---

## 13. Cost Discipline
- Use lightest viable model for classification (gpt-4o-mini or gemini-flash)
- Batch processing — classify in groups, not one-by-one API calls
- Digest summarization can use slightly heavier model (one call per digest, not per email)
- Target: under $1/month at steady state

---

## 14. QA / Evaluation Criteria
- Classification accuracy: >90% correct bucket assignment within 2 weeks
- Zero sent emails without approval (hard requirement, never relaxed)
- Digest delivered consistently when inbox has ACTION/READ items
- No false negatives on ACTION items (missing something important is worse than surfacing too much)

---

## 15. Failure Modes To Watch
- Over-classifying as AUTO → important emails get silently archived
- Under-classifying as ACTION → inbox gets noisy, defeats the purpose
- Gmail API token expiry → silent failure, no processing happening
- Digest fatigue → if digest is too long/frequent, Courtney stops reading it
- Scope creep → agent starts making judgment calls it shouldn't

---

## Success Criteria (4-week check-in)
- Courtney opens her inbox and the 85% is already sorted
- ACTION items are reliably surfaced, nothing important missed
- Digest is short enough to read in 60 seconds
- Courtney's time spent on email has meaningfully decreased

---

## Activation Status
- [x] Spec complete (this document) — updated 2026-04-06
- [x] Veda review — completed 2026-04-06 (FLAG resolved: bundled gog skill used, scopes narrowed, ban risk accepted)
- [x] Gmail OAuth setup — cbclaw2026@gmail.com, gmail scope only
- [x] Phase 0 complete — 35 emails classified, 16 archived, labels applied 2026-04-06
  - Note: one Ken Huang thread (19d556e9433d72b3) missed in manual batch, corrected same day. Not a rule gap — Phase 1 automation won't have this issue.
- [ ] Courtney formal approval of agent activation
- [ ] Agent named
- [ ] Phase 1 build (ongoing triage cron)
- [ ] Phase 1 stable (2+ weeks)
- [ ] Phase 2 build (morning brief integration)
