# WHOLE GENOME SEQUENCING (WGS) of _Mycobacterium tuberculosis_
WGS pipeline (Quality Check, Genome Mapping, Variant Calling, and Variant Annotation) of _Mycobacterium tuberculosis_


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
