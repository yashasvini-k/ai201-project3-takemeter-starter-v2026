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

TakeMeter is a text-classification project using posts from the Reddit community r/artificial. The dataset contains 200 posts about AI and technology. The classifier sorts each post into one of three categories: sourced_information, personal_opinion, or unsupported_claim. The project explores whether a text-classification model can learn these distinctions from labeled examples and how well it performs on posts held out from training.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `label_one` sourced_information

**Definition:** Primarily reports information attributed to an external source, such as a linked article, research paper, or cited report.

**Example 1:**
> “I analyzed the 2025 acquisition landscape and was surprised by how manufacturing dominates the M&A market.” The post describes a methodology based on acquisition announcements and sector classifications.

**Example 2:**
> “The first C-SPAN stream is scheduled to start at 9:31 a.m. Eastern ...” The post provides specific event information and includes a news-and-primary-sources section.

### `label_two` personal_opinion

**Definition:** Primarily expresses the author's personal experience, opinion, preference, or prediction.

**Example 1:**
> “Having a mental blank, there was a company recently ... that had a disastrous software update ... Anyone have any idea what I might be thinking of?”

**Example 2:**
> “3 of us started a company together, we're friends. CEO had the idea ... and they approached me to be the CTO and build up the app.”

### `label_three` unsupported_claim

**Definition:** Primarily makes a broad factual claim without a cited source or specific supporting evidence.

**Example 1:**
>  “I’m a Social Media Manager looking for clients and i have already worked with few pages.” The post promotes services but does not provide evidence for its performance claims.

**Example 2:**
> “We help businesses transform complex ideas into simple, user-friendly, and high-converting digital experiences.” The promotional claim is not supported by specific evidence in the excerpt.

### The hardest boundary

**Which two labels:** sourced_information and unsupported_claim

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
If a post reports information and gives a specific, identifiable source or describes a checkable methodology, use sourced_information. If it makes a factual or promotional claim without identifiable evidence, use unsupported_claim. If its main purpose is to share a personal experience or viewpoint, use personal_opinion.
---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** The Reddit community r/artificial. The project uses a dataset of AI- and technology-related posts saved in gold_reddit_raw.csv, with the labeled dataset stored in labels.csv.

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->
I used batch scripts to assign labels and explanatory notes to the 200 posts. The notes describe each post's main purpose or the reason for its assigned category. The current files do not establish that the first 20 posts were independently labeled as cold examples or that the remaining posts were AI-pre-labeled and individually corrected. I have therefore not claimed either workflow without verification.



**Counts per label:**

| Label | Count | Share |
|---|---|---|
| sourced_information | 34 | 17.0% |
| personal_opinion | 139 | 69.5% |
| unsupported_claim | 27 | 13.5% |
| **Total** | 200 | 100% |



**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:* Startup equity discussion
> The author describes a real business arrangement but also shares a personal perspective about equity distribution. 
> *Could have been:*
> The competing labels are personal_opinion and sourced_information.
> *I chose, because:* the post's main purpose is to discuss the author's experience and seek advice.

**2.**
> *The post:* Manufacturing and M&A trend
> The author claims manufacturing dominates acquisition activity and describes a methodology. 
> *Could have been:*
> The competing labels are sourced_information and unsupported_claim.
> *I chose, because:* sourced_information if the full post identifies supporting sources or sufficiently specific, checkable evidence; otherwise, I would choose unsupported_claim.

**3.**
> *The post:* Agency marketing post
> The agency claims it delivers “high-converting digital experiences” and helps businesses “drive growth.”
> *Could have been:*
> The competing labels are unsupported_claim and personal_opinion.
> *I chose, because:* unsupported_claim because these are promotional performance claims without supporting evidence in the excerpt.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:** distilbert-base-uncased
 
**Settings:** <!-- epochs, learning rate, batch size, seed --> 
EPOCHS = 3
LEARNING_RATE = 2e-5
BATCH_SIZE = 16
SEED = 42

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->
train 139  
val 31  
test 30


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* Help troubleshooting the Python scripts and checking the labeled dataset for missing values, duplicates, and label counts.
- *What came back:* Suggested commands for inspecting the CSV files and verifying the dataset.
- *What I changed:* I ran the checks in my local environment and used the outputs to confirm that the dataset contained 200 rows and to identify the label distribution.

**Moment 2**

- *What I asked for:*  Help interpreting the initial model evaluation and understanding why accuracy and per-label F1 scores differed.
- *What came back:* An explanation of the confusion matrix and the fact that the model predicted every test post as personal_opinion.
- *What I changed:* I documented the observed results and identified the need to investigate the label definitions and evaluation setup rather than assuming the accuracy score demonstrated good performance.

**Pre-labelling disclosure:** The available batch scripts assign labels and notes directly, but the current files do not establish whether an AI model pre-labeled the posts. I have not claimed that AI pre-labeling occurred. If AI was used to suggest individual labels before they were reviewed, that workflow should be disclosed accurately here.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure                  | Baseline | Trained | Difference |
|--------------------------|----------|---------|------------|
| Overall accuracy         | 0.333    | 0.700   | +0.367     |
| Macro F1                 | 0.310    | 0.275   | -0.035     |
| F1 — personal_opinion    | 0.414    | 0.824   | +0.410     |
| F1 — sourced_information | 0.267    | 0.000   | -0.267     |
| F1 — unsupported_claim   | 0.250    | 0.000   | -0.250     |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

I did not record a prediction before viewing the trained-model results, so I cannot honestly present a retrospective prediction as a prior one.

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->

The trained model's accuracy increased from 0.333 to 0.700, but its macro F1 decreased from 0.310 to 0.275. It predicted `personal_opinion` for all 30 test posts. It identified the majority class but failed to identify `sourced_information` and `unsupported_claim`. The accuracy increase therefore did not indicate balanced performance across all three labels.

---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|-----------|--------|---------|--------|-----------|---------|
| 1. Overall accuracy | >= 0.60 for all seeds | 0.700 | 0.700 | 0.700 | Meets saved results; verify independent runs |
| 2. F1 for every label | >= 0.45 for all seeds | 0.000 for two labels | 0.000 for two labels | 0.000 for two labels | Missed |
| 3. Label balance | No label above 60% | 69.5% personal_opinion | 69.5% personal_opinion | 69.5% personal_opinion | Missed |
| 4. Second-labeling agreement | >= 27/30 agree | Not measured | Not measured | Not measured | Not yet measured |
| 5. High-confidence accuracy | >= 75% correct at confidence >= 0.80, with >= 20 evaluated | Not verified | Not verified | Not verified | Not yet measured |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted        | sourced_information | personal_opinion | unsupported_claim |
|-------------------------|---------------------|------------------|-------------------|
| **sourced_information** | 0                   | 5                | 0                 |
| **personal_opinion**    | 0                   | 21               | 0                 |
| **unsupported_claim**   | 0                   | 4                | 0                 |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

The largest off-diagonal count is 5: all five posts labeled sourced_information were predicted as personal_opinion. The model also predicted personal_opinion for all four unsupported_claim posts. It therefore failed to distinguish the other two categories from the majority class. Although accuracy was 0.700, the model's macro F1 was only 0.275, showing poor performance across all three labels.

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion                      | Target | Verdict | How I decided |
|---|--------------------------------|--------|---------|---------------|
| 1 | Overall accuracy               | >= 0.60 for all three seeds | Meets saved results; verify independent runs | All three saved entries report 0.700 accuracy, but their identical metrics need verification. |
| 2 | Per-label F1                   | >= 0.45 for every label across all seeds | MISSED | The saved results show F1 of 0.000 for sourced_information and unsupported_claim. |
| 3 | Label balance                  | No label above 60% | MISSED | personal_opinion makes up 69.5% of the 200 labeled posts. |
| 4 | Independent labeling agreement | At least 27/30 matches | NOT YET MEASURED | No completed agreement score has been verified. |
| 5 | High-confidence accuracy       | At least 75% correct at confidence >= 0.80, with at least 20 examples | NOT YET MEASURED | The available summary does not establish the required number of predictions at that confidence threshold. |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

The clearest problem is that the model predicts personal_opinion for every test post. This explains its zero F1 scores for sourced_information and unsupported_claim. The model may be favoring the majority class, but the evaluation alone cannot establish whether the underlying cause is limited training data, inconsistent labels, overlapping definitions, or a model limitation.

The dataset is also imbalanced: 69.5% of its labels are personal_opinion, exceeding the 60% target. An independent agreement review is still needed to help determine whether labeling inconsistencies contribute to the model's poor performance.

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

The agreement script compared my labels against the staff reference labels for all 30 posts. It reported 30 agreements, 0 disagreements, and 100% agreement.

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

I changed the training loss to use class weights calculated from the training-set label frequencies. This gave less frequent labels more weight during training, addressing the concern that the original model was predicting only the majority class, `personal_opinion`.

**Which diagnosis pointed at it:**

The before-results showed that all 30 test posts were predicted as `personal_opinion`, resulting in zero F1 for `sourced_information` and `unsupported_claim`. The label distribution was also imbalanced: 69.5% of the 200 labeled posts were `personal_opinion`. Class-weighted training was an attempt to reduce the model's majority-class bias.

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---:|---:|---:|---|
| 1. Overall accuracy | >= 0.60 for all seeds | 0.733 | 0.600 | 0.200 | MISSED |
| 2. F1 for every label | >= 0.45 for every label across all seeds | 0.444 minimum | 0.000 minimum | 0.000 minimum | MISSED |
| 3. Label balance | No label above 60% | 69.5% personal_opinion | 69.5% personal_opinion | 69.5% personal_opinion | MISSED |
| 4. Independent labeling agreement | At least 27/30 matches | Not measured | Not measured | Not measured | NOT YET MEASURED |
| 5. High-confidence accuracy | >= 75% correct at confidence >= 0.80, with at least 20 examples | Not verified | Not verified | Not verified | NOT YET VERIFIED |


**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->

The results were mixed. Average accuracy decreased from 0.700 before the change to approximately 0.511 across the three after-runs. Average macro F1 increased from approximately 0.275 to 0.402. Seed 42 improved substantially, with accuracy of 0.733 and macro F1 of 0.605, while seed 7 had macro F1 of 0.375 and seed 2024 had macro F1 of 0.225. The change improved average macro F1 but did not reliably improve performance across seeds. The results suggest that class weighting alone is insufficient; more consistent labels, clearer label boundaries, and further evaluation are needed.

---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

The accuracy target was not met across all three seeds after class weighting: seed 2024 reached only 0.200 accuracy. The per-label F1 target also failed because some labels had F1 below 0.45, including zero F1 for `unsupported_claim` in seed 7 and zero F1 for `personal_opinion` in seed 2024. I would next review mislabeled or ambiguous examples, improve the consistency of the label definitions, and test another training configuration. I would not claim the model is reliable until the results improve consistently across seeds.

The label-balance target remains unmet because `personal_opinion` accounts for 69.5% of the dataset. I would collect and manually review additional examples for the two less frequent labels rather than changing labels just to force a balanced distribution.

The independent labeling-agreement and high-confidence criteria are not yet verified. I need a valid independent labeling comparison to calculate agreement, and I need to count predictions with confidence of at least 0.80 and evaluate their correctness. I have not treated either criterion as passed without those measurements.

**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->

Before class weighting, the model predicted `personal_opinion` for every test post, even when the correct label was `sourced_information` or `unsupported_claim`. After class weighting, its performance varied considerably by seed, suggesting that it has not yet learned stable boundaries between all three categories.

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
