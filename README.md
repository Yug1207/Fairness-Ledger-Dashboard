# The Fairness Ledger

An interactive dashboard for the Safewater Lines employee engagement survey. It shows where people are proud, where they feel treated unfairly, and who is most likely to leave.

Built as a TISS live industry project, *From Employee Voices to Organisational Impact*.

## View the dashboard

Download `index.html` and open it in any browser. It works offline and needs no setup.

## What it does

The notebook reads the survey responses from one Excel sheet, scores every answer, and writes that HTML file.

- A landing balance that weighs pride against fairness, switchable to settled against unsettled answers
- A ranked overview of the six survey areas
- Five charts, each with its own filters (department, tenure, location, gender)

## The five charts

| Chart | Question it answers |
|---|---|
| 1. Retention grid | Who is proud but not fairly treated, and who plans to stay? |
| 2. Department averages | Is low fairness spread out, or concentrated in particular teams? |
| 3. Tenure lines | How do pride and fairness change with years of service? |
| 4. Comment themes | What do people who feel unfairly treated ask for? |
| 5. Priority map | Which survey questions should be settled first? |

## Rebuild it from the survey data

```bash
pip install pandas numpy scipy openpyxl plotly
```

1. Open `fairness_ledger_dashboard.ipynb` in Jupyter.
2. In Cell 1, set `SOURCE_FILE` to the path of your Excel file. On Windows, keep the `r` before the quotes.
3. Run all cells (Kernel > Restart & Run All).

The last cell rewrites `fairness_ledger_dashboard.html` and opens it in your browser.

Plotly is only used to embed its JavaScript, so the page works offline. Fonts are embedded when the notebook has internet access. Without it, the page falls back to system fonts.

## Input data

The survey workbook is not included in this repository. The notebook expects a sheet named `SWL - MASTERDATA`:

- Row 1 holds section banners, row 2 holds the question titles
- Columns 1 to 6: location, designation, department, years of service, gender, optional name
- Columns 7 to 36: 30 rated questions
- Columns 37 to 43: 7 open comment questions

## How the numbers are built

1. Each answer becomes a score from 1 to 5: always or almost always = 5, often or usually = 4, sometimes = 3, rarely = 2, almost never = 1. The notebook stops with an error if an answer does not match.
2. Questions are grouped into six areas, following the survey's own sections: credibility, respect, fairness, pride, camaraderie and overall experience. "Intend to stay" and "would recommend" are kept apart as outcomes, so no area score contains the result it is compared with.
3. A person's area score is the average of their answers. The area score shown is the average across people.
4. A fairness answer of often or always is "settled". Sometimes or worse is "debt".
5. "Proud" means a pride score of 4.3 or more. "Fairly treated" means a fairness score of 4.0 or more. Both cut-offs are judgement calls.
6. Years of service are merged into equal five-year groups: 0-5, 5-10, 10-15 and 15+.
7. Comments are tagged into themes by keyword matching. Each person counts once per theme.
8. Names are dropped before any analysis.
9. Charts 2 to 4 highlight a gap only when a statistical check says it is larger than chance.

## Data note

The HTML file contains each respondent's scores along with their department, tenure, location and gender, so keep this repository private. It contains no names and no comment text.

## Repository contents

```
fairness_ledger_dashboard.ipynb   builds the dashboard from the survey workbook
fairness_ledger_dashboard.html    the finished dashboard, open in a browser
README.md
```

## Context

TISS Mumbai, BS in Analytics and Sustainability Studies
