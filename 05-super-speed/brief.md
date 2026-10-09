# Quiet Responders: see it first, then decide what to change

Brief · Product, Dispatch · 9 October 2026 · For Helen Achebe · Draft

## What you asked for
Not a quiet number change. Something a handler like Kip would notice and a responder who's gone quiet would feel differently about, shown before anyone touches the code. This brief proposes that in stages, so each step is a decision for you and nothing changes who gets pinged until you've seen the evidence.

## Problem
Since 4.2 shipped on 12 August, missed pings went from about 2% to 21% in release week and are still 13% in the week of 31 August. Turned-down pings stayed flat. Four responders (The Undertow, Vesper, Meteor Mite, Farlight) fell from about 49 pings a week combined to 3, with no takes since late August.

The code explains why they can't recover. A missed ping is recorded as a decline. A decline costs 0.12 and a take earns back 0.08, so a responder needs a 60% take rate to break even. Scores only move when someone is pinged, and nothing decays. Wen's note about this has sat unanswered since 2019. A handler never sees an offer or its outcome, so nobody notices until the silence is weeks old.

Farlight (Uptown, handler Linda Pruitt) is the clearest case. Her last take was 14 Aug and she has had no pings since 28 Aug (nine days to the end of the data on 6 Sep). Before 12 Aug she was pinged on all 59 Uptown callouts and took 55. Since 12 Aug only 6 of 31 Uptown callouts reached her, and she took 2. The other 25 went to responders in Kingsbridge, Mill District and Foundry Row, and Farlight is the only responder based in Uptown. Of her last 4 pings, 3 were missed, and two of those were out-of-area callouts. All 7 misses since 12 Aug fall between 09:45 and 19:51, so there is no overnight pattern. Linda has 11 open tickets quoting ping counts that match our database exactly. Handlers like Kip describe both sides: one responder "dead quiet", another "exhausted".

## Proposal: three stages, each a decision point
**Stage 1: make it visible. No change to routing.**
- Handler roster flags it: "Farlight: no pings in 9 days while available, 3 of last 4 pings missed." Opening the row shows every ping since 12 Aug, and which Uptown callouts went elsewhere.
- Missed and turned-down reported separately, per responder, every week.
- Linda's 11 tickets, and the other open ones, get a real answer.
- What Kip notices: he sees the quiet and the overload side by side. What the responder feels: someone finally knows.

**Stage 2: give handlers a hand on the live ping.** Needs a small console feed, since handlers can't see offers today.
- A live strip shows who holds a ping, how long is left, and what happened to it.
- The handler can nudge the responder before it expires.
- On an open callout that routing sent out of area, or where the ping to a quiet responder expired, the handler can offer it to the quiet in-area responder instead. The action sits on a real open callout, never on its own.
- The offer depends on Wen Li confirming that a handler assignment records a take. If it doesn't, it gives the responder work but not a way back in the score.

**Stage 3: change the scoring. Only with your sign-off and Wen Li's input.**
- A miss is recorded as a miss and costs less than a decline.
- A quiet responder gets a real way back, and is told when they've gone quiet.
- This changes ranking for everyone, so it comes last, with the size of the change set by Wen Li and checked against Stage 1 data.

A clickable mock covering the handler and responder views is in `prototype.html`. It uses invented data.

## Owner
I (incoming PM, Dispatch) own this brief, the direction and the measures. Proposed, not yet agreed with anyone: Marcus Oyelaran's team builds it, Wen Li is the source for the ranking logic, and Sofia Marino designs the screens.

## Scope
Out, deliberately:
- A straight revert of 60s to 90s, and making the ping wait a setting. The 60s wait is a strong suspect for the extra misses (response times would confirm it), but a revert leaves the loop that stranded four people. Both are out of this brief and decided separately (Decision 3); the setting question is for Wen Li.
- Availability Confidence, which could penalise the same people twice.
- Shared cover, which doesn't reach in-area, available responders.
- Any change to the Availability Record until Supply is looped in. Starved responders may look like low-callout windows, so Supply may be booking maintenance into them. Supply contact not yet found.
- Anything that identifies who a responder is (Security Policy 4.1).

## Success measure
Numbers marked *provisional* are my placeholders, to be confirmed with Ravi Menon and Wen Li before this goes further.

- **Stage 1:** No available responder goes more than 3 days without a ping (*provisional*; N to agree with Ravi). Checked weekly from the per-responder report, starting the first week it ships.
- **Stage 1:** Missed and turned-down reported separately, per responder, weekly, not only in the aggregate acceptance rate. Live within 2 weeks of agreement (*provisional*).
- **Stage 1:** All 45 open quiet-responder and vanished-ping tickets answered within 2 weeks (*provisional*).
- **Overall outcome:** Weekly missed-ping rate back under 5% by the end of Q4 (*provisional*; it was about 2% before 4.2, 13% in the week of 31 August). Turned-down pings stay flat, so the gain is not just a shift between the two.
- **Stage 2:** Handlers use the live strip and offer-instead on real callouts, and quiet-responder tickets stop arriving. Target to be set when Marcus sizes it (*not yet set*).
- **Stage 3:** Every responder who is available and in range gets pinged again, and none sits below the score floor for more than a week (*provisional*). The size of the change is Wen Li's call, checked against Stage 1 data.

## Decisions for you
1. Agree the staged direction, with Stage 1 starting now.
2. Whether Stage 2 and 3 should be treated as Q4 commitments. The Q3 roadmap hasn't been reconciled since 30 June, so this is also a chance to settle which Q3 items are still committed.
3. Whether you want a ping-wait revert, or making the ping wait a setting, considered in parallel as its own decision (outside this brief).

## Open questions
- **Wen Li:** miss penalty size and what "way back" looks like in ranking. Are scores stored permanently or only in memory? Do overrides record a take? Travel times between neighbouring areas?
- **Response times:** none in the database. I can't yet confirm the four are simply slower, and no responder has been heard directly.
- **Evidence gaps:** no prior-year data, and callouts fell about 15% from 12 Aug across 14 of 15 areas, cause unknown.

## Next steps
1. You agree the direction.
2. I ask Ravi for the per-responder split and Nadia to answer the open tickets (Stage 1).
3. I take Stages 2 and 3 to Marcus and Wen Li to size.
4. I talk to Linda and one quiet responder before anything is built.
5. I find the Supply contact before touching the Availability Record.
