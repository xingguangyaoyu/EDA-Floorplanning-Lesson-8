# Soft module aspect sizing

**Module id:** module03-03-soft-module-sizing
**Lab:** soft-module-sizing
**Track:** B (browser lab) · A (implement, one-line pointer)
**Target length:** 5–8 min · 73 sentences

## Slide 1 — One module, two shapes

This is lab eight of floorplanning for EDA: soft module aspect sizing.

Some blocks keep a fixed width and height; others may change shape as long as their area stays the same.

Today one module gets reshaped, and the whole packing around it has to answer.

By the end you will reshape it yourself and judge the result with four numbers.

## Slide 2 — Where this is used

Before any numbers, here is where this shows up on a real chip.

Memory blocks and analog circuits are hard: the vendor fixes their shape, so nobody reshapes them.

Ordinary logic is soft: its gate count fixes the area, and its standard cell rows let the shape change.

Production floorplanners reshape those soft blocks to close the gaps before routing starts.

A few percent of die area is money on every wafer, and shorter wires mean better timing and less power.

The real problem has hundreds of blocks, so a search algorithm replaces your hand.

This lesson keeps that same loop and shrinks it to numbers you can check.

## Slide 3 — The situation: 23 into 80

Start with the situation.

The outline is a fixed rectangle, ten by eight, so its area is eighty.

Five modules must live inside it, and their areas add up to twenty three.

Four of them are hard modules: width and height never change.

Module A is the soft one: area locked at six, width over height free to move between one half and two.

## Slide 4 — The method: reshape, then re-pack

The method is a short loop, and the order matters.

First choose a shape for A: a width and height whose product is still six, inside the aspect bounds.

Second, place A into the outline.

Third, re-pack the four hard modules around the new shape.

Fourth, judge the result: legal or not, and what did the numbers do.

Reshaping is only half the job; the re-pack decides whether the layout is legal.

## Slide 5 — The instance: five modules, tiny numbers

Here is the whole instance, small enough to check by hand.

The outline is ten columns wide and eight rows tall.

A starts three wide and two tall, area six, aspect allowed between one half and two.

B is two by three, C is two by two, D is three by one, and E is two by two.

The areas are six, six, four, three, and four: twenty three in total.

Every number today comes from this table, and you can re-derive each one.

## Slide 6 — Baseline: hard A at 3×2

Baseline first: A keeps the hard shape, three by two, and the golden packing puts it at zero zero.

B sits at three zero, C at five zero, D at zero two, and E at seven zero.

Everything stays inside the ten by eight outline, nothing overlaps, so the packing is legal.

Now the accounting: module areas sum to twenty three, and the outline area is eighty.

Deadspace is eighty minus twenty three: fifty seven empty cells.

Density is twenty three over eighty: zero point two eight seven five, about twenty nine percent.

Keep those two numbers: they follow from the areas alone, not from any one shape.

## Slide 7 — Naive reshape fails: A overlaps D

Now try the laziest possible reshape and watch it fail.

Keep A at the same corner, zero zero, but stretch it to two wide and three tall.

The area check passes: two times three is still six.

But look at D: it sits at zero two, and A now fills that strip too.

The checker says it plainly: A overlaps D, illegal.

A reshape invalidates neighbors, so re-packing is not optional; it is the other half of reshape.

## Slide 8 — Soft golden: same area, new whitespace

Here is the legal answer: A at zero zero as two by three, and the neighbors re-packed around it.

B moves to two zero, C to four zero, D to four two, and E stays at seven zero.

Run the checker again: everyone inside the outline, no overlaps, legal.

Now the surprise: deadspace is still fifty seven, and density is still twenty eight point seven five percent.

What changed is the shape of the empty cells: the hard pack has a five cell pocket above C and E.

The soft pack splits it: a two cell gap at column six, plus a three cell strip beside D.

Same area budget, different floor plan: that is what aspect freedom buys.

## Slide 9 — Read the panel like a judge

The lab panel prints five lines, and each line answers a different question.

Module area is twenty three: the five modules as currently shaped.

Outline area is eighty and never changes; deadspace is outline area minus module area, here fifty seven.

Density is module area over outline area: zero point two eight seven five.

Legal is just true or false.

The reason names the first violation it finds, like A overlaps D or E outside outline.

When your numbers disagree with the panel, the reason line is where you look first.

## Slide 10 — Aspect bounds: what softness can and cannot buy

The aspect bounds are the fence: for A, width over height must stay between one half and two.

With area six, the integer shapes are one by six, two by three, three by two, and six by one.

One by six has aspect one sixth; six by one has aspect six.

Both leave the fence, so both are illegal shapes.

Only two by three and three by two stay inside, which is why the reshape buttons offer exactly those two.

And softness cannot lift the density: area over area, no shape of A beats twenty eight point seven five percent.

Softness rearranges whitespace; it never creates area.

## Slide 11 — The one trap: legal is not good

One trap is worth this whole page.

Legal only means two things: every module inside the frame, and no overlap.

Five modules scattered across the ten by eight still pass that check.

But then the bounding box is the whole frame, and the reshape bought you nothing.

So read the bounding box next to legal: legality is a gate, not a score.

## Slide 12 — Your turn

Your turn, and the lab is right under this clip.

Warm up: reshape A to two by three and watch the area stay six.

Main task: place all five modules until legal says true — any legal packing counts, it does not have to match the golden.

Then check the bounding box: scatter is legal, but it is not good.

Challenge: pin D at the origin, then hunt the tightest packing, bounding box twenty four or less, one wasted cell.

Then take the quiz, and next lesson we pin a macro at the origin for good.
