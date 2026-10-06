# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I'm the incoming PM for **Rook Dispatch**, replacing Priya Raghunathan (left 21 Aug 2026; no overlap).
Sources: `00-rook/company/notes/handoff-from-priya.docx` and the Rook wiki (Company section), read 6 Oct 2026.

### The company
- Rook Industries sells coordination and provisioning software to the protective-response sector. Real customers are independent masked **responders** and the **handlers** and **quartermasters** who support them. Rook employs none of them.
- Founded 2014; HQ Site Aleph (ice-shelf research station, twice-weekly transport, so most staff are remote); offices in Berlin, Singapore and a Cornish lighthouse. 241 employees. Subscription revenue, priced per active responder.
- Monthly release train; point releases are 4.x. Three support tiers; tickets filed from inside an active callout bypass the queue.
- **Hard constraint:** Rook never stores or can reconstruct a mapping from a responder's cover identity to a legal identity (contractual; Security Policy 4.1). Never design for, or try to work out, who anyone is.

### Products
- **Dispatch** (mine, flagship, release 4.2): handler web console plus responder phone app. Flow: incident enters console → Dispatch ranks available responders (routing priority) → ping to the top responder's phone → taken, or turned down / missed and it moves to the next. Routing config ships with the release; handlers can't change it at runtime. Handlers can override routing (audit log since 4.0).
- **Supply** (separate PM): requisitions → quartermaster approval → fulfilment → maintenance schedule from service intervals; field failure reports feed back.
- **Dependency to remember:** Dispatch writes the Responder Availability Record; Supply reads it to schedule maintenance into low-callout windows. Any change in how Dispatch calculates or updates that record silently changes Supply's scheduling. Loop in Supply before touching it.

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one callout offered to one responder. **Taken / turned down / missed** (nobody answered within the ping wait; recorded separately from turned down, though both move the ping on).
- **Ping wait**: how long a ping stays live. Set in the release, same for everyone. (Priya's note calls this "ping timeout"; same thing.)
- **Routing priority**: ranking score. Inputs: proximity (travel-time estimate since 4.1), availability, capability match, recent acceptance history. Turning down or missing pings lowers recent acceptance, which lowers future rank.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation.
- **Metrics**: *acceptance rate* (headline; pings taken / pings; weekly, aggregate), *time-to-accept* (median seconds ping to taken), *coverage gap* (no available responder had the tags; means nobody *could* go, not that nobody *would*).
- **Mutual aid**: cross-area cover between responders. Not supported; Q4 exploration.

### People
- **Helen Achebe**, Director of Product (Site Aleph): my director; owns roadmap and commitments.
- **Marcus Oyelaran**, Eng Manager, Dispatch (Site Aleph): start here when unsure; can pull numbers.
- **Wen Li**, Staff Engineer (Berlin): built the ping-ranking logic. No written spec exists; she is the source. Was away 14-24 Aug, i.e. just after the 4.2 ship.
- **Nadia Hoffmann**, Support Lead (Berlin): owns the tickets; hears handler complaints first. Priya suggests a standing 15 minutes.
- **Sofia Marino**, Product Designer (Site Aleph): console and phone app; ran the September interviews.
- **Ravi Menon**, Data Analyst (Singapore): weekly acceptance-rate reporting.

### Where things stand (as of 6 Oct 2026)
- **Releases:** 4.0 (7 Apr: new nav, profile redesign, override audit log); 4.1 (16 Jun: travel-time proximity, bulk callout, push reliability; mobile stable since); **4.2 (12 Aug)**: proximity weighted up in routing, ping wait cut 90s → 60s, console filters persist, three defect fixes.
- **The live problem (rook-database, 29 Jun-6 Sep; ~1,700 pings):** Priya's "mostly seasonal" read is not supported. Weekly acceptance was a flat 75-78% through 9 Aug, then 54% (week of 10 Aug), 66%, 67%, 73% (week of 31 Aug): a step change on release week, only partly recovered. Turned-down pings stayed flat (~35/week); the whole drop is **missed** pings, 1-3% before vs 21% in release week, 13% by early Sep. Daily, misses went from ~0 to 7-12 on 12 Aug itself. That fits the 90→60s ping wait cut; the routing change is a separate suspect. Callouts also fell (~138/week to 110-127); no prior-year data, so seasonality can't be ruled in or out for that.
- **Starvation loop (hypothesis):** four responders (The Undertow, Vesper, Meteor Mite, Farlight) averaged ~49 pings/week combined before 4.2, then 43, 16, 6, 3, with zero taken since late Aug. The other 12 absorbed the load (123 → 162/week). Consistent with: missed ping → lower recent-acceptance score → fewer pings → no chance to recover. No response-time column exists, so I can't confirm *why* they missed. Ask Wen Li whether recent acceptance ever recovers.
- **Tickets** (147 total): "ping moved on before he could answer" (13) and "responder getting few/no pings" (26) were **zero before 12 Aug**; filter-persistence tickets are 14 (incl. thank-yous), the "noise" Priya predicted. Roughly 6-8 tickets/week before, 20-32 after. Many remain open; Nadia's team has not closed the loop.
- **Q3 roadmap** (last reviewed 30 Jun, so stale; Priya owned every row):
  - 4.2 committed: routing change (shipped), ping timeout tuning (a 90→60 cut shipped; unclear it's the intended "tuning"), **Availability Confidence** (confidence score beside stated availability) — **not in 4.2 release notes, so apparently dropped**.
  - 4.3 committed: requisition approval chains (Supply).
  - Q4 exploring: handler phone app (today handlers are web-only), shared cover between responders.
  - Priya says "a couple" of items were squeezed out of 4.2 and that I need to agree with Helen which are still Q3 commitments. Not yet done. Roadmap changes go through Product.
- **Known noise:** console filter persistence will generate cosmetic tickets; don't let it eat the first month.
- **Open to-dos:** write down how we decide who gets pinged (nothing exists; work it out with Wen Li); reconcile roadmap with Helen. Priya admits she made calls faster than she checked them, so expect unexamined decisions.
- **Handler interviews** (Sofia, 2-5 Sep, console-redesign research, 4 handlers; routing wasn't the topic, so these are volunteered): Aunt Dot (Vesper) and Mr. Ambrose (Capt. Vantage) describe pings vanishing before the responder reaches the phone, "more than it used to"; Dot also reports quiet stretches and had never connected the two. Kip: Meteor Mite is dead quiet while The Gale is "exhausted", "all the way to one side or the other, no middle". Halloran (Bulwark) mentions one early-ping loss, otherwise Supply complaints. Corroborates the database; Vesper and Meteor Mite are two of the four starved responders. Other asks: dark mode (Kip), bigger text/badges (Dot, Ambrose), warn when saved filters reset, per-responder alert sounds, tell handlers when a ping arrives. Supply: one approval queue regardless of priority (11-day wait on a cracked vest plate), failure reports vanish, poor catalog search.
- **Defect read (end of session 1):** (1) the 90→60s ping wait cut turns slow-but-willing responders into "missed" (strong evidence; Ambrose says slow answers used to still win); (2) acceptance history has no recovery path, so a responder who misses gets fewer pings and can't climb back (symptom proven, mechanism a hypothesis); (3) the headline acceptance rate is an aggregate that lumps missed with turned down, hid four near-silent responders, and also feeds the ranking; (4) 4.2 bundled two changes with no runtime control and no tracking of the slipped Availability Confidence. Strongest tell: Meteor Mite (starved) and The Gale (overloaded) are both in Eastgate, so proximity can't explain the gap, acceptance history can. Smaller: silent filter resets are a real trust issue (14 tickets, 2 interviews), not just noise; Supply has one approval queue regardless of priority.
- **Next steps:** raise the ping wait with Wen Li and Marcus first (cheapest fix to test; ask whether it can become a setting, not a release). I drafted questions for Wen Li, Helen, Marcus, Ravi and Nadia in chat on 6 Oct; they weren't saved, so ask me to redraft. Ravi should split the weekly report by responder and by missed vs turned down. Nadia should answer the open tickets from handlers whose responders went quiet. No Supply PM is named in the directory; find the contact before touching the Availability Record.
- **Possible Supply knock-on (unchecked):** if starved responders look like low-callout periods in the Availability Record, Supply may now book maintenance into them. Check with Supply.
- **Not yet read:** wiki Product briefs (Bulk Callout, Handler Phone App, Requisition Approval Chains, Routing Override Audit Log). Database has no response-time or routing-score columns.
- **Session 2 (7 Oct), interviews + tickets compared:** the code in `00-rook/code/dispatch-routing` confirms the loop: `offer.py` records a decline for a missed ping, `history.py` has no recovery (2019 TODO), and offers go only to the responder's phone, never the handler. Ticket counts corrected: quiet-responder tickets are 30 (from 4 handlers about Farlight, Undertow, Halfmoon, Corporal Ashgrove) plus 2 "first ping in days, missed it"; vanished-ping tickets are 13; all 45 still open. Only Farlight and Undertow are near-silent; Halfmoon and Ashgrove dip about 25-35%. Vesper and Meteor Mite are near-silent in the data but nobody filed tickets for them.
- **Open puzzle:** the four starved responders miss 50-65% of the few pings they still get vs about 15% for everyone else, though the ping wait is the same. Possibly they are the slowest responders; needs response times. No responder has been heard directly, only through handlers.
- **Interview vs ticket gaps:** Ambrose's lost callout is dated 12 Aug in ticket 3043 but "two weeks ago" in his 2 Sep interview. Halloran called Bulwark "steady" but Bulwark's misses went 0 to 18%. Nobody ticketed the overloaded side (Kip's The Gale). Tickets add shift handover/shared sign-ins (~8) and admin (18) that no interviewee raised.
- **Roadmap vs evidence:** Handler Phone App brief fixes the handler alert gap but not the 60s expiry; Requisition Approval Chains brief adds a $2,000 second sign-off while Halloran and tickets want urgency handled in the queue; Availability Confidence could double-penalize starved responders; shared cover doesn't help them (they are in-area and available). Bulk callout shipped in 4.1 though its Jan brief says unowned.
