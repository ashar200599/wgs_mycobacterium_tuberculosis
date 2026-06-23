# Chapter 1 : Make a directory

**1. Make root folder**

```bash
mkdir wgs
cd wgs
```

**2. Make sub-folder**

```bash
mkdir raw_data reference_data scripts results
mkdir -p results/fastqc
mkdir -p results/fastp
mkdir -p results/bwa
mkdir -p results/samtools
mkdir -p results/freebayes
mkdir -p results/bcftools
```

# Chapter 2: Conda Setup (Windows)

## A.Installing Conda

**1. Download Conda installer**

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

**2. Run the installer**

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

**3. Waking Up Conda**

```bash
source ~/.bashrc
conda --version
```

**4. Create a conda environment**

```bash
conda create -n wgs python=3.9 -y
conda activate wgs
```

## B. Setting up Bioconda

```bash
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

## C. WGS Tools installation

```bash
conda install -y sra-tools fastqc multiqc fastp bwa samtools freebayes snpeff

prefetch --version
fastq-dump --version
fastqc --version
multiqc --version
fastp --version
bwa --version
samtools --version
freebayes --version
snpeff --version
```

**Notes:**

If installing freebayes error try this

```bash
sudo apt update
sudo apt update && sudo apt install -y pkg-config liblzma-dev cmake
```

```bash
git clone --recursive https://github.com/freebayes/freebayes.git
cd freebayes
meson setup build
cd build
meson compile
freebayes --version
```

If installing snpeff error try this

1. Check Java version

```bash
java --version
```

2.If jave version less than ver.21, update java

```bash
sudo apt update
sudo apt install openjdk-21-jdk
```

3. Download and install snpeff

```bash
wget https://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip
unzip snpEff_latest_core.zip
cd snpEff
java -jar snpEff.jar --version
```

# Chapter 3: Data download

**1. Download SRA data**

```bash
cd raw_data
prefetch SRR37582408


```

**2. SRA to FASTQ conversion**

```bash
fastq-dump --split-files SRR37582408.sra

```

# Chapter 4: Quality control

**1. FastQC**

```bash
fastqc SRR37582408_1.fastq SRR37582408_2.fastq -o ../results/fastqc/
```

**2. Adapter trimming**

```bash

fastp -i SRR37582408_1.fastq -I SRR37582408_2.fastq -o ../results/fastp/sample_clean_1.fastq -O ../results/fastp/sample_clean_2.fastq --detect_adapter_for_pe --html ../results/fastp/fastp_report.html --json ../results/fastp/fastp_report.json


```

**3.Check fastp result**

```bash
cd ../results/fastp
explorer.exe fastp_report.html
```

**4. Check the quality after trimming**

```bash
fastqc sample_clean_1.fastq sample_clean_2.fastq -o ../fastqc/
explorer.exe sample_clean_1_fastqc.html
explorer.exe sample_clean_2_fastqc.html
```

# Chapter 5 : Genome Mapping

**1. Reference genome download**

```bash
cd ../reference_data
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/195/955/GCF_000195955.2_ASM19595v2/GCF_000195955.2_ASM19595v2_genomic.fna.gz
```

**2.Unzip reference genome**

```bash
 gunzip GCF_000195955.2_ASM19595v2_genomic.fna.gz

```

**3.Rename reference genome**

```bash
mv GCF_000195955.2_ASM19595v2_genomic.fna reference.fna

```

**4. Index reference genome**

```bash
bwa index reference.fna

```

**5.Mapping Reads into reference genome**

```bash
cp ../results/fastp/sample_clean_1.fastq .
cp ../results/fastp/sample_clean_2.fastq .
bwa mem reference.fna sample_clean_1.fastq sample_clean_2.fastq -o ../results/bwa/alignment.sam

```

# Chapter 6 : Convert and Short Data

**1. Convert SAM to BAM**

```bash
cd ../results/bwa
samtools view -bS alignment.sam -o ../samtools/alignment.bam
cd ../samtools
samtools sort alignment.bam -o ../samtools/sorted.bam
samtools index sorted.bam
```

**2. Using samtools for advanced analysis**

```bash
samtools flagstat sorted.bam        # see basic statistic
samtools depth sorted.bam  |  head -n 10         # see depth of coverage
samtools coverage sorted.bam                    # see depth of coverage
```

# Chapter 4: Variant calling

1. Copy sorted.bam and reference.fna to the freebayes directory

```bash
cp ../samtools/sorted.bam .
cp ../../reference_data/reference.fna .

```

2. Run freebayes

```bash
freebayes -f reference.fna --min-mapping-quality 20 --min-base-quality 20 --min-coverage 10 sorted.bam > variants_raw.vcf
```

3. Filter VCF file with BCF tools

```bash
sudo apt install bcftools
bcftools filter -e 'QUAL<30 || INFO/DP<10 || AF < 0.1' variants_raw.vcf -o ../bcftools/variants_filtered.vcf
```

4. VCF Normalization

```bash
cd ../bcftools
cp ../../reference_data/reference.fna .
bcftools norm -f reference.fna -m- variants_filtered.vcf -o variants_norm.vcf
```

5. Check result

```bash
grep "^#CHROM" variants_norm.vcf && grep -v "^#" variants_norm.vcf | head -5
```

# Chapter 5: Variant Annotation

1. Variant Annotation

```bash
grep -v "^#" variants_norm.vcf | cut -f1 | sort -u          #check CHROM
sed 's/NC_000962.3/Chromosome/g' variants_norm.vcf > variants_norm_renamed.vcf   #rename CHROM

```

2. Run snpEff

```bash
cd ../../snpEff
cp ../wgs/results/bcftools/variants_norm_renamed.vcf .
java -jar snpEff.jar ann -v -dataDir "F:/Materi WGS Inbio/wgs/reference_data" -stats ../wgs/results/snpEff/snpEff_summary.html -csvStats ../wgs/results/snpEff/snpEff_summary.csv  Mycobacterium_tuberculosis_h37rv variants_norm_renamed.vcf > ../wgs/results/snpEff/variants_annotated.vcf
```

3. Check results

```bash
cd ../snpEff
explorer.exe snpeff_summary.html
```

4. Data exploration

```bash
bcftools view -H variants_annotated.vcf | wc -l     #Count variants
```

```bash
bcftools view -H variants_annotated.vcf | cut -f10 | cut -d: -f1 | sort | uniq -c  #Check homozygote or heterzogote variants
```

5. Visualization

```bash
git clone https://github.com/ewels/ngi_visualizations.git
```

```bash
conda install -y setuptools matplotlib numpy #install dependencies
cd ngi_visualizations
python setup.py install

```

If error

```bash
pip install 2to3
2to3 -w ngi_visualizations/
pip install .
```

```bash
python ngi_visualizations/snpEff/snpEff_plots.py ../wgs/results/snpEff/snpEff_summary.csv #MAke plot

```
