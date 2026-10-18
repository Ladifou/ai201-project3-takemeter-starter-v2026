# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. _"The model is accurate"_ is an
opinion. _"Every label has an F1 of at least 0.60 on the held-out set"_ is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — _"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"_. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area                  | A question it could answer                                            |
| --------------------- | --------------------------------------------------------------------- |
| Overall accuracy      | How often does it need to be right to be worth using?                 |
| Per-label performance | Is one label allowed to be much worse than the others?                |
| Balance               | How lopsided can your label counts get before it's a problem?         |
| Consistency           | If someone else labelled the same posts, how often should you agree?  |
| Confidence            | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

Accuracy on the held-out test set is at least 0.70 in each of the three seeds.

**Why this target:**
With two labels, a coin-flip guesser gets 50%. At 0.70 the tool is wrong on about 3 posts in 10, which on a test split of about 40 posts is roughly 12 posts to check by hand per run. Anything worse means the output needs review before anyone acts on it.

---

## 2.

Each label has an F1 of at least 0.60 in each of the three seeds, and the two labels' F1 scores differ by no more than 0.15.

**Why this target:**
Analysis and Hot take are the hard pair, and the smaller label is the one most likely to be neglected.

---

## 3.

No label makes up more than 65% of labels.csv, so the smaller label has at least 35% of the rows.

**Why this target:**
If one label were 70% of the data, always predicting it would score 0.70, exactly my accuracy target, so accuracy would show nothing about learning.

---

## 4.

I re-label a random 20 of my own posts after at least a week, without looking at my first labels, and agree with my first labels on at least 18 of them (90%).

**Why this target:**
The consistency question is whether the rules produce the same label twice.

---

## 5.

Among test posts where the model's top probability is at least 0.80, at least 85% are correct, and that rate is at least 10 points higher than for posts below 0.80, in each of the three seeds.

**Why this target:**

Confidence only helps if a confident call is more reliable than an unsure one. I expect confident mistakes at the Analysis and Hot take boundary, since a heated Hot take can look like a sourced claim.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
