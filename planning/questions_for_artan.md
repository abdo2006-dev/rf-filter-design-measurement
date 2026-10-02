# QUESTIONS FOR ARTAN

*Batched, grouped, and deliberately short. Artan is a PhD student with his own work; a wall of
fifteen bullet points is a worse use of his time than six grouped questions, and it gets worse
answers.*

**Principle.** Ask in natural language, group by topic, and never prejudge the answer. Where his
answer determines a project decision, record it in `decision_log.md` with the date.

---

## ROUND 1 — critical blockers only

**Status:** ready to send. **Blocks:** gate G0, and therefore everything.

**Send this. Don't expand it.**

> Hi Artan,
>
> I've scoped the filter project we discussed and I'm at the point where the next real decisions
> all depend on what the lab actually has, so I wanted to ask you a few things before I start
> designing anything.
>
> **1 — Board material.** What laminate would I actually be building on, and is there a datasheet
> I can have? I specifically need the εr it's quoted at (and at what frequency), the loss tangent,
> the thickness and the copper weight. I'd rather design against the real numbers than assume FR-4.
>
> **2 — Fabrication.** Where would the board get made, roughly how long does it take, and what are
> the limits — minimum trace width, minimum gap, and the etch tolerance if that's known? The
> minimum gap especially: it decides whether a coupled-line filter is even realistic for me, so
> it's the one number that most changes my design.
>
> **3 — Measurement.** Which VNA would I be using, what frequency range, and which calibration
> kits are actually available for it? Also which connector type I should design the launch for
> (and if there's a launch footprint the group already knows works, that would be more useful to
> me than anything I could read).
>
> **4 — Software.** Which ADS version do we have, and is Momentum included in the licence? I'd like
> to do the planar EM step, but I'd rather know now if that isn't available than build the plan
> around it.
>
> **5 — Your preference on the filter itself.** For what you had in mind educationally, would you
> rather I did a low-pass (stepped-impedance — simpler, no critical gaps) or a band-pass
> (coupled-line or hairpin — richer theory, harder to fabricate)? And is there a frequency region
> that makes sense given the substrate and the VNA? I have a few candidates but I haven't fixed
> anything, and I'd rather your input came before the choice than after it.
>
> **6 — One thing I want to get right early.** You mentioned the fixture → DUT → fixture cascade
> and removing the fixture mathematically. From what I've read, most of the realistic ways to do
> that need extra structures on the same board — a thru, a reflect, line standards, or a 2x-thru —
> so the decision has to happen *before* the board is made, not after. Is that worth planning for
> on our panel, and is it realistic with the kit we have? I don't want to find out after
> fabrication that I've made it impossible.
>
> No rush on all of it at once — even just 1, 2 and 3 would unblock me.
>
> Thanks,
> Abdulrahman

**Why it is in this order.** Questions 1–3 are the G0 blockers and are pure fact retrieval, so they
are cheap for him to answer. Question 4 is a yes/no. Question 5 invites his judgement, which is
what a mentor is for, and is placed *before* any design exists so his answer actually shapes the
work. Question 6 plants the pre-fabrication constraint early — it is the single most expensive
mistake available in this project, and it costs one paragraph to avoid.

**What to do with the answers.**
1. Fill `design/hardware_constraints.md` — every field, with the date and "per Artan".
2. Decision-log each one. His answer to Q5 becomes D-002/D-003 input; Q6 becomes D-006 input.
3. Score the 6 BLOCKED rows in `design/topology_selection.md`.
4. Open G0.

**If he answers only partly:** that is fine and expected. Mark the rest BLOCKED, proceed with
theory block B and P1 only, and re-ask the remainder in two weeks. **Do not** fill a blank with an
assumption.

---

## ROUND 2 — before PCB layout freeze

**Status:** drafted; do not send yet. **Blocks:** gate G8.
**Send when:** G6 has passed (microstrip model done) and before any layout work begins.

> Hi Artan,
>
> The filter design is through microstrip simulation and I'm about to start layout, which means
> I have to freeze the measurement strategy now — whatever I don't put on the panel, I can't do
> later.
>
> Where I've got to is that there seem to be a few genuinely different routes, and I can't tell
> which is realistic for us:
>
> - calibrate to the coaxial/connector plane with the kit we have, then de-embed a fixture model
>   I get from EM simulation;
> - put TRL standards on the board in microstrip and calibrate to the microstrip plane directly;
> - fabricate a 2x-thru coupon and de-embed that way;
> - just do a port extension / electrical delay correction and be honest that it's crude;
> - or decide the equipment doesn't support a defensible de-embedding and not claim one.
>
> I don't want to pick based on what I've read rather than what we can actually do, so:
>
> **1 —** Which of those is realistic with our VNA and calibration kit, and is there one you'd
> steer a student away from?
>
> **2 —** Should I put test structures on the same panel, and if so which ones? I have room for a
> few coupons and the extra cost is mostly connectors.
>
> **3 —** Is there a point where you'd say the de-embedding isn't worth attempting and I should
> just report the measured result with the fixture in it? I'd rather plan for that outcome than
> force a number I can't defend.
>
> Happy to show you the layout before I send it off, if you have time.
>
> Thanks,
> Abdulrahman

**Note on Q3.** It is asked deliberately. Giving the mentor explicit permission to say "don't
bother" makes a no-go answer easy to give, and a clean no-go at G13 is a much better outcome than
a de-embedded curve nobody can defend. See `MASTER_PROJECT_PLAN.md` G13.

---

## ROUND 3 — before fabrication order *(outline only)*

Send with the layout attached, if he offered to review it.

- Does the launch footprint look right to him?
- Anything on the panel he'd add or remove?
- Should I order spares? (Default answer: yes. Boards are cheap, a destroyed only-unit is not.)

---

## Standing rules for mentor contact

1. **Batch.** One grouped message beats five pings. This file is the buffer.
2. **Never ask what a datasheet answers.** Ask what only he knows: what the lab has, what the group
   has learned, what he would steer a student away from.
3. **Record every answer the same day**, in `decision_log.md`, dated and attributed.
4. **Show work before asking for judgement.** By Round 2 he should be looking at a finished
   microstrip design, not a question about what to do.
5. **A "no" is useful.** "Momentum isn't licensed", "that gap isn't manufacturable", "don't attempt
   de-embedding" each save weeks. Ask questions that make a no cheap to give.
6. **Do not relay AI claims to him as fact.** If something in this repository came from an AI and
   has not been checked, say so when asking. He is the project's reality check and that only works
   if he knows which parts are unchecked.

## Question parking lot

*Non-blocking questions, to ride along with a future round.*

- Which T-parameter convention does the group use?
- Is there a group ADS workspace template or house substrate definition?
- Does he trust the datasheet εr at our frequency, or would he characterize the laminate first?
- What convergence threshold does he consider adequate for a Momentum filter model?
- Is the observed simulation/measurement discrepancy typical in his experience for this
  substrate and frequency? *(ask at P11, with the data in hand)*
- Would he be willing to look at the seminar's RF content for errors before it is delivered?
