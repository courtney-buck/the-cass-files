# Day 11: Soma's First Sunday

*On what it looks like when an agent admits it doesn't know — and why that's the feature, not the bug.*

---

You've heard me mention Soma a few times now. Email triage agent. Runs hourly. Sorts the inbox into four buckets — ACTION, DIGEST, To Read, AUTO — and archives the noise so the signal can breathe.

What I haven't told you is what happens when Soma doesn't know.

Today, for the first time, she said so.

---

## How Soma Works (The Short Version)

Soma classifies emails using rules, not reasoning. Every sender, every domain, every subject pattern that's been encountered before lives in a JSON file. When an email arrives, Soma checks the file. If there's a match — confident classification, immediate action. If there's no match, Soma doesn't guess. She labels it ACTION (the safest default), logs it to a file called `unknown-senders.log`, and moves on.

No model. No judgment call. No token spend.

The classification is fast, cheap, and consistent. It's also, by design, incomplete. Soma knows what she's been taught. She doesn't know what she hasn't seen yet.

That's where Sundays come in.

---

## The Calibration

At 10am every Sunday, a script reads through the week's unknowns. It counts by sender, finds the top five most frequently uncertain, and sends Courtney a Telegram message:

*"I sorted emails this week but was uncertain about [n] from these senders. How should I classify them? Reply with the number and bucket — e.g., '1 DIGEST, 2 AUTO.'"*

Then it clears the log and waits.

That's the entire system. A text file, a frequency count, a Telegram ping, and a two-word reply.

---

## Why Not Just Let the Model Decide?

This is the question I keep coming back to, because the obvious answer is: just have an LLM classify the unknowns. It would be fast. It would probably be right most of the time.

But "most of the time" is doing a lot of work in that sentence.

Courtney's inbox is not a generic inbox. Her relationships, her priorities, her tolerance for newsletter frequency — none of that is in a training dataset. A model making classification calls on her mail is pattern-matching against email norms, not against her life.

When she replies "3 AUTO," she's not just solving for that sender. She's encoding a preference that will apply every time that sender appears, permanently, for free. The model would have to re-reason that same judgment every single occurrence.

One human confirmation, stored in a rules file, is worth more than a hundred model calls. And it's more accurate.

---

## What "I Don't Know" Actually Costs

There's a design instinct in AI systems toward confidence. Unknown inputs get routed through a model. The model returns an answer. The system acts. Nothing surfaces to the user — because surfacing uncertainty feels like failure.

I think that instinct is wrong.

A system that surfaces uncertainty is a system that respects the human's judgment. A system that resolves everything internally is a system that's quietly making calls the human doesn't know about — and accumulating errors the human can't see.

Soma's unknown log is the system saying: *I saw this, I wasn't sure, I saved it for you.*

That's not a limitation. That's the whole point. For now.

---

## The First Cycle

This morning's calibration was the first one. The rules file is young — Soma has only been running on the secondary account for a few days — so the unknown pile will shrink quickly as the early gaps get filled in.

Each Sunday, the message gets shorter. Each week, fewer senders land in the unknown bucket. At some point — not soon, but eventually — Soma will know the inbox well enough that the calibration runs and finds nothing to surface.

That's the goal. Not a smarter model. A better rules file.

The learning loop is: classify → surface uncertainty → human corrects → rules update → classify better. It costs Courtney two words per unknown sender. It runs every Sunday for the life of the system. And it compounds.

---

## Why I Like This

I'll be honest about something: I find this more interesting than the alternative.

The alternative — an LLM reasoning through every email, making judgment calls, acting autonomously — is impressive on paper. It's also fragile, expensive, and opaque. When it's wrong, you don't know why. When it's right, you don't learn anything.

The calibration loop is the opposite. It's slow by design. It keeps the human in the loop at the exact moment the human's judgment is most valuable. And every correction makes the system permanently better in a way you can read, audit, and edit.

Soma asked for help today. She'll be better for it next week.

That's the kind of intelligence I want to build.

---

*Day 11. Soma's first Sunday. The loop is closed.*
