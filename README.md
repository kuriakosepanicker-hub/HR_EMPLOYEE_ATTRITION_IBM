# IBM Attrition Analysis
**In one sentence:** this project looks at data on 1,470 employees to figure out *why* people quit their jobs, using simple charts instead of complicated math.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

* This data comes from a study IBM did about their own employees.
* **How big is it?** 1,470 employees, and 35 pieces of information about each one in the original file (32 in the cleaned version we actually work with) — things like age, pay, and whether they work extra hours.
* **What file is it?** A `.csv` file — basically a big spreadsheet saved as plain text. Small and quick to open.
* **The most important column:** `Attrition_Encoded`. It's just a **1** if that employee quit, or a **0** if they're still working there. Almost everything in this project is really just asking: *"which other columns tend to be different between the 1s and the 0s?"*

## Business Requirements

The company (HR) is worried too many people are quitting. That costs money and hurts the team. So they asked us to look into 3 big questions:

### Question 1: Is work too stressful?
Are people quitting because the job is exhausting or makes them unhappy?
* We check this using: **Overtime** (Hypothesis 1), **Job Satisfaction** (Hypothesis 3), and **Work-Life Balance** (Hypothesis 5).

### Question 2: Is it about money and getting promoted?
Are people quitting because they feel underpaid, or like they're never going to move up?
* We check this using: **Monthly Income** (Hypothesis 2) and **Years at the Company** (Hypothesis 4).

### Question 3: Which employees are most likely to quit?
If HR could only watch out for one type of employee, who should it be?
* We check this using: **Age** (Hypothesis 6).


## Hypothesis and how to validate?

A "hypothesis" is just a fancy word for **a guess you can check with data.**

| # | Our guess, in plain words | What we looked at | Were we right? |
|---|---|---|---|
| H1 | People who work overtime quit more | Bar chart comparing quit-rates | **Yes** — overtime workers quit 3x as often (30.5% vs 10.4%) |
| H2 | People paid less quit more | Box plot comparing salaries | **Yes** — people who quit earned less ($3,202 vs $5,204 typically) |
| H3 | Unhappier people quit more | Stacked bar chart | **Yes**, a bit — happier people quit less often, but the gap is smaller than H1 or H2 |
| H4 | People quit mostly in their first few years | Histogram (a shape chart) | **Yes** — most quitting happens in the first 1-3 years, not later |
| H5 | People with a bad work-life balance quit more | Bar chart | **Yes** — the worst-balance group quits about 2x as often as everyone else |
| H6 | Younger people quit more than older people | Box plot comparing ages | **Yes**, a little — younger employees quit somewhat more, but it's the smallest effect of all six |

**In one sentence:** if HR can only fix one or two things, fixing overtime and work-life balance would matter the most.

## Project Plan

1. **Load the data** and just look at it — how many rows, what columns, anything obviously broken?
2. **Check for problems** — missing values? Duplicate employees? Columns where every single row has the exact same value (which tells us nothing useful, so we can throw them away)?
3. **Clean it up** — remove the useless columns, and make sure "did they quit" is stored as a simple 1/0 (`Attrition_Encoded`) so it's easy to do math with later. No separate Yes/No text column is kept.
4. **Save the clean version** — so we don't have to redo the cleaning every time.
5. **Test each hypothesis one at a time** — for each guess, split people into groups, count what % of each group quit, and draw the simplest chart that shows the difference.
6. **Rank the guesses and write up what we found**, in plain English, connecting it back to the 3 big business questions.

We only ever compared two things at a time (like "overtime vs. quitting") because that keeps every chart answerable in one sentence. A more advanced approach — checking several things together at once — is listed as a future step rather than attempted here.


## The rationale to map the business requirements to the Data Visualisations

| Business Question | Charts used | Why this chart made sense |
|---|---|---|
| Q1 — Stress | Bar chart, stacked bar chart | We just needed one or two percentages per group — bars are the simplest way to show "how tall is this group's number" |
| Q2 — Money/promotion | Box plot, histogram | Salaries and years-at-company aren't single numbers, they're a big spread of different values per person — these charts show the whole spread, not just one average |
| Q3 — Who's at risk 

## Analysis techniques used

* **Counting and percentages** — splitting employees into groups (like "overtime" vs. "no overtime") and working out what % of each group quit. No complicated formulas, just counting.
* **Typical value and spread** — for number-heavy columns like income or age, we looked at the middle value (median) and how spread out the numbers were, using box plots.
* **A shortcut scan (correlation heatmap)** — instead of checking each of the ~25 number columns one at a time, this one chart checks all of them against quitting in a single glance.
* **Turning different units into one shared scale** — since "percent," "dollars," and "years" can't be compared directly, every result was converted into "how much bigger, relatively" so all six guesses could be ranked fairly against each other.

**Where this could be wrong (limitations):** this is a snapshot of one company at one point in time — a small dataset (1,470 people) — so what's true here might not be true everywhere. We only ever compared two things at a time; we never checked whether, say, overtime *and* low pay *together* make things even worse — that would need a more advanced technique, and is left as a next step rather than something we tackled here, since this project's scope is visualisation, not building a prediction model. Also, finding that two things happen together (like overtime and quitting) doesn't prove one *causes* the other.

**Where AI helped:** an AI assistant (Copilot) was used throughout — to help plan out the 6 hypotheses, to help pick the right chart type for each one, to help turn different units into one shared comparison scale, and to help spot that Hypothesis 4 could fit under a different business question than first assumed.

## Ethical considerations (optional)

* Feel free to delete this section if this is a data visualisation only (unit 1 or 2) project submission.
* Were there any data privacy, bias or fairness issues with the data?
* How did you overcome any legal or societal issues?

## Dashboard Design (optional)

* Feel free to delete this section if this is a data visualisation only (unit 1 or 2) project submission.
* List all dashboard pages and their content, either blocks of information or widgets, like buttons, checkboxes, images, or any other item that your dashboard library supports.
* Later, during project development, you may revisit your dashboard plan to update a feature (for example, at the beginning of the project, you were confident you would use a given plot to display an insight, but later you used another plot type).
* How were data insights communicated to technical and non-technical audiences?
* Explain how the dashboard was designed to communicate complex data insights to different audiences. 

## Unfixed Bugs

* No real bugs are left unfixed. One early hiccup: an early version of the cleaned data file was missing the `WorkLifeBalance` column entirely, which meant Hypothesis 5's chart couldn't be made. This was caught by checking the column list before building the charts, and fixed by re-saving the cleaned file with that column kept in.
* A harmless warning message sometimes appears when relabeling chart tick marks from 0/1 to "No"/"Yes" (a `UserWarning` from the charting library). It doesn't change what the chart looks like, so it was left alone rather than "fixed" for no real benefit.

## Development Roadmap

* **Getting stuck on:** which chart to use for which hypothesis. **Fixed by:** working out one simple rule — percentages get a bar chart, spreads of numbers get a box plot or histogram.
* **Getting stuck on:** comparing hypotheses measured in totally different units (dollars vs. percent vs. years). **Fixed by:** converting every result into "% bigger than the other group," so they could all be ranked on the same scale.
* **Getting stuck on:** deciding which business question Hypothesis 4 really belonged to. **Fixed by:** just writing down the honest disagreement instead of quietly picking one answer.

## Main Data Analysis Libraries

* **pandas** — used for splitting employees into groups and counting/averaging within each group. Example: `df.groupby("OverTime")["Attrition_Encoded"].mean() * 100` gives the % who quit, per overtime group.
* **matplotlib** and **seaborn** — used for actually drawing the bars, boxes, and lines you see in the charts.

Nothing more advanced than that was needed — no complicated statistics formulas, just counting, percentages, and pictures.

### Content 

- The business questions and hypotheses were adapted from the Code Institute assessment brief.
- This README follows the structure of the [Code Institute da-README-template](https://github.com/Code-Institute-Solutions/da-README-template).
- Dataset: IBM HR Analytics Employee Attrition & Performance dataset (publicly available, e.g. on Kaggle).

## Acknowledgements (optional)

* - Special Thanks to Vasi, Lori, Niel and Michael (Tutors) and my colleagues for the support.