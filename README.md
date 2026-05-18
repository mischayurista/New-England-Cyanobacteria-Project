# New England Cyanobacteria Project
## Authors 
Ram Prajapati and Mischa Yurista
## Background
Cyanobacteria (blue-green algae) are photosynthetic prokaryotes found in aquatic environments worldwide. Some species produce cyanotoxins, potent biotoxins that can accumulate in water and pose serious health risks to humans and wildlife. The Lake Tahoe Aerosol Project investigates an emerging concern: pico-scale cyanobacteria that are so small they can aerosolize into water vapor and become airborne (Merrill et al., 2022; doi: https://doi.org/10.3390/ijms22168726). This phenomenon may result in chronic inhalation exposure to biotoxins, potentially contributing to neurological pathologies (Fobel et al., 2014; doi: https://doi.org/10.1212/WNL.88.16_supplement.P5.086).
Our objective was to characterize cyanobacterial communities in aerosol and water samples from New England lakes collected over the summer. By comparing aerosolized samples (AIR) with whole water samples (WLW), we aimed to identify which cyanobacteria are small enough to aerosolize and assess the toxin-producing potential of these communities. 
## Methods
Samples were collected from multiple New England lakes during summer months. We analyzed three types of samples:
AIR-EW, AIR-TK, AIR-VP: Aerosolized water samples, containing bacteria small enough to aerosolize
WLW-EW, WLW-TK, WLW-VP: Filtered whole lake water samples, containing all bacteria including those that do and do not aerosolize
NTC: No template control (negative control)
PAC: Blank control
16S rRNA Sequencing and Data Processing
DNA was extracted from all samples and amplified using 16S rRNA gene primers targeting the V4-V5 hypervariable region. All sequencing was performed, generating paired-end fastq files (*.fastq.gz). Processing was conducted using QIIME2 (Bolyen et al., 2019) and the DADA2 pipeline on the RON computing cluster.
Pipeline overview:

Quality Control (01_trim.sh): PolyG tail filtering and read quality assessment using fastp (Chen et al., 2023). This step removes reads with low quality and filters polyG tails that can occur in Illumina sequencing.
Primer Removal (02_cutadapt.sh): Removal of 16S V4-V5 forward (GTGYCAGCMGCCGCGGTAA) and reverse (CCGYCAATTYMTTTRAGTTT) primers using cutadapt.
Denoising (03_denoise.sh): DADA2 denoising with parameters optimized for 16S V4-V5 amplicons (overlap=10, truncLenF=220, truncLenR=215). This step infers amplicon sequence variants (ASVs).
Taxonomic Classification (04_classify.sh): Classification of ASVs using SILVA 16S reference database (99% identity threshold) with a pre-trained naive Bayes classifier.

All code is version controlled and available in the code/ directory of this repository for reproducibility.
## Findings
![Taxa Barplot](plots/taxa-barplot.png)
Figure 1. 
Quality control and taxonomic composition analyses revealed the distribution of cyanobacterial communities across aerosol and water sample types.
Figure 1. Taxonomic composition of cyanobacterial ASVs across sample types. Visualization generated using QIIME2's built-in taxonomy bar plot tool. ASVs were assigned to operational taxonomic units (OTUs) based on 99% sequence similarity to the SILVA reference database. This figure highlights the relative abundance of cyanobacterial taxa in aerosolized samples (AIR) versus whole water samples (WLW) from three lakes (EW, TK, VP), demonstrating differential representation of taxa between aerosol and non-aerosol fractions.
Key Observations:
1. Specific cyanobacterial taxa were enriched in aerosol samples relative to whole water, suggesting size-fractionation of the cyanobacterial community
2. Sample controls (NTC, PAC) showed minimal contamination, validating the quality of our analysis
3. Community composition varied between lakes, reflecting distinct environmental conditions at each sampling site

These results support the hypothesis that pico-scale cyanobacteria capable of aerosolizing are a distinct subset of the broader lake cyanobacterial community. Further work should investigate the toxin-producing potential of aerosolized taxa and assess long-term health impacts from chronic inhalation exposure in affected lake regions.
## References
Bolyen, E., Rideout, J. R., Dillon, M. R., et al. (2019). Reproducible, interactive, scalable and extensible microbiome data science using QIIME 2. Nature Biotechnology, 37(8), 852–857.
Chen, S., Zhou, Y., Chen, Y., & Gu, J. (2023). Fastp: an ultra-fast all-in-one FASTQ preprocessor. Bioinformatics, 34(17), i884–i890.
Fobel, R., et al. (2014). Chronic neurological disease associated to cyanobacterial toxins. Neurology, 88(16 Supplement), P5.086.
Merrill, S., Desai, K., Carney, A., et al. (2022). Small, toxic: cyanobacterial toxins in aerosolized water. International Journal of Molecular Sciences, 22(16), 8726.
