# Constructive Critic + Reporter Notes

Project: Week 04 Lab, Exploring ggplot2 with Pygoscelis Penguins

Use these as short report-ready notes for the final QMD/HTML. The tone should stay clear and student-like: explain what the plot shows, then explain why that matters.

## Draft explanatory text

### Ungrouped bill length histogram

The ungrouped bill length histogram does not look like one simple unimodal distribution. It has visible structure, such as shoulders or more than one high-density region, because the plot is pooling penguins from different species into one group. Adelie penguins usually have shorter bills, while Chinstrap and Gentoo penguins tend to have longer bills, so combining them creates a mixed distribution. This means the histogram is useful as a first check, but it hides the species groups that are probably causing the pattern.

### Jitter vs beeswarm

Jitter is useful because it quickly spreads overlapping points so we can see individual observations instead of one dark stack of points. The downside is that the spreading is random and artificial, so the exact horizontal position should not be interpreted as a real value. A beeswarm plot is usually clearer for grouped numeric data because it avoids overlap while keeping the packing related to the local density of points. The downside is that beeswarm plots can look busy with many observations, and the side-to-side position is still mainly a display method, not an extra variable.

### Violin plus box plot

A violin plot with a box plot overlay is more informative than a box plot alone because it shows both the distribution shape and the summary statistics. The violin shows where values are more common, including skew or multiple clusters, while the box plot shows the median, interquartile range, and possible outliers. For this penguins data, that combination makes it easier to compare species because we can see both the typical bill length and how spread out each species is.

### Bill depth vs bill length species separation

The bill depth vs bill length scatter plot separates the species better than looking at one bill measurement by itself. Adelie penguins tend to sit in the shorter bill length and deeper bill depth region, while Gentoo penguins tend to have longer but shallower bills. Chinstrap penguins usually have longer bills too, but their bill depth helps separate them from Gentoo. There is still some overlap, so the plot should be described as showing strong separation, not perfect classification.

### Pooled vs grouped scatter interpretation

The pooled scatter plot shows the overall relationship across all penguins, but that relationship can be misleading because species differences are mixed together. When the points are coloured or faceted by species, it becomes clearer whether the trend happens inside each species or mostly between species. If the grouped trends look different from the pooled trend, the report should focus on the grouped interpretation because species is an important explanatory variable here.

### Simpson's paradox note

This data is a good place to mention Simpson's paradox or a Simpson's-paradox-like effect. A trend seen in the pooled data can change, weaken, or even reverse after grouping by species, because each species has its own average bill length and bill depth. In this case, Gentoo penguins having relatively long but shallow bills can pull the pooled pattern away from the within-species pattern. The final report should not claim a full paradox unless the plotted trend lines or summary statistics actually show a reversal, but it should warn that pooled correlations can be misleading.

## Final insight summary draft

The penguins dataset shows that bill measurements are strongly linked to species, so grouped plots are more useful than pooled plots. The ungrouped bill length histogram is not clearly unimodal because it combines species with different typical bill lengths. When the data is split by species, Adelie penguins generally have shorter bills, while Chinstrap and Gentoo penguins have longer bills. The bill depth vs bill length scatter plot gives better separation because Gentoo penguins tend to have shallower bills than the other long-billed group. Violin plots with box plot overlays are useful because they show both the distribution shape and the main summary statistics. Overall, the main lesson is that pooling the data can hide important group structure, so the report should interpret trends by species before making general claims.

## Critic checklist for final QMD/HTML

- Check that every required plot is present in both the QMD source and rendered HTML.
- Check that plots have readable titles, axis labels with units where useful, and legends that match the mapped variables.
- Check that the ungrouped histogram explanation mentions hidden species grouping rather than only saying "the data is spread out".
- Check that jitter and beeswarm are compared fairly: jitter is simple and fast, beeswarm shows density/overlap better, both have display-position limitations.
- Check that violin plus box plot is explained as distribution shape plus median/IQR/outliers, not just "it looks nicer".
- Check that bill depth vs bill length is interpreted by species, with wording like "strong separation" instead of "perfect separation".
- Check that pooled scatter comments do not overclaim correlation without looking at grouped trends.
- Check that the Simpson's paradox paragraph is careful: say "possible" or "paradox-like" unless the plot/statistics confirm a reversal.
- Check that plot captions and paragraphs are concise and directly tied to the plot immediately above or below them.
- Check that code chunks have sensible names, do not print unnecessary messages/warnings, and render cleanly.
- Check that any `set.seed()` needed for reproducible jitter is included near the plot code.
- Check that missing values are handled consistently, especially if `drop_na()` or `na.rm = TRUE` is used.
- Check that the HTML is rendered from the latest QMD, not an older output file.
- Check that there are no leftover notes to team members, TODOs, debug output, or copied console errors in the final HTML.

## Likely clarity/style issues to watch

- Avoid saying "the graph proves" when the plot only suggests a pattern.
- Avoid writing long generic descriptions of ggplot2; focus on what this dataset shows.
- Avoid switching terms between "bill length", "culmen length", and "beak length" unless the report defines them.
- Keep species names capitalised consistently: Adelie, Chinstrap, Gentoo.
- Use short paragraphs after each plot instead of one large block at the end.
- Make sure colours and shapes are explained through the legend, not only in the prose.

## Submission ZIP contents check

- Include the final `.qmd` file.
- Include the rendered `.html` file generated from that QMD.
- Include any required supporting folders/files created by Quarto only if the HTML depends on them.
- Do not include `tmp`, `role_logs`, cache folders, draft notes, or unrelated screenshots unless the assignment specifically asks for them.
- Open the zipped HTML once after packaging to confirm the plots still display.
- Check the ZIP filename follows the team/class submission naming rule.
