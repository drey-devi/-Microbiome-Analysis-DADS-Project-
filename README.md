# -Microbiome-Analysis-DADS-Project-
## Overview

This project analyzes how Diallyl Disulfide (DADS), soil type, and incubation conditions affect soil microbial communities using 16S rRNA sequencing.
We evaluate sequencing depth, apply multiple normalization methods, test three ecological hypotheses using PERMANOVA, and visualize beta diversity via PCoA and CAP.

## Data & Design

24 soil samples

Soils: Madras vs. Tulelake

Treatments: DADS-treated vs. untreated

Incubation: Aerobic vs. Anaerobic

Avg depth: 18,469 reads/sample
(From project slides 

BDS 491_ Group 1

)

## Pipeline Summary
1. Load Data
<pre>```bash arg1  <- readRDS("phyloseq.dads.rds")
soil  <- read.csv("Metadata_diallyldisulfide_exp_16S.csv")```</pre>

2. Normalization
<pre>```bash
RA (Relative Abundance)

RF (Rarefaction)

CSS (Cumulative Sum Scaling)
</pre>
RA showed the tightest clustering → used for hypotheses.

3. Beta Diversity
<pre>```bash
gp.ord <- ordinate(arg1_norm_RA, "PCoA")
plot_ordination(arg1_norm_RA, gp.ord, color="Treatment")```</pre>

5. Statistical Testing
<pre>```bash
PERMANOVA (adonis2)
```</pre>
Bray–Curtis distance

CAP constrained ordination

## Hypotheses & Results
Hypothesis 1 — Soil type influences microbial composition

(Full analysis in Divy PDF 

Hypothesis_1_testing_divy

)

Soil alone: not significant (p = 0.07, R² = 1.5%)

Treatment alone: highly significant (p = 0.001, R² ≈ 72%)

Conclusion: DADS treatment dominates, soil has minimal effect.

Hypothesis 2 — Incubation affects microbial composition

PERMANOVA shows significant incubation effect.

CAP plots separate aerobic vs. anaerobic groups.

Conclusion: Incubation matters, but less strongly than treatment.

Hypothesis 3 — Soil × Treatment × Incubation interaction

Interaction significant in PERMANOVA.

Treatment overrides soil, while incubation modulates within-group structure.

Conclusion: Treatment > Incubation > Soil in effect strength.

Top Taxa Contributors
biplot_df <- plot_ordination(arg1_norm_RA, gp.ord, type="biplot", justDF=TRUE)


Identifies phyla contributing most to observed beta-diversity patterns.

## Reproducibility

Run the main analysis:

quarto render Project_Soil.qmd

## Summary

DADS treatment is the primary driver of community shifts.

Incubation has a secondary but significant effect.

Soil type contributes minimally on its own.

RA normalization provides the clearest ecological signal.
