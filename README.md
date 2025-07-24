# 🧬 RNA-seq Pipeline with Ubuntu, FastQC, Trimmomatic, HISAT2, and Samtools

This repository presents a complete **RNA-seq pipeline** using essential bioinformatics tools such as **FastQC**, **Trimmomatic**, **HISAT2**, **Samtools**, and the **SRA Toolkit** to process raw sequencing data (e.g., FASTQ or SRA files) into aligned and sorted **BAM** files.

---

## 📚 Introduction

This RNA-seq pipeline includes:

- Data acquisition from NCBI GEO/SRA
- Quality control using FastQC
- Adapter and quality trimming with Trimmomatic
- Splice-aware alignment using HISAT2
- BAM conversion and sorting using Samtools

All steps are executed in a **Linux/Ubuntu environment**. If you're using Windows, you’ll need [**Windows Subsystem for Linux (WSL)**](https://learn.microsoft.com/en-us/windows/wsl/) and Ubuntu, both can be downloaded from the **Microsoft Store**.

Use this [**youtube tutorial**](https://youtu.be/OqCPkcRoMF0?si=eTzRoNglRq6dEFWn) to download Ubuntu and WSL.

### 🧪 Learn Bash Basics for Bioinformatics

Recommended beginner-friendly tutorials:

1. [Bash for Biologists #1](https://youtu.be/zvXe3udfg_I)
2. [Bash for Biologists #2](https://youtu.be/lUGj5FygYGA)
3. [Bash for Biologists #3](https://youtu.be/h1Xm0j-gjbQ)
4. [Linux Bash Basics](https://youtu.be/amUmwDt1WB0)

---

## 💻 Why Linux for RNA-seq?

1. Open source, customizable environment.
2. Compatible with tools like HISAT2, STAR, DESeq2.
3. Efficient for large-scale datasets.
4. Supports parallel processing.
5. Access to Bioconda/Bioconductor for bioinformatics tools.

---

## 🔎 Acquiring SRA Data

Use [**NCBI GEO**](https://www.ncbi.nlm.nih.gov/geo/) to find transcriptomic datasets.

### Example:
From the study ["Rice B2 and B3 RAFs play central roles in ABA and osmotic stress signaling"](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE282986):

- Click **SRA Run Selector**
- Download the **SRA Accession List**
- Watch this [YouTube tutorial](https://youtu.be/zE851fWCYQg?si=n5Jwdo_YaAz4I8Dy) for help (watch up to 5:33)

---

## 🔧 Install the SRA Toolkit 

```bash
# In bash: Download by using wget
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.2.1/sratoolkit.3.2.1-ubuntu64.tar.gz

# In Bash: Extract
tar -xvzf sratoolkit.3.2.1-ubuntu64.tar.gz

# In Bash: Add to PATH
echo 'export PATH="$HOME/sratoolkit.3.2.1-ubuntu64/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# In Bash: Test
fastq-dump --version
```
## 📥 SRA File Download

After installing the SRA Toolkit, use the `SRA_downloader_bash_script` provided in this repository.

> **Note**: The output directory used in the script is:  
> `SRA_TOOL/tmp`

---

 ## ⬇️ A demo FASTQ file used in the above given pipeline in the repository can be downloaded here:
[Demo FASTQ File](https://drive.google.com/file/d/1DGHjbhcRy_zTm6H9C_AUpkzBML-JhtA3/view) 

---


## 🐍 Installing Miniconda on Linux

Follow these steps to install Miniconda and configure channels for bioinformatics work.Miniconda is used to manage tools like `fastqc`, `multiqc`, `trimmomatic`, `hisat2`, and others.

### 1. Download Miniconda Installer

Visit the [Miniconda download page](https://docs.conda.io/en/latest/miniconda.html) or use the command below for 64-bit Linux:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

### 2. Verify the Installer (Optional but Recommended)

```bash
sha256sum Miniconda3-latest-Linux-x86_64.sh
```

### 3. Run the Installer

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the prompts to complete the installation.

### 4. Initialize Conda

```bash
~/miniconda3/bin/conda init bash
```

### 5. Restart the Terminal or Source Your Shell Config

```bash
source ~/.bashrc
```

### 6. Test the Conda Installation

```bash
conda --version
```

---

## ➕ Add Bioconda and Conda-Forge Channels

After installing Conda, add the necessary channels to install bioinformatics tools.

```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

> **Note**: Bioconda is required to install most bioinformatics tools like `sra-tools`, `samtools`, `bwa`, and others. Conda-forge is also important because many Bioconda packages depend on it.


# Unified Conda Environment for RNA-seq Tools

After adding channels, we create a Unified Conda Environment. Instead of managing separate environments for each tool, create a single Conda environment that includes all necessary tools (FastQC, Trimmomatic, HISAT2, etc.) to minimize activation steps.

## Create Environment

```bash
conda create -n rna_seq -c bioconda -c conda-forge fastqc multiqc hisat2 samtools trimmomatic
```

### Description

- `conda create -n rna_seq`: creates an environment named `rna_seq`
- `-c bioconda -c conda-forge fastqc multiqc hisat2 samtools trimmomatic`: installs all necessary tools in the environment

### Activate Environment

```bash
conda activate rna_seq
```

---

# How to Interpret the FastQC Report

## Materials
1. [MSU FastQC Tutorial](https://rtsf.natsci.msu.edu/genomics/technical-documents/fastqc-tutorial-and-faq.aspx)
2. [Academia Guidelines](https://www.academia.edu/89303100/Guidelines_for_RNA_Seq_data_analysis)
3. [YouTube Tutorial](https://youtu.be/G1KpIoeEXlo?si=MozEEpEdzo2qya98)

---

# Downloading Essential Materials

## a. Adapters for Trimmomatic

Download from [Trimmomatic GitHub - Adapters](https://github.com/usadellab/Trimmomatic/tree/main/adapters)

### Conditions
- For Single End Reads (SE): `TruSeq3-SE.fa`
- For Paired End Reads (PE): `TruSeq3-PE.fa`

### Bash Commands

```bash
mkdir adapters
cd adapters
wget https://github.com/usadellab/Trimmomatic/raw/refs/heads/main/adapters/TruSeq3-PE.fa
wget https://github.com/usadellab/Trimmomatic/raw/refs/heads/main/adapters/TruSeq3-SE.fa
```

## b. Reference Genome (Human)

Download from [HISAT2 Download Page](https://daehwankimlab.github.io/hisat2/download/)

```bash
wget https://genome-idx.s3.amazonaws.com/hisat/grch38_genome.tar.gz
tar -xvfz grch38_genome.tar.gz
```

---

# Understanding Trimmomatic

## 1. Removing Adapter Sequences

```bash
trimmomatic PE -phred33 SRR12345678_1.fastq SRR12345678_2.fastq   output_R1_paired.fq output_R1_unpaired.fq output_R2_paired.fq output_R2_unpaired.fq   ILLUMINACLIP:TruSeq3-PE.fa:2:30:10
```

## 2. Trimming Low Quality Bases

```bash
trimmomatic SE -phred33 SRR12345678.fastq output_trimmed.fq   LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```

- `LEADING:3`, `TRAILING:3`: Remove bases with quality <3 from start/end
- `SLIDINGWINDOW:4:15`: Remove if 4-base window avg quality <15
- `MINLEN:36`: Discard reads <36 bases

## 3. Filtering Short or Poor-Quality Reads

The `MINLEN` parameter ensures only sufficiently long reads are retained.

## 4. Paired-End vs Single-End Reads

- `PE` = maintain read pairing
- `SE` = simple quality trimming

---

# References

## Trimmomatic
- [Trimmomatic Manual](http://www.usadellab.org/cms/?page=trimmomatic)
- [Trimmomatic Article](https://pmc.ncbi.nlm.nih.gov/articles/PMC7671312/)

**Note:** Use `trimmomatic` (from conda) instead of `java -jar trimmomatic-0.39.jar`.

## HISAT2
- [HISAT2 Manual](https://daehwankimlab.github.io/hisat2/manual/)
- [HISAT2 Paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC5032908/pdf/nihms816842.pdf)
- [HISAT2 YouTube](https://youtu.be/KldnnPM2gm4?si=9xEpczpObkHsVJX4)

---

# Final Note

Use the provided `RNA-seq_Pipeline_bash_script` **step by step**. Do not run it all at once. Manage input/output directories accordingly or seek help from AI tools when necessary.


