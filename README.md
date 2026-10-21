# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->
TakeMeter uses a fine tuned LLM to classify posts from a specific online community. In this case, the system classifies posts from the subreddit r/buildapc, a community centered on questions, advice, and discussion about building a PC. Posts will be sorted into categories such as build help, discussion, and troubleshooting.


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `build help`

**Definition: Lists some or all parts of a build and asks for guidance or confirmation.**

**Example 1:**
> What deal would be better for my build? 
>  So I am trying to figure out what deal would be better value for me, my max budget is 2k USD.I am in between getting either an Intel or AMD bundle.
> I have little to no knowledge on pc building so any recommendations would be appreciated.

>Intel bundle:$629.99
>G. Skill Rip jaws(2x16)32GB ddr5 ram
>Intel core ultra 7 270k
>Gigabyte z890 Eagle WiFi7 Plus motherboard

>AMD bundle: $779.99
>G. Skill Flare (2x16)32GB ddr5 ram
>AMD Ryzen 7 7800X3D
>Gigabyte X870 Gaming Wifi6 Am5 motherboard 

**Example 2:**
> What should I do next without the CPU Cooler? 
> I want to know exactly what to do next since I don't have my CPU Cooler yet. I have the RAM installed, SSD installed, and CPU installed. I'm a first-time builder and I'm trying to get this PC finished ASAP. 

### `discussion`

**Definition: Asks a general/open-ended question or a question not about an entire build.**

**Example 1:**
> Is DDR4 still good for a long-term budget gaming build? 
> Hi guys, I'm thinking of buying a budget PC that can last me about 5 years before I need to upgrade again. Is DDR4 still good for gaming modern AAA titles and other heavy games, or should I stretch my budget for DDR5? Thanks

**Example 2:**
> Is this the worst time to buy a gaming PC? 
>  For about a month now, I want to buy a gaming PC on Black Friday if there are good deals at Micro Center But I see many of the PC community saying not to expect good sales because they will only continue and continue to rise Want I want is a PC with RX 9060 XT and 16gb ram, $1,500 aprox at Micro Center Should I last longer with my PS5 and Steam Deck? 

## `troubleshooting`

**Definition: Names a specific problem and asks for solutions or explanations.**

**Example 1:**
> PC is constantly tripping outlets in my dorm room and I don't know what to do. 
>To give a little more context. I have had this PC for about 3 years and never had any issues with it. As soon as I move into my dorm for college, my PC starts tripping the circuits in my room. It sometimes trips when my computer starts up, but there has also been times where it last for more than a week before tripping. It has tripped about 5 times now on different outlets/circuits and the electricians here believe my PC is causing the issues. I am not sure what to do at this point because I want to use my PC at school, but I can't keep tripping the breaker. If anyone has any suggestions I would appreciate it. 

**Example 2:**
> Having troubles with UX200 SE cooler and B650 motherboard
> I’m having some issues with this heat sync. Unfortunately, I didn’t look anything up besides if this was a good heat sync for its price. I’m just not seeing where to place the bracket. Any help will be appreciated. 

### The hardest boundary

**Which two labels: `troubelshooting` and `build help`**

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
     If the post names a specific problem after the pc is built (or while it's being built), then it's troubleshooting because there is a real problem after buying the parts or building the pc.  



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
r/buildapc (Reddit)

**How I labelled them:**
I labeled a few posts from each section then I let AI label the rest.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| `Build Help` | 71 | 35.5% |
| `Discussion` | 66 | 33% |
| `Troubleshooting` | 63 | 31.5% |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
> "6700 xt or a 9060 xt 8gb

>I just bought a new AMD Radeon RX 9060 XT 8GB from Newegg for a good price, but it isn’t installed yet. I’m currently running PCIe 3.0 and won’t be upgrading for another 10 months or so. My CPU is a Ryzen 5 5500, and my motherboard is a B450.  
>The dilemma is that there’s a guy near me selling a used RX 6700 XT 12GB for a good price. I know the RX 9060 XT 8GB has a full x16 interface, but I’m worried about the 8GB VRAM buffer >overflowing on PCIe 3.0.  
>My question is: In demanding 1080p games like Cyberpunk 2077 and Bodycam, is it worth returning the RX 9060 XT 8GB and buying the used RX 6700 XT for the 12GB VRAM safety net? Or would the raw >performance of the RX 9060 XT make that trade-off not worth it?"

> *Could have been:*
> `Troubleshooting`

> *I chose `Build Help`, because: Although the post mentions a problem, the post mainly asks for advice if it is worth returning the RX 9060 XT 8GB to get a RX 6700 XT for more VRAM*

**2.**
> *The post:*
>"CPU pairing for GTX 285 (possibly SLI)

>Curious what would you pick.
>GTX 285 came out in Jan 2009 as a die shrink of the GTX 280 from Jun 2008, the last DX 10 only generation from Nvidia.
>I'm planning to build a reverse sleeper retro machine around it as I was in university during that era and was way too poor to afford a gaming PC back then.
>Can't decided between sticking with a Core 2 Duo E8600 (which feels a bit more period correct for Win XP), a late Core 2 Quad or a first gen i5/i7.
>I already have a board for socket 775, but it sadly came without an I/O shield.
>Case will most likely be Fractal Pop Air."

> *Could have been:*
> `Discussion`

> *I chose, `Build Help` because: Although the post asks about the reader's thoughts on the matter, it asks for advice on a specifion CPU choice (not a general case)*

**3.**
> *The post:*
> "please help me  choose a GPU i cant decide.

>**RX 9060 XT 8GB vs RTX 5060 8GB which is better value for gaming?**
>I'm building a budget gaming PC and trying to get the best performance for my money.
>**My planned specs:**
>CPU: AMD Ryzen 5 5600G
>Motherboard: MSI B550M-A PRO
>RAM: 16GB DDR4 3200MHz
>**GPU options:**
>Sapphire Radeon RX 9060 XT PULSE 8GB OC
>NVIDIA GeForce RTX 5060 8GB
>I mainly want to play Helldivers 2 at 1080p
>Which GPU would you recommend for gaming performance and value? Is there a reason to choose the RTX 5060 over the RX 9060 XT? I'd also appreciate any compatibility advice or alternative recommendations.",Discussion,

> *Could have been:*
> `Discussion`

> *I chose, `Build Help` because: The post shows a plan of what parts to buy and asks for a GPU choice*

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**
distilbert-base-uncased

**Settings:** <!-- epochs, learning rate, batch size, seed -->
EPOCHS = 3, LEARNING_RATE = 2e-5, BATCH_SIZE = 16, Seed = 42

**Anything I changed from the defaults, and why:**
Nothing was changed

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->

train 139  ·  val 31  ·  test 30

| Label | Train | Val | Test |
| ---- | ---- | ---- | ---- |            
| Build Help | 49 | 11 | 11 |
| Discussion | 46 | 10 | 10 |
| Troubleshooting | 44 | 10 | 9 |


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* I provided Claude with label definitions and gathered data and asked it to label the unlabeled entries. 
- *What came back:* Claude labeled the entries and returned the text.
- *What I changed:* I put the labeled data in labels.csv.

**Moment 2**

- *What I asked for:* I aksked Claude if my criteria were objective and based on numbers.
- *What came back:* Claude said that the criteria looked good and I didn't need to change anything.
- *What I changed:* Nothing.

**Pre-labelling disclosure:**
Yes, I used AI to prelabel and I corrected any incorrect labels.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.500 | 0.433 | -0.067 |
| Macro F1 | 0.405 | 0.349 | -0.055 |
| F1 — `Build Help` | 0.519 | 0.541 | +0.022 |
| F1 — `Discussion` | 0.000 | 0.308 | +0.308 |
| F1 — `Troubleshooting` | 0.696 | 0.200 | -0.496 |

**What I predicted before I looked:**
I predict that that the trained model will have higher accuracy for all three labels (`Build help`, `Discussion`, `Troubleshooting`).

**What the gap actually means:**
Suprisingly, the trained model had worse accuracy and F1 scores compared to the baseline. Looking at the labels, the trained model was slightly better at `Build Help` (only a 2% increase) and significantly better at `Discussion` (~30% increase). However, the trained model performed much worse at `Troubleshooting` (~50% decrease). This is likely due to mislabeled training data. 



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
