# Gender Pay Gap Exercise

**Module:** QM1
**Student ID:** 5796695

## Research question

Is there a gender pay gap among large UK employers?

The data have one row per employer, and the variable of interest is that
employer's own mean hourly pay gap in percent. There is no column of men's pay
and women's pay to compare, so this is not an independent-samples test of men
against women. It is a one-sample *t*-test of the employer-level gap against
the 0% that equal average hourly pay would produce.

- **H₀:** in the population of large UK employers, the mean employer-level
  hourly pay gap is zero (μ = 0)
- **H₁:** it is not zero (μ ≠ 0)

Two-tailed, α = .05.

## Data

| | |
|---|---|
| Source | UK Government [gender pay gap service](https://gender-pay-gap.service.gov.uk/viewing/download-data/2025), 2025-26 reporting year |
| File | `UK_gender_pay_gap_2025-26.csv` |
| N | 11,187 employers (all with 250+ staff; reporting is compulsory, so this is close to a census) |
| Outcome | `DiffMeanHourlyPercent`, i.e. (male mean − female mean) / male mean × 100 for hourly pay. Positive = women paid less |
| Grouping (stretch task) | `Sector`, derived from `DueDate`: 31 March 2026 = Public Sector, 5 April 2026 = Business / Charity |

A data dictionary covering all 27 variables is in the replication document.

## Contents

| File | What it is |
|:---|:---|
| `UK_gender_pay_gap_2025-26.csv` | Raw data |
| `gender_pay_gap_exercise.Rmd` | Replication code: raw CSV to every number, table and figure |
| `gender_pay_gap_exercise.html` | The knitted replication document |
| `gender_pay_gap_writeup.Rmd` | Source for the write-up; no visible code, every number generated from the raw data |
| `gender_pay_gap_writeup.docx` | The write-up |
| `makefile` | `make all` rebuilds both outputs |

## Method

One-sample *t*-test of `DiffMeanHourlyPercent` against μ = 0. No employer was
excluded and there were no missing values on the outcome.

For the stretch task I used Welch's two-sample *t*-test to compare sectors,
because the variances are unequal.

Run in R 4.4.1 with `tidyverse`, `lubridate`, `scales`, `knitr`, `rmarkdown`
and `Hmisc`.

```r
rmarkdown::render("gender_pay_gap_exercise.Rmd", "html_document")
rmarkdown::render("gender_pay_gap_writeup.Rmd", "word_document")
```

## Results

Women at large UK employers were paid significantly less per hour than men.
The mean hourly pay gap across employers was 11.50% in women's disfavour
(*SD* = 15.99, *Mdn* = 10.64%), reliably greater than zero,
*t*(11186) = 76.06, *p* < .001, 95% CI [11.20, 11.80], *d* = 0.72. Women were
paid less at 85.01% of employers and more at only 14.43%.

**Stretch task.** Public sector employers reported a larger mean gap
(*M* = 13.35%, *SD* = 10.42, *n* = 1,945) than businesses and charities
(*M* = 11.11%, *SD* = 16.91, *n* = 9,242), a difference of 2.23 percentage
points, Welch's *t*(4413.10) = 7.58, *p* < .001, 95% CI [1.66, 2.81],
*d* = 0.14.

## Interpretation

H₀ is rejected. A typical large UK employer pays women about 11.5 pence less
for every pound it pays men.

On the sector comparison, the large difference in standard deviations comes
from a handful of extreme business and charity returns (the minimum is −757%)
rather than from a generally wider spread, since the interquartile ranges are
very similar (15.81 against 14.40 percentage points). What does differ is how
consistently the gap runs against women: it favours women at 15.76% of
businesses and charities but at only 8.07% of public sector employers. The
standardised effect is small, so the conclusion is that the public sector is
not the better performer, not that it is markedly worse.

## Assumptions and limitations

- **Independence:** one return per employer, so observations are independent.
- **Normality:** the raw distribution is heavy-tailed rather than normal, but
  with *n* = 11,187 the central limit theorem makes the test robust to this.
- **Equal variances:** not relevant to the one-sample test. For the sector
  comparison the variances are clearly unequal, hence Welch's correction.
- **Caveats:**
  - The unit is the employer, so a firm with 250 staff counts as much as one
    with 250,000. This is the mean of employer gaps, not the gap facing the
    average UK worker.
  - A raw pay gap is not unequal pay for equal work. It mixes pay
    discrimination with occupational segregation, i.e. who holds the senior
    and the junior jobs.
  - Figures are self-reported, and only employers with 250+ staff must
    report, so smaller employers are absent entirely.
  - The sector split rests on the reporting deadline, which is a reliable but
    indirect marker of sector.
