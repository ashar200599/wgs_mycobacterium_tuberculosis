# WHOLE GENOME SEQUENCING (WGS) of _Mycobacterium tuberculosis_
WGS pipeline (Quality Check, Genome Mapping, Variant Calling, and Variant Annotation) of _Mycobacterium tuberculosis_)


---
## 🧬 Biological Question

> Are there variants in rifampicin resistance genes?

| | |
|---|---|
| **Dataset** | SRR37582408 —  _Mycobacteriun tuberculosis_ sputum isolate|
| **Genome Reference** | GCF_000195955.2 |
| **Key finding** | rpoB as rifampicin resistance gene is present |



---
## Results

### SNP Effect by Region Barplot
![Barplot](https://github.com/ashar200599/wgs_mycobacterium_tuberculosis/blob/d48d0e1f77571dcdd0a371081ebe42ee3426a054/plot/effect_regions.png)

### SNP Effect by Type Barplot
![Barplot](https://github.com/ashar200599/wgs_mycobacterium_tuberculosis/blob/d48d0e1f77571dcdd0a371081ebe42ee3426a054/plot/effect_types.png)

### Manhattan Plot
![Manhattan Plot](https://github.com/ashar200599/wgs_mycobacterium_tuberculosis/blob/d48d0e1f77571dcdd0a371081ebe42ee3426a054/plot/manhattan_plot.png)

### Pie Chart
![Pie Chart](https://github.com/ashar200599/wgs_mycobacterium_tuberculosis/blob/d48d0e1f77571dcdd0a371081ebe42ee3426a054/plot/pie_charts.png)

```
.
├── README.md
├── freebayes
├── ngi_visualizations
├── plot
│   ├── effect_regions.png
│   ├── effect_types.png
│   ├── manhattan_plot.png
│   └── pie_charts.png
├── reference_data
│   ├── GCF_000195955.2_ASM19595v2_genomic.fna.gz
│   ├── Mycobacterium_tuberculosis_h37rv
│   │   ├── snpEffectPredictor.bin
│   │   └── snpEffectPredictor.bin.fai
│   ├── reference.fna
│   ├── reference.fna.amb
│   ├── reference.fna.ann
│   ├── reference.fna.bwt
│   ├── reference.fna.pac
│   └── reference.fna.sa
├── results
│   ├── bcftools
│   │   ├── reference.fna
│   │   ├── reference.fna.fai
│   │   ├── variants_filtered.vcf
│   │   ├── variants_norm.vcf
│   │   └── variants_norm_renamed.vcf
│   ├── fastp
│   │   ├── fastp_report.html
│   │   └── fastp_report.json
│   ├── fastqc
│   │   ├── SRR37582408_1_fastqc.html
│   │   ├── SRR37582408_1_fastqc.zip
│   │   ├── SRR37582408_2_fastqc.html
│   │   ├── SRR37582408_2_fastqc.zip
│   │   ├── sample_clean_1_fastqc.html
│   │   ├── sample_clean_1_fastqc.zip
│   │   ├── sample_clean_2_fastqc.html
│   │   └── sample_clean_2_fastqc.zip
│   ├── freebayes
│   │   ├── reference.fna
│   │   ├── reference.fna.fai
│   │   ├── sorted.bam.fai
│   │   └── variants_raw.vcf
│   ├── samtools
│   │   ├── alignment.bam.fai
│   │   ├── reference.fna
│   │   ├── reference.fna.fai
│   │   ├── sorted.bam.bai
│   │   └── variants_raw.vcf
│   └── snpEff
│       ├── snpEff_summary.csv
│       ├── snpEff_summary.genes.txt
│       ├── snpEff_summary.html
│       └── variants_annotated.vcf
├── scripts
│   ├── plot_script.Rmd
│   └── script.md
└── snpEff
    ├── SnpSift.jar
    ├── examples
    │   ├── 1kg.head_chr1.filtered.vcf.gz
    │   ├── 1kg.head_chr1.vcf.gz
    │   ├── cancer.ann.vcf
    │   ├── cancer.eff.vcf
    │   ├── cancer.vcf
    │   ├── cancer_pedigree.ann.vcf
    │   ├── cancer_pedigree.vcf
    │   ├── example_motif.vcf
    │   ├── examples.sh
    │   ├── file.vcf
    │   ├── intervals.bed
    │   ├── my_annotations.bed
    │   ├── samples_cancer.txt
    │   ├── samples_cancer_one.txt
    │   ├── test.1KG.ann_encode.vcf
    │   ├── test.1KG.ann_reg.vcf
    │   ├── test.1KG.vcf
    │   ├── test.ann.vcf
    │   ├── test.chr22.ann.filter_missense.vcf
    │   ├── test.chr22.ann.filter_missense_any.vcf
    │   ├── test.chr22.ann.filter_missense_any_TRMT2A.vcf
    │   ├── test.chr22.ann.filter_missense_first.vcf
    │   ├── test.chr22.ann.one_per_line.txt
    │   ├── test.chr22.ann.txt
    │   ├── test.chr22.ann.vcf
    │   ├── test.chr22.vcf
    │   ├── test.vcf
    │   ├── variants_1.ann.vcf
    │   ├── variants_1.vcf
    │   ├── variants_2.ann.vcf
    │   └── variants_2.vcf
    ├── galaxy
    │   ├── snpEff.xml
    │   ├── snpEffWrapper.pl
    │   ├── snpEff_download.xml
    │   ├── snpSiftWrapper.pl
    │   ├── snpSift_annotate.xml
    │   ├── snpSift_caseControl.xml
    │   ├── snpSift_filter.xml
    │   ├── snpSift_int.xml
    │   ├── tool-data
    │   │   ├── snpEff_genomes.loc
    │   │   └── snpEff_genomes.loc.sample
    │   ├── tool_conf.xml
    │   └── tool_dependencies.xml
    ├── scripts
    │   ├── 1kg.sh
    │   ├── annotate_demo.sh
    │   ├── annotate_demo_GATK.sh
    │   ├── bedEffOnePerLine.pl
    │   ├── buildDbNcbi.sh
    │   ├── cgShore.pl
    │   ├── cgShore.sh
    │   ├── countColumns.py
    │   ├── db.pl
    │   ├── extractSequences.pl
    │   ├── fasta2tab.pl
    │   ├── fastaSample.pl
    │   ├── fastaSplit.pl
    │   ├── fastqSplit.pl
    │   ├── filterBy.py
    │   ├── gffRemovePhase.pl
    │   ├── gsa
    │   │   ├── bayesFactor_correction_scoreCount.r
    │   │   ├── bayesFactor_correction_scoreCount.sh
    │   │   ├── bayesFactor_correction_scoreCount_max10.sh
    │   │   ├── checkGeneNames.py
    │   │   ├── create_sets.bds
    │   │   ├── geneSetOverlap.py
    │   │   ├── geneSetOverlap.sort.txt
    │   │   ├── geneSetsGtex.py
    │   │   ├── pvalue_correction_scoreCount.r
    │   │   ├── pvalue_correction_scoreCount.sh
    │   │   └── pvalue_correction_scoreCount_min10.sh
    │   ├── isutf8.py
    │   ├── join.pl
    │   ├── joinSnpEff.pl
    │   ├── make_dbNSFP.sh
    │   ├── nextProt_filter.pl
    │   ├── ped2vcf.py
    │   ├── plot.pl
    │   ├── plotHistogram.pl
    │   ├── plotLabel.pl
    │   ├── plotMA.pl
    │   ├── plotQQ.pl
    │   ├── plotQQsubsample.pl
    │   ├── plotSmoothScatter.pl
    │   ├── plotXY.pl
    │   ├── queue.pl
    │   ├── sam2fastq.pl
    │   ├── snpEff
    │   ├── snpSift_filter_sample_to_number.pl
    │   ├── sortLine.py
    │   ├── splitChr.pl
    │   ├── statsNum.pl
    │   ├── swapCols.pl
    │   ├── transpose.pl
    │   ├── txt2fa.pl
    │   ├── txt2vcf.py
    │   ├── uniqCount.pl
    │   ├── uniqCut.pl
    │   ├── vcfAnnFirst.py
    │   ├── vcfBareBones.pl
    │   ├── vcfEffHighest.ORI.py
    │   ├── vcfEffOnePerLine.pl
    │   ├── vcfFilterSamples.pl
    │   ├── vcfInfoOnePerLine.pl
    │   ├── vcfOnlyAlts.pl
    │   ├── vcfReduceGenotypes.pl
    │   ├── vcfRefCorrect.py
    │   └── wigSplit.pl
    ├── snpEff.config
    ├── snpEff.jar
    └── variants_norm_renamed.vcf
```
---
## Methods
| Step | Tool | Details |
|---|---|---|
|Data Download| SRA Toolkit | SRR37582408 |
|SRA to FASTQ conversion |fastq-dump | splitting files into SRR37582408_1.fastq SRR37582408_2.fastq |
|Quality Control| FastQC and MultiQC | check FASTQ quality
|Adapter Trimming | FastP | clean th adapters |
|Genome Mapping| bwa | mapping reads into GCF_000195955.2 genome
|Convert SAM to BAM | samtools | convert .sam output into .bam format
|Variant Calling | freebayes | check variants
|Variant Annotation | snpEff | annotate variant using snpEff custom database
|VCF Plot | ggplot | Barplot, Manhattan plot, Pie chart


---

## 📈 Key Results

| Findings | Details | Biological Meaning |
|---|---|---|
| Downstream & Upstream gene regions | ~4000 genes | could affect gene expression |
| Variant Quality | uniform distribution | onsistent sequencing depth across the genome |
| Silent/Synonymous variants|38.73% |  these mutations don't change amino acid sequence|
| Missense variants |60.3% |amino acid change and alter protein function
| Modifier impact | 91.45% | variants in non-coding or regulatory regions with indirect/unknown effects
| Variant rate | 1 variant every 3,846 bases | relatively high genetic divergence from the reference strain

**Conclusion:** The _Mycobacterium tuberculosis_ sample has a low variant rate and variants driven by both regulatory and protein-level adaptive changes


---

## 👤 Author

**Ashar Kurnia** 
