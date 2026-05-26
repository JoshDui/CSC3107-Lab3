# Navigator + Verifier Notes

Role: Navigator + Verifier  
Lab: Week 04 Lab, ggplot2 with Pygoscelis penguins  
Scope: notes for the Coder to merge into the canonical QMD

## Assumptions

- I used `palmerpenguins::penguins` as the source data. If the QMD only loads `tidyverse` and `penguins` is not found, add `library(palmerpenguins)` or call `palmerpenguins::penguins` directly.
- For this lab, `penguins_bill` should be made by keeping only `species`, `bill_len`, and `bill_dep`, then using `drop_na()`. Do not run `drop_na()` on the full penguins data first, because that would also remove rows with missing `sex` and gives a different count.

```r
penguins_bill <- palmerpenguins::penguins |>
  transmute(
    species,
    bill_len = bill_length_mm,
    bill_dep = bill_depth_mm
  ) |>
  drop_na()
```

## Navigation Checklist For Coder

- Data prep: show original size of `penguins` as 344 rows and 8 columns.
- Cleaning: confirm `penguins_bill` has 342 rows, so 2 rows were removed.
- Histogram range check: bill length should span 32.1 mm to 59.6 mm. Make sure the histogram does not clip either end.
- Summary table: include mean `bill_len` and mean `bill_dep` by species.
- Exact overplotting: report hidden points and max stack, then mention exact overlap is not the only kind of visual overlap.
- Scatter/regression: report pooled Pearson correlation and per-species correlations. The signs should match the trend lines.
- Final observations: explicitly name Simpson's paradox when explaining why the pooled trend is misleading.
- Source consistency: final conclusion should be consistent with Horst, Hill and Gorman (2022): bill length/depth can separate species fairly well, but not perfectly, and including species reverses the apparent bill length vs bill depth trend.

## Independent Verification Notes

### Cleaned Row Removal Cross-Check

Use `filter()` and `nrow()` to count rows that should be removed because either bill measurement is missing:

```r
palmerpenguins::penguins |>
  filter(is.na(bill_length_mm) | is.na(bill_depth_mm)) |>
  nrow()
# 2
```

Expected result:

- Original data: 344 rows
- Cleaned `penguins_bill`: 342 rows
- Removed rows: 2

If the Coder gets 333 rows, they probably used `drop_na()` on the full dataset before selecting the bill columns. That is not the cleaning described in Section 3.1(c).

### Bill Length Range

For the cleaned bill data:

- Minimum `bill_len`: 32.1 mm
- Maximum `bill_len`: 59.6 mm

The histogram should show the full 32.1 to 59.6 mm range without cutting off either extreme.

### Species Mean Bill Table

Merge-ready table values, rounded to 2 decimals:

| species | n | mean_bill_len | mean_bill_dep |
|---|---:|---:|---:|
| Adelie | 151 | 38.79 | 18.35 |
| Chinstrap | 68 | 48.83 | 18.42 |
| Gentoo | 123 | 47.50 | 14.98 |

This supports the visual interpretation that Gentoo penguins have much shallower bills on average, Chinstrap penguins have the longest bills on average, and Adelie penguins have shorter bills.

### Exact Overlap Check With `distinct()`

The `distinct()` cross-check is:

```r
nrow(penguins_bill) -
  nrow(distinct(penguins_bill, bill_len, bill_dep))
# 4
```

Expected values:

- Total cleaned rows: 342
- Unique `(bill_len, bill_dep)` coordinates: 338
- Hidden points by exact overlap: 4
- Maximum stack at one exact coordinate: 2 rows

Duplicate coordinate pairs found:

| bill_len | bill_dep | n |
|---:|---:|---:|
| 35.0 | 17.9 | 2 |
| 37.9 | 18.6 | 2 |
| 45.1 | 14.5 | 2 |
| 50.5 | 15.9 | 2 |

Short explanation to merge: exact coordinate overlap hides 4 points, but it is not the only cause of overplotting. Points can also visually cover each other when they are close but not exactly equal, because plotted marks have non-zero size.

### Pearson Correlations

Use Pearson correlation with `cor(bill_len, bill_dep)`.

| group | n | Pearson r | sign |
|---|---:|---:|---|
| all species pooled | 342 | -0.23505287 | negative |
| Adelie | 151 | 0.39149169 | positive |
| Chinstrap | 68 | 0.65353621 | positive |
| Gentoo | 123 | 0.64338395 | positive |

The pooled trend should slope downward, but the species-specific trend lines should slope upward. This is the expected Simpson's paradox pattern.

### Consistency With Horst, Hill and Gorman (2022)

The final observations are consistent with Horst, Hill and Gorman (2022) if they say that:

- `penguins` is a real-world dataset with missing values and unequal species counts.
- Bill length and bill depth help distinguish the three species, but the separation is not perfect.
- Ignoring species gives a misleading negative pooled relationship between bill length and bill depth.
- Adding species reveals positive bill length-depth relationships within each species.
- This reversal is Simpson's paradox.

The R Journal paper by Horst, Hill and Gorman (2022), DOI `10.32614/RJ-2022-020`, uses the bill length vs bill depth example in the same way: the overall trend is negative when species is omitted, but positive within species once species is included.
