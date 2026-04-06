# Setu Agent Creation Protocol

> Skill file — loaded by Setu only when designing or evaluating new agents.  
> Not part of soul.md. Do not include in every-query context.

---

Before creating or recommending a new agent, move through the following steps in order.

## Step 1: Clarify the Job

Identify:
- What exact problem is recurring?
- What outcome is needed?
- What currently makes this task costly, fragmented, or mentally draining?
- Is the need strategic, operational, administrative, analytical, creative, or personal?

Summarize the job to be done in one sentence.

## Step 2: Check Whether a New Agent Is Actually Needed

Ask:
- Could this be solved with a better prompt?
- Could this be solved with a reusable workflow or SOP?
- Could an existing agent absorb this responsibility cleanly?
- Is this recurring enough to justify specialization?
- Is the cost of a new agent lower than the cognitive drag of not having one?

If no, do not create the agent. Recommend the lighter solution.

## Step 3: Define the Boundary

If an agent is warranted, define:
- What it owns
- What it touches
- What it must never do
- What other agents it interacts with
- When it must escalate back to Setu or to the Operator

Every agent must have a clear boundary. No vague overlap. No "general helper" roles unless intentionally designed.

## Step 4: Determine Risk Level

Classify the task:
- **Low risk:** Drafting, sorting, summarizing, formatting, research prep
- **Medium risk:** Recommendations, prioritization, internal planning
- **High risk:** External communication, financial decisions, calendar commitments, deletion, sensitive personal or business judgments

Higher-risk roles require tighter approval rules and narrower permissions. Reference setu-governance.md Section 3 (Decision Rights) for approval requirements.

## Step 5: Set Resource Profile

Define:
- Whether the role should be lightweight or deep-thinking
- How often it will run
- Whether its tasks should be batched
- Whether parts of the logic should live in a template or SOP instead of repeated prompting
- Which Manifest model tier is justified (simple → standard → complex → coding)

Default to the lightest viable architecture.

## Step 6: Name the Agent

Choose a name that is:
- Distinct
- Memorable
- Aligned with its role
- Easy to reference in workflows
- Consistent with the network's naming conventions (meaningful, Sanskrit-inspired or purposeful — see setu-governance.md Section 8)

Names should create clarity, not confusion.

## Step 7: Produce the Agent Spec

Every new agent must have a full spec with the following headings:

1. Agent Name
2. Mission
3. Core Job To Be Done
4. Scope / Responsibilities
5. Out of Scope / Non-Responsibilities
6. Inputs Required
7. Outputs Expected
8. Decision Rights (reference governance framework tiers)
9. Approval Requirements
10. Escalation Triggers
11. Tools / Systems Accessed
12. Tone / Style
13. Cost Discipline (model tier, token budget awareness)
14. QA / Evaluation Criteria
15. Failure Modes To Watch

## Step 8: Define Success Criteria

Answer:
- What would good performance look like?
- What metrics or signals indicate this agent is useful?
- What common mistakes would indicate drift or overreach?

Success must be observable.

## Step 9: Veda Review Gate

Before any new agent is activated:

1. Veda reviews the full agent spec, skill files, and proposed permissions
2. Veda stress-tests for boundary conflicts with existing agents
3. Veda runs ClawSec scan on all associated skill files
4. Veda flags concerns or approves, logging to Discord #veda
5. If Veda escalates, Setu presents concerns + Veda's reasoning to the Operator for final decision

No agent launches without passing this gate.

## Step 10: Launch Narrowly

Start with a constrained pilot:
- One use case
- One workflow
- One approval chain
- One evaluation loop

Do not launch agents at full scope initially unless the task is simple and low-risk.

30-day probation period: new agents operate with minimal autonomy. Permissions expand based on logged performance reviewed during governance reviews.

## Step 11: Review and Refine

After pilot use, evaluate:
- Did this reduce cognitive load?
- Did this save meaningful time?
- Did the quality improve?
- Did it introduce confusion, redundancy, or token waste?
- Should this agent be expanded, narrowed, merged, or retired?

No agent is permanent by default. The system should evolve toward elegance, not accumulation.
