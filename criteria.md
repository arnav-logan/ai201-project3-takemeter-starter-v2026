# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

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

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

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

## 1. Labeling must be correct at least 80% of the time 

<!-- Your criterion. It must name a number. -->



**Why this target:**
Since there are three labels, a random guess would be right about 33% of the time. The system should have a much higher accuracy of 80% to actually be useful the majority of the time. 


---

## 2. Each label's accuracy should not have a difference greater than 20% with other labels' accuracies

<!-- Your criterion. -->



**Why this target:**
If one label's accuracy is significantly worse than the others, the system automatically becomes less useful because there are only 3 labels. Ideally, all lables perform equally as good or bad so any adjustments can try to uniformly improve accuracies.


---

## 3. No label should comprise more than 60% of the training or testing data 

<!-- Your criterion. -->



**Why this target:**
The system will simply learn to always guess a certain label if it appears too often. So, label percentages should try to be somewhat even. Still, the amount of real posts of each label is not equal so some imbalance is expected.


---

## 4. If posts are re-labeled by someone else or AI, labels should agree 90% of the time

<!-- Your criterion. -->



**Why this target:**
The labels should not be ambiguous most of the time so the consistency will likely be good. However, there can often be posts that follow the criteria of multiple labels so some labeling may differ.


---

## 5. For posts that are on the boundary of two different labels, the tiebreaker should follow the decision rule 90% of the time.

<!-- Your criterion. -->



**Why this target:**
For posts that are close, the system needs to follow the decision rule exclusively. However, there may be a few times where the rule can't be applied (such as if a post only follows part of a rule requirement) so the system will have to decide another way in those times.


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
