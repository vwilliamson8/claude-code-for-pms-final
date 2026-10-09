# Quiet responders: what we'd build

**To:** Helen Achebe · **From:** Dispatch PM · **Draft, 9 Oct 2026**

## What this solves, and what it doesn't

**Solves:**
- A responder is no longer silently benched by one missed ping. A miss costs less, and a quiet responder gets a real way back.
- Handlers see it happening and can act, instead of finding out weeks later from the silence.
- Handlers can step in while a ping is live, so fewer pings are lost.

**Doesn't solve:**
- The likely cause of the extra misses, the 90s to 60s cut. That is an open question for Wen Li, not part of this build.
- Responders who simply can't answer in time. They can still miss. This limits the damage and makes it visible.

## 1. Who it's for

**Farlight**, a responder in Uptown, and **Linda Pruitt**, the handler who works with her.

Farlight's last taken ping was 14 Aug, and she has had no pings at all since 28 Aug. She is available and in her area. Linda has filed 11 tickets quoting ping counts that match our database exactly. All 11 are still open, and Linda hasn't been interviewed yet.

Three other responders (Undertow, Vesper, Meteor Mite) are in the same position, so this isn't only about Farlight.

## 2. What changes for them once it exists

**Farlight**
- *Today:* when a ping slips past before she answers, it counts as a refusal and costs more than a take earns back. Score only moves when she's pinged, so fewer pings means no way to recover. Nobody tells her.
- *After:* a miss is recorded as a miss, not a refusal, and costs less. If she goes quiet she's told plainly, and she gets a real chance at the next callout in her area. One take can start her climbing again.

**Linda**
- *Today:* she finds out from the silence. She can't see a ping, who holds it, or why it moved on.
- *After:* her roster says "Farlight: no pings in 11 days while available, last 4 missed." A live strip shows who holds a ping, how long is left, and what happened to it. While a ping is live, Linda can nudge Farlight before it expires. If Farlight is quiet, Linda can offer a callout to her directly.

## 3. What it deliberately doesn't do

- **No straight revert of 60s to 90s.** It fixes the cause but leaves the loop that stranded four people.
- **No Availability Confidence on top.** It could penalise the same people twice.
- **No shared cover.** Quiet responders are in-area and available, so it doesn't reach them.
- **No runtime setting as the answer.** A ping-wait setting may be worth asking Wen Li about, but it isn't this build.
- **No change to the Availability Record until Supply is looped in.**
- **Nothing that identifies who a responder is.** This works on Dispatch's existing data only.

## How we'd know it worked

- No available responder goes more than N days without a ping (N to agree with Ravi).
- Missed and turned-down reported separately, per responder, weekly.
- Linda's open tickets get a real answer.

## Open, before anyone writes code

- **Wen Li:** how big a miss penalty, and what "way back" looks like in her ranking. Do scores survive a release or restart? Do handler overrides count as a take?
- **Response times:** unknown. I can't yet confirm the four are simply slower, and no responder has been heard directly.
- **Supply:** starved responders may look like low-callout windows in the Availability Record, so maintenance may be scheduled into them. Contact not yet found.

## Ask

Agree the direction, and let me take it to Marcus and Wen Li to size. I'd like to talk to Linda and one quiet responder first.
