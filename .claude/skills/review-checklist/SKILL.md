---
name: review-checklist
description: Reviews a product brief against the PM's standing checklist before it moves forward. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief file and asks if it is ready to go further.
---

# Review checklist

Run the same check on any brief, every time. The user points you at a brief (a file path, or text pasted into chat). If they haven't said which brief, ask once, then proceed.

Read the whole brief first. Then check the four items below, in order. Judge only from what the brief actually says; don't fill gaps with assumptions or with knowledge from elsewhere. Quote or point to the line you based each verdict on.

## The four checks

1. **Owner named.** The brief names a specific person who owns it (not just a team or "TBD"). If several people are named, say whether it's clear which one is accountable.
2. **Success measure.** The brief says how we'll know it worked: a metric, a target or direction, and ideally a time frame or the way it will be measured. "Improve the experience" doesn't count.
3. **Scope matches.** Compare the scope stated at the start (goals, what's in/out) with the scope at the end (deliverables, rollout, next steps, open items). Flag anything that appears at the end but wasn't promised at the start, anything promised at the start that never shows up, and any success measure that doesn't match what is actually being built.
4. **Problem before fix.** The problem is explained, with evidence or a clear account of who is affected, before any solution is proposed. Flag solutions that appear first, and problems that are only described in terms of the fix ("we need X").

## Verdict per check

Mark each as one of:
- **Pass**: clearly met, with the supporting line.
- **Partly**: present but vague or incomplete; say what's missing.
- **Fail**: absent or contradicted.

## Output format

```
Brief: <title / file>

1. Owner named: <Pass | Partly | Fail> — <one line, with quote>
2. Success measure: <...>
3. Scope matches: <...>
4. Problem before fix: <...>

Summary of my understanding
<3-5 sentences in plain language: what problem this brief is about, who is affected, what it proposes, who owns it, and how success will be judged. Say "not stated" for anything the brief doesn't say, rather than guessing.>

Ready to move forward? <Yes / Not yet>, because <one sentence>.
Fix before it moves: <short bullet list of the specific changes, or "nothing">
```

## Rules

- The summary of understanding is required every time, even when all four checks pass. It is the user's confirmation that the brief is understood before it goes further. Keep it short and use only what the brief says.
- "Ready" means all four checks pass. Any Partly or Fail means "Not yet".
- Review only; don't edit the brief unless the user asks you to.
- Don't add checks beyond these four. If something else looks wrong, mention it in one line after the output, labelled "Also noticed".
