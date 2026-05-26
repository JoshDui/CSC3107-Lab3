# Coder Log

Project: CSC3107 Week 04 Lab - Exploring ggplot2 with Pygoscelis Penguins  
Role: Coder  
Date: 2026-05-26  
Main project files touched by coder work: `team-steelblue-penguins-lab.qmd`, `ai_log.md`, rendered HTML, submission ZIP  

This is my rough working record as the Coder using an AI chat tool while doing the assignment. It is not a verbatim AI transcript. The fuller AI interaction record is in `ai_log.md`. This file is more about what I asked, what I accepted or rejected, and what I manually checked in R/Quarto before trusting anything.

## Short Summary

| Time | Coder activity with AI tool | Result |
|---|---|---|
| 08:40-09:00 | Asked for a lab structure and package setup | Used the outline, corrected package assumptions |
| 09:00-09:25 | Asked for ggplot code patterns for histograms and point plots | Used some code, edited labels/captions manually |
| 09:25-09:45 | Asked AI to help compare jitter and beeswarm plots | Rewrote the explanation after checking plots |
| 09:45-10:05 | Asked for verification checks and interpretation help | Accepted numeric check ideas, verified in R |
| 10:05-10:25 | Asked for Quarto/render/package cleanup checklist | Rendered HTML, updated `ai_log.md`, rebuilt ZIP |
| Later cleanup | Asked how to make coder log focus on Coder-to-AI usage | Rewrote this file as coder-to-AI working notes |

## Working Log

### 08:40-09:00 - Initial setup and QMD skeleton

- Coder prompt summary: asked the AI chat tool how to organise a CSC3107 Week 04 penguins lab Quarto file, including setup, plots, explanations, AI-use reflection, and output files.
- AI response summary: suggested splitting the QMD into sections for package loading, data cleaning, visualisation tasks, interpretation, and reflection.
- Accepted:
  - Section-based QMD structure.
  - Keeping plot code chunks labelled clearly.
  - Using `tidyverse` for data wrangling and plotting.
- Rejected/changed:
  - AI first treated `penguins` like it would just exist after loading tidyverse. I corrected this because the dataset comes from `palmerpenguins`.
  - I added `palmerpenguins` explicitly and made the QMD wording explain that it supplies the dataset.
- Manual check:
  - Ran the setup chunk in R/Quarto and confirmed `penguins` was available only after loading `palmerpenguins`.
  - Checked the QMD file name stayed as `team-steelblue-penguins-lab.qmd`.

### 09:00-09:25 - Cleaning and first bill length plots

- Coder prompt summary: asked AI for tidyverse code to create the cleaned bill dataset and plot bill length distributions.
- AI response summary: gave a `select()`/`drop_na()` style workflow and basic `ggplot()` histogram examples.
- Accepted:
  - Creating a smaller bill dataset with species, bill length, and bill depth.
  - Using `drop_na()` after selecting the bill variables.
  - Trying a few histogram bin widths to compare how shape changes.
- Rejected/changed:
  - I did not use any overcomplicated helper functions AI suggested. The lab only needed readable ggplot code.
  - I changed labels to include units in mm and added captions referring to the penguins data source.
- Manual check:
  - Ran row-count checks in R after cleaning.
  - Confirmed the cleaned bill dataset had 342 rows.
  - Checked bill length range was 32.1 to 59.6 mm.
  - Rendered partway through because Quarto errors are easier to catch early.

### 09:25-09:45 - Jitter vs beeswarm plots

- Coder prompt summary: asked AI to help write the raw point, jitter, and beeswarm plot section for bill length by species.
- AI response summary: suggested `geom_point()`, `geom_jitter()`, and `geom_beeswarm()` with a short explanation that beeswarm reduces overlap.
- Accepted:
  - Used `geom_jitter()` for the jitter version.
  - Used `geom_beeswarm()` from `ggbeeswarm` for the beeswarm version.
  - Kept the idea that raw points hide repeated/overlapping values.
- Rejected/changed:
  - The AI explanation was too neat and generic at first. It sounded like "beeswarm is better" without enough evidence from the plot.
  - I rewrote it to say jitter is simple and built into ggplot2, while beeswarm shows overlap and density more systematically but can look busier and needs `ggbeeswarm`.
  - Added that jitter can imply artificial vertical movement even though the y-values were only being spread for display.
- Manual check:
  - Viewed the plots in the rendered HTML and compared whether the text matched what was visible.
  - Checked the expanded jitter vs beeswarm paragraph after feedback because the first version was too short.

### 09:45-10:05 - Scatter plots, checks, and interpretation

- Coder prompt summary: asked AI what checks should support the scatter plot interpretation for bill length vs bill depth.
- AI response summary: suggested row counts, species means, duplicate/overlap checks, and correlations by species versus pooled.
- Accepted:
  - Added checks for original row count, cleaned row count, bill ranges, mean table, exact overlap, and correlations.
  - Used the contrast between pooled and grouped correlations in the written interpretation.
  - Mentioned Simpson's paradox carefully when explaining why the pooled trend can mislead.
- Rejected/changed:
  - AI wording initially overclaimed that grouped plots are automatically "better". I changed it to explain that grouping matters because species have different bill shapes.
  - Removed a few phrases that sounded too polished for a student lab report.
- Manual check:
  - Ran the R code that calculated correlations and checked the pooled correlation was negative while species-level correlations were positive.
  - Checked that the plot captions, axes, and units were visible.
  - Made sure the conclusions were tied to the actual plotted data and printed checks, not just AI-written interpretation.

### 10:05-10:25 - AI log, render, ZIP, and push

- Coder prompt summary: asked AI for a final checklist before rendering and packaging the Quarto lab.
- AI response summary: suggested checking required files, captions, AI reflection, render output, ZIP contents, and GitHub push.
- Accepted:
  - Kept `ai_log.md` separate from the QMD reflection.
  - Updated the QMD reflection to describe useful AI help and one correction/incomplete output.
  - Rendered the Quarto file to HTML before packaging.
  - Rebuilt the submission ZIP after the final text updates.
  - Pushed the final project state to GitHub.
- Rejected/changed:
  - Did not treat the checklist as proof by itself. I still checked the rendered HTML output.
  - Did not copy AI reflection text directly. I edited it to match what actually happened in this project.
- Manual check:
  - Rendered `team-steelblue-penguins-lab.qmd` to HTML.
  - Quarto was installed but not available directly on PATH in this shell, so rendering used the full Quarto executable path.
  - Opened/checked the rendered HTML for visible plots, captions, axis units, and the AI-use section.
  - Checked the ZIP included the needed project files, including the QMD and `ai_log.md`.

### Later correction - fixing this coder log

- Coder prompt summary: clarified that `coder_log.md` should record interaction between the Coder and the AI tool, not messages between team roles.
- AI response summary: suggested converting the file into a rough coder-side working log with prompt summaries, AI response summaries, accepted/rejected suggestions, manual verification, and corrections.
- Accepted:
  - Rewrote this log around Coder-to-AI workflow.
  - Kept it rough and dated by work blocks instead of making it a formal report.
  - Added a clear note that this is not a verbatim AI transcript because `ai_log.md` already covers that.
- Rejected/changed:
  - Removed role-to-role communication sections from this file.
  - Avoided claiming exact AI wording unless it is only a summary.

## Corrections Made Because AI Was Incomplete or Too Generic

- Added `palmerpenguins` because the AI initially implied the dataset was available through tidyverse alone.
- Kept the cleaning step focused on bill variables before `drop_na()`, instead of dropping all rows with any missing penguin variable.
- Expanded the jitter vs beeswarm explanation so it discussed what the plots show, not just which function was used.
- Checked correlations manually before accepting the Simpson's paradox explanation.
- Edited AI-written text to sound like a Year 2 CS lab answer rather than a polished article.
- Verified render output in HTML instead of only trusting that the R chunks ran.

## Final Coder Checks

- `team-steelblue-penguins-lab.qmd` used `tidyverse`, `ggbeeswarm`, and `palmerpenguins`.
- Required plots rendered in Quarto HTML.
- Jitter vs beeswarm explanation was expanded after feedback.
- `ai_log.md` was kept as the separate AI-use log.
- Submission ZIP was rebuilt after final edits.
- Project was pushed to GitHub after the render and ZIP rebuild.
