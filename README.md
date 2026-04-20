README
Overview
This repository contains data and analysis workflows used to assess how arbuscular mycorrhizal fungal (AMF) inoculation alters soil microbial communities in field soil. Community responses were evaluated by comparing:
•	Total community composition (DNA metabarcoding)
•	Putatively active community composition (rRNA-derived data)
The experimental design included factorial treatments of:
•	AMF isolate: Control, CC4, Cuba8, DAOM197198
•	Fertilizer: No, High
•	Tillage: NoTill, Till
•	Harvest time: 2 and 4 months

Dependent factors:
•	Inoculant abundance and establishmnent in root and soil
•	Host biomas (root and shnoot)
•	Host foliar P concentration
•	Soil pH
•	Soil P concentration
•	AMF community response (metabarcoding  and RNA-derived taxonomy) in soil
•	Non-AMF community response (RNA-derived taxonomy) in soil
•	Soil function:

Analyses included:
•	Alpha diversity (Richness, Shannon, Simpson, Evenness)
•	Beta diversity (Bray–Curtis, Jaccard)
•	PERMANOVA and dispersion analyses
•	Mantel and Procrustes comparisons (DNA vs RNA)
•	SIMPER analysis to identify taxa driving compositional shifts

Data Description
Meta data
We performed metatrascriptome sequencing on a subset (n =5) of the samples used for metabacoding (n =5)
•	Meta_data_RNA.csv
Sample metadata including AMF treatment, fertilization, tillage, and harvest time for all RNA analyses
•	Meta_data_metabarcoding.csv
Sample metadata including AMF treatment, fertilization, tillage, and harvest time for all RNA analyses

Primary data files
•	Plant_data.csv
Plant biomass, foliar phosphorus, soil phosphorus, and soil pH for each experimental unit
•	ddpcr_data.csv
ddPCR-derived AMF abundance estimates used to quantify inoculant establishment
•	AMF_metabarcode_ASV_long_4363.csv
DNA metabarcoding dataset (ASV-level), rarefied to 4,363 reads per sample
•	AMF_rna_ASV_long_relative_abundance.csv
RNA-derived AMF dataset represented as within-sample relative abundance
•	summed_phyla_viruses.csv
•	summed_phyla_fungi.csv
•	summed_phyla_protists.csv
•	summed_phyla_prokaryotes.csv
Community composition aggregated at the phylum level for major taxonomic groups

Scripts and Analysis Workflow
1. Inoculant establishment: Quantifies AMF inoculant presence and abundance using ddPCR-derived data.
•	Concentration_AMF
•	PresenceAbsence_AMF

2. RNA preprocessing and taxonomic assignment: RNA-derived sequence data were preprocessed to:
•	filter and format transcriptome-derived features
•	separate AMF and non-AMF taxa
•	assign taxonomy and standardize taxonomic labels
•	AMF_RNA_Feature_Table

3. Resident AMF community responses (DNA metabarcoding): Assesses effects of AMF inoculation, fertilization, and tillage on total AMF community structure.

•	Metabarcoding_alpha
•	Metabarcoding_beta
•	Bubble_plot_Alpha_AMF

4. Resident AMF community responses (RNA-derived data): Assesses treatment effects on the putatively active fraction of the AMF community.
•	RNA_alpha
•	RNA_beta

5. DNA vs RNA community comparison: Compares community structure inferred from DNA metabarcoding and RNA-derived taxonomy.
•	RNAvDNA_full

6. Non-AMF microbial community responses: Evaluates treatment effects on bacteria/archaea, fungi, protists, and viruses.
•	Kingdom_taxonomy_clean
•	Kingdom_prep
•	Kingdoms_alpha
•	Kingdoms_beta

7. Plant and soil responses: Tests effects of AMF inoculation and soil management on plant performance and soil chemistry.
•	PlantMR_Soil_Chem

Analysis Workflow Summary
1.	Data preparation
o	Import DNA and RNA feature tables
o	Standardize taxonomy across datasets
o	Merge with metadata
o	Restrict analyses to matched samples where required

2.	RNA preprocessing
o	Filter transcriptome-derived data
o	Separate AMF and non-AMF taxa
o	Assign and clean taxonomy
o	Generate relative abundance tables

3.	Normalization
o	DNA data rarefied to 4,363 reads per sample
o	RNA data analyzed as within-sample relative abundance
o	All community analyses conducted on relative abundance data

4.	Diversity analyses
o	Alpha diversity calculated using standard ecological metrics
o	Beta diversity calculated using Bray–Curtis (abundance) and Jaccard (presence/absence) dissimilarities

5.	Statistical testing
o	Full factorial models: AMF × fertilization × tillage
o	PERMANOVA (999 permutations) for community composition
o	Homogeneity of dispersion assessed using betadisper
o	Pairwise comparisons adjusted using Benjamini–Hochberg correction

6.	Cross-method comparison (DNA vs RNA)
o	Mantel tests (Spearman, 999 permutations)
o	Procrustes analysis (999 permutations)
o	PERMANOVA with method as a fixed effect
o	SIMPER analysis to identify taxa contributing to differences

7.	Taxonomic contribution
o	SIMPER used to identify taxa contributing up to 70% of dissimilarity

8.	Visualization
o	Figures generated using ggplot2


Requirements
R environment, R ≥ 4.4.1
Packages:
•	tidyverse
•	vegan
•	emmeans
•	MASS
•	cplm
•	patchwork
•	ggplot2
•	lme4
•	nlme
•	ggplot2

External tools
•	QIIME2 (2024.10)
•	mmseqs2

Computing environment
Analyses were conducted using RStudio (v.2024.09.0) and, where required, on the UBC Advanced Research Computing (ARC) Sockeye cluster using SLURM.

Reproducibility Notes
•	Analyses assume consistent sample identifiers across all datasets
•	DNA and RNA comparisons were restricted to shared samples (n = 27 paired samples)
•	RNA and DNA datasets differ in sequencing depth; comparisons are therefore based on relative abundance
•	All permutation-based analyses used 999 permutations unless otherwise specified

Data Availability
Sequence data and associated metadata are available through the NCBI Sequence Read Archive (SRA) (accession: XXXX).

