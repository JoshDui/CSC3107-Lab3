# Coder Log

Project: CSC3107 Week 04 Lab - Exploring ggplot2 with Pygoscelis Penguins  
Role: Coder  
Date: 2026-05-26  


1. How should I structure this Quarto .qmd file according to the lab sections?

A clean structure would be to follow the lab requirements section by section, instead of putting all the code in one long block. For example:

---
title: "Steelblue Penguins Lab"
format: html
editor: visual
---

## Setup

```{r}
#| label: setup
#| message: false
#| warning: false

library(tidyverse)
library(palmerpenguins)
Data Preparation
#| label: data-cleaning

penguins_clean <- penguins |>
  filter(!is.na(bill_length_mm), !is.na(bill_depth_mm))
Histograms
Point, Jitter, and Beeswarm Plots
Violin and Box Plots
Scatter Plots
Verifier Checks
Interpretation and Conclusion

This makes the final HTML easier to follow and also makes it clear that each assignment requirement has been addressed.

---
```

## 2. Can you help me create a clean Quarto skeleton for this penguins ggplot lab?

Yes. You can start with this skeleton:

````markdown
---
title: "Penguins Data Visualization Lab"
author: "Team Steelblue Penguins"
format: html
---

## Setup

```{r}
#| label: setup
#| message: false
#| warning: false

library(tidyverse)
library(palmerpenguins)
Data Setup
#| label: data-setup

penguins_clean <- penguins |>
  filter(!is.na(bill_length_mm), !is.na(bill_depth_mm))
Histograms
#| label: bill-length-histogram

# Add histogram code here
Faceted Histograms
#| label: faceted-histogram

# Add faceted histogram code here
Point-Based Plots
#| label: point-plots

# Add raw point, jitter, and beeswarm plots here
Violin and Box Plots
#| label: violin-boxplot

# Add violin + boxplot code here
Scatter Plots
#| label: scatter-plots

# Add pooled, count-symbol, and grouped scatter plots here
Verifier Checks
#| label: verifier-checks

# Add row count, range, duplicate, and correlation checks here
Interpretation

Write your explanation of the plots and findings here.


This gives you the main layout first, then you can fill in each section without losing track of the assignment requirements.

---

## 3. What should the YAML header look like if I need to render the submission to HTML?

For a basic Quarto HTML submission, this is enough:

```yaml
---
title: "Penguins Data Visualization Lab"
author: "Team Steelblue Penguins"
format: html
---
```

If you want a cleaner rendered output, you can use:

```yaml
---
title: "Penguins Data Visualization Lab"
author: "Team Steelblue Penguins"
format:
  html:
    toc: true
    number-sections: true
    theme: cosmo
---
```

The `toc: true` option adds a table of contents, and `number-sections: true` makes the report easier to navigate.

---

## 4. How do I label R chunks properly so each plot/check is easy to identify?

In Quarto, you can label chunks using `#| label:` inside the chunk. For example:

````markdown
```{r}
#| label: bill-length-histogram

ggplot(penguins_clean, aes(x = bill_length_mm)) +
  geom_histogram()
```

Use clear labels such as:

#| label: setup
#| label: data-cleaning
#| label: bill-length-histogram
#| label: bill-depth-histogram
#| label: faceted-histogram
#| label: jitter-plot
#| label: beeswarm-plot
#| label: violin-boxplot
#| label: grouped-scatter-regression
#| label: verifier-checks

Avoid vague labels like chunk1, plot2, or test, because they make debugging harder when Quarto gives an error.

5. How do I hide package messages and warnings in the rendered Quarto HTML?

You can hide messages and warnings in the setup chunk:

```{r}
#| label: setup
#| message: false
#| warning: false

library(tidyverse)
library(palmerpenguins)
```

You can also apply this globally in the setup chunk:

knitr::opts_chunk$set(
  message = FALSE,
  warning = FALSE
)

Then your rendered HTML will look cleaner because it will not show package startup messages.

6. Why does penguins return “object not found” after I load tidyverse?

Because penguins is not automatically loaded by tidyverse. The dataset comes from the palmerpenguins package.

So this will not work by itself:

library(tidyverse)

penguins

You need:

library(tidyverse)
library(palmerpenguins)

penguins

The confusion is understandable because many examples use penguins together with tidyverse, but the actual dataset is from palmerpenguins.

7. Is the penguins dataset part of tidyverse, or does it come from another package?

It comes from the palmerpenguins package, not from tidyverse.

You can load it like this:

library(palmerpenguins)

penguins

You can still use tidyverse for data manipulation and plotting:

library(tidyverse)
library(palmerpenguins)

So the clean explanation is:

The penguins dataset is provided by the palmerpenguins package. The tidyverse package is used for data manipulation and plotting, but it does not contain the dataset itself.

8. How do I load the penguins dataset correctly using palmerpenguins?

Use:

library(palmerpenguins)

data(penguins)

Or simply:

library(palmerpenguins)

penguins

A full setup chunk could look like this:

```{r}
#| label: setup
#| message: false
#| warning: false

library(tidyverse)
library(palmerpenguins)
```

Then you can create your cleaned dataset:

penguins_clean <- penguins |>
  filter(!is.na(bill_length_mm), !is.na(bill_depth_mm))
9. Since palmerpenguins is outside the core package list, how should I explain why I used it?

You can write something like this in the report:

The palmerpenguins package was used only to access the penguins dataset required for this lab. The main data manipulation and visualisation work was completed using the permitted tidyverse tools, especially dplyr and ggplot2.

A slightly more formal version:

Although palmerpenguins is outside the core package list, it is necessary because the penguins dataset is not included in tidyverse. Therefore, palmerpenguins was loaded only as the data source, while the analysis and plotting were carried out using the required packages.

This makes it clear that you are not using extra packages to avoid the assignment requirements. You are only using it because the dataset itself lives there.

10. How do I create a cleaned penguins dataset by removing rows with missing bill length or bill depth?

You can use filter() with !is.na():

penguins_clean <- penguins |>
  filter(
    !is.na(bill_length_mm),
    !is.na(bill_depth_mm)
  )

If your plots also depend on species, it is safer to include that too:

penguins_clean <- penguins |>
  filter(
    !is.na(species),
    !is.na(bill_length_mm),
    !is.na(bill_depth_mm)
  )

You can check the row count before and after cleaning:

nrow(penguins)
nrow(penguins_clean)

11. How do I make a ggplot histogram for bill length?

You can make a basic bill length histogram using geom_histogram():

ggplot(penguins_clean, aes(x = bill_length_mm)) +
  geom_histogram(binwidth = 2, colour = "black", fill = "steelblue") +
  labs(
    title = "Distribution of Penguin Bill Length",
    x = "Bill Length (mm)",
    y = "Count"
  )

The important part is:

aes(x = bill_length_mm)

because a histogram only needs one continuous variable on the x-axis. The y-axis is automatically counted by ggplot.

12. How do I make a ggplot histogram for bill depth?

It is almost the same as the bill length histogram, but you change the x-variable to bill_depth_mm:

ggplot(penguins_clean, aes(x = bill_depth_mm)) +
  geom_histogram(binwidth = 0.5, colour = "black", fill = "steelblue") +
  labs(
    title = "Distribution of Penguin Bill Depth",
    x = "Bill Depth (mm)",
    y = "Count"
  )

The binwidth = 0.5 means each bar covers a bill depth interval of 0.5 mm. You can adjust the bin width if the plot looks too rough or too detailed.

13. How do I facet the bill length histogram by species?

Use facet_wrap():

ggplot(penguins_clean, aes(x = bill_length_mm)) +
  geom_histogram(binwidth = 2, colour = "black", fill = "steelblue") +
  facet_wrap(~ species) +
  labs(
    title = "Bill Length Distribution by Species",
    x = "Bill Length (mm)",
    y = "Count"
  )

This creates one histogram for each species. It is useful because the pooled histogram mixes all species together, while the faceted version shows whether each species has its own distribution.

14. How do I interpret why the pooled bill length histogram has a structured or multi-peaked shape?

The pooled bill length histogram can look structured or multi-peaked because it combines different penguin species into one plot. Each species has a different typical bill length, so the overall distribution is not from one single group.

You could write:

The pooled bill length histogram appears structured because it combines penguins from multiple species. Since Adelie, Chinstrap, and Gentoo penguins have different typical bill lengths, their distributions overlap but are not identical. This creates visible peaks or clusters in the overall histogram.

The main point is that the shape is caused by group differences hidden inside the pooled data.

15. How do I create a raw point plot comparing bill measurements across species?

A raw point plot can be made using geom_point() with species on the x-axis and bill length on the y-axis:

ggplot(penguins_clean, aes(x = species, y = bill_length_mm)) +
  geom_point() +
  labs(
    title = "Bill Length by Species",
    x = "Species",
    y = "Bill Length (mm)"
  )

However, this plot may hide overlapping points because many penguins can have similar or identical values. That is why jitter or beeswarm plots are often better for showing individual observations.

16. How do I create a jitter plot in ggplot, and when is it better than a raw point plot?

Use geom_jitter():

ggplot(penguins_clean, aes(x = species, y = bill_length_mm)) +
  geom_jitter(width = 0.2, height = 0) +
  labs(
    title = "Jitter Plot of Bill Length by Species",
    x = "Species",
    y = "Bill Length (mm)"
  )

A jitter plot is better than a raw point plot when many points overlap. It adds a small amount of random horizontal movement, making individual observations easier to see.

You could explain it like this:

The jitter plot improves on the raw point plot by reducing overplotting. Since many penguins have similar bill length values, the raw points can overlap and hide the number of observations. Jitter spreads the points slightly so the density of observations is easier to see.

17. How do I create a beeswarm plot for this dataset?

A beeswarm-style plot can be created using the ggbeeswarm package:

library(ggbeeswarm)

ggplot(penguins_clean, aes(x = species, y = bill_length_mm)) +
  geom_beeswarm() +
  labs(
    title = "Beeswarm Plot of Bill Length by Species",
    x = "Species",
    y = "Bill Length (mm)"
  )

If the assignment does not allow extra packages besides the required ones, you may need to explain that ggbeeswarm is used only for this specific visualization. Alternatively, if extra packages are not allowed, you can use jitter as a simpler replacement.

18. What is the difference between jitter and beeswarm, and what are the tradeoffs?

A jitter plot randomly spreads points sideways to reduce overlap. It is simple and easy to make, but because the spreading is random, the exact position of each point does not carry much meaning.

A beeswarm plot also spreads points sideways, but it does so in a more controlled way to avoid overlap. This makes the distribution easier to read, but it may require an extra package like ggbeeswarm.

You could write:

Jitter plots are simple and effective for reducing overlap, but the horizontal placement is random and can slightly distort how the data appears. Beeswarm plots arrange points more systematically so that overlapping observations are shown more clearly. However, beeswarm plots may require an additional package and can look more crowded when there are many observations.

So, in simple terms:

Raw point plot: simple, but overlap is hidden.
Jitter plot: reduces overlap randomly.
Beeswarm plot: reduces overlap more systematically.
19. How do I overlay a boxplot on a violin plot in ggplot?

You can use geom_violin() first, then add geom_boxplot() on top:

ggplot(penguins_clean, aes(x = species, y = bill_length_mm)) +
  geom_violin(fill = "steelblue", alpha = 0.5) +
  geom_boxplot(width = 0.15, outlier.shape = NA) +
  labs(
    title = "Violin and Boxplot of Bill Length by Species",
    x = "Species",
    y = "Bill Length (mm)"
  )

The violin plot shows the overall distribution shape, while the boxplot shows the median and spread more clearly.

The width = 0.15 makes the boxplot narrow so it fits neatly inside the violin plot.

20. How do I explain why a violin plot plus boxplot is useful?

You can explain it like this:

A violin plot is useful because it shows the full distribution shape of bill length for each species, including where values are more concentrated. However, it can be harder to identify exact summary statistics from the violin alone. Adding a boxplot helps by showing the median, interquartile range, and possible outliers. Together, the violin and boxplot give both the distribution shape and the key summary statistics.

A shorter version:

The violin plot shows the shape and density of the data, while the boxplot shows the median and spread. Combining them gives a clearer comparison between species than using either plot alone.

This is a good interpretation because it explains why the plot is useful, not just what code was used.

21. How do I create a pooled scatter plot of bill length against bill depth?

A pooled scatter plot means you plot all penguins together without separating them by species.

ggplot(penguins_clean, aes(x = bill_length_mm, y = bill_depth_mm)) +
  geom_point() +
  labs(
    title = "Pooled Scatter Plot of Bill Length and Bill Depth",
    x = "Bill Length (mm)",
    y = "Bill Depth (mm)"
  )

This shows the overall relationship between bill length and bill depth across the whole cleaned dataset.

However, because all species are combined, the plot may hide species-level patterns. That is why it is useful to compare this pooled plot with a grouped scatter plot later.

22. How do I create a scatter plot where repeated coordinate points are represented by count symbols?

You can use geom_count(). It automatically makes larger points when multiple observations share the same x and y coordinates.

ggplot(penguins_clean, aes(x = bill_length_mm, y = bill_depth_mm)) +
  geom_count() +
  labs(
    title = "Count Plot of Bill Length and Bill Depth",
    x = "Bill Length (mm)",
    y = "Bill Depth (mm)",
    size = "Count"
  )

This is useful because normal scatter plots can hide overlapping points. If two or more penguins have the same bill length and bill depth, they may appear as only one point. geom_count() helps reveal that hidden overlap.

23. How do I create a grouped scatter plot by species with separate regression lines?

You can map species to colour, then use geom_smooth(method = "lm"):

ggplot(penguins_clean, aes(
  x = bill_length_mm,
  y = bill_depth_mm,
  colour = species
)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE) +
  labs(
    title = "Bill Length and Bill Depth by Species",
    x = "Bill Length (mm)",
    y = "Bill Depth (mm)",
    colour = "Species"
  )

Because colour = species is inside aes(), ggplot automatically fits separate regression lines for each species.

If you placed colour = species only inside geom_point(), the points would be coloured, but the regression line might still be pooled. So it is cleaner to put it in the main ggplot() mapping.

24. How do I check the original number of rows in the penguins dataset?

Use nrow():

nrow(penguins)

You can also put it into a small tibble for cleaner report output:

tibble(
  dataset = "Original penguins dataset",
  row_count = nrow(penguins)
)

This is useful for your verifier checks because it confirms the dataset size before cleaning.

25. How do I check the row count after cleaning missing values?

If your cleaned dataset is called penguins_clean, use:

nrow(penguins_clean)

For a cleaner comparison:

tibble(
  dataset = c("Original", "Cleaned"),
  row_count = c(nrow(penguins), nrow(penguins_clean))
)

This shows how many rows were removed during cleaning.

If your cleaning removed rows with missing bill length and bill depth, the cleaned dataset should have fewer rows than the original dataset.

26. How do I calculate the range of bill length values?

Use range():

range(penguins_clean$bill_length_mm)

This returns the minimum and maximum bill length.

If you want it in a cleaner table:

penguins_clean |>
  summarise(
    min_bill_length = min(bill_length_mm),
    max_bill_length = max(bill_length_mm),
    bill_length_range = max(bill_length_mm) - min(bill_length_mm)
  )

This gives you the minimum, maximum, and actual range difference.

27. How do I calculate mean bill length and bill depth by species?

Use group_by() and summarise():

penguins_clean |>
  group_by(species) |>
  summarise(
    mean_bill_length = mean(bill_length_mm),
    mean_bill_depth = mean(bill_depth_mm),
    .groups = "drop"
  )

This calculates the average bill length and bill depth for each penguin species.

You can also round the values for cleaner output:

penguins_clean |>
  group_by(species) |>
  summarise(
    mean_bill_length = round(mean(bill_length_mm), 2),
    mean_bill_depth = round(mean(bill_depth_mm), 2),
    .groups = "drop"
  )

This is useful because the species means help explain why the pooled plots look structured.

28. How do I find exact duplicate bill length and bill depth coordinate pairs?

You can group by both coordinates and count how many times each pair appears:

duplicate_coords <- penguins_clean |>
  group_by(bill_length_mm, bill_depth_mm) |>
  summarise(
    count = n(),
    .groups = "drop"
  ) |>
  filter(count > 1)

duplicate_coords

This shows coordinate pairs where more than one penguin has the same bill length and bill depth.

If you want the number of duplicate coordinate pairs:

nrow(duplicate_coords)

If you want the number of hidden overlapping observations:

duplicate_coords |>
  summarise(hidden_overlap_count = sum(count - 1))

The idea is that if a coordinate pair appears 3 times, a normal scatter plot shows only 1 visible point, so there are 2 hidden overlapping observations.

29. How do I calculate pooled correlation and species-level correlations between bill length and bill depth?

For the pooled correlation:

cor(
  penguins_clean$bill_length_mm,
  penguins_clean$bill_depth_mm
)

This gives the overall correlation across all species combined.

For species-level correlations:

penguins_clean |>
  group_by(species) |>
  summarise(
    correlation = cor(bill_length_mm, bill_depth_mm),
    .groups = "drop"
  )

This calculates the correlation separately for each species.

The important part is to compare the pooled correlation with the grouped correlations. If the pooled result suggests one relationship, but the species-level results suggest a different relationship, that supports the Simpson’s paradox explanation.

30. How do I explain Simpson’s paradox in the grouped scatter plot without making the report sound like it is just code output?

You can write something like this:

The pooled scatter plot suggests a different relationship between bill length and bill depth compared to the species-level scatter plot. When all penguins are combined, the overall trend is affected by differences between species. However, when the data is separated by species, the relationship within each species becomes clearer. This is an example of Simpson’s paradox, where the trend in the combined dataset differs from the trends observed within individual groups.

A stronger version:

The grouped scatter plot shows that species is an important hidden variable. In the pooled plot, the relationship between bill length and bill depth appears to follow an overall trend across all penguins. However, this pooled relationship is partly caused by mixing species with different typical bill measurements. Once the data is grouped by species, the within-species regression lines show a different pattern. This demonstrates Simpson’s paradox because the overall trend does not accurately represent the relationships within the individual species groups.

A shorter student-style version:

This plot demonstrates Simpson’s paradox because the combined data gives a misleading impression of the relationship between bill length and bill depth. After separating the data by species, each species shows its own trend, which differs from the pooled trend. This shows why grouping variables should be considered before interpreting an overall correlation.

That is probably the best final interpretation because it explains the chart, mentions the hidden grouping variable, and avoids sounding like you only copied code output.