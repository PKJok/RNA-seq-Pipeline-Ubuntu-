# 🧬 RNA-seq Pipeline with Ubuntu, FastQC, Trimmomatic, HISAT2, and Samtools

This repository presents a complete **RNA-seq pipeline** using essential bioinformatics tools—**FastQC**, **Trimmomatic**, **HISAT2**, **Samtools**, and the **SRA Toolkit**—to process raw sequencing data (e.g., FASTQ or SRA files) into aligned and sorted **BAM** files.

---

## 📚 Introduction

This RNA-seq pipeline includes:

- Data acquisition from NCBI GEO/SRA
- Quality control using FastQC
- Adapter and quality trimming with Trimmomatic
- Splice-aware alignment using HISAT2
- BAM conversion and sorting using Samtools

All steps are executed in a **Linux/Ubuntu environment**. If you're using Windows, you’ll need [**Windows Subsystem for Linux (WSL)**](https://learn.microsoft.com/en-us/windows/wsl/) and Ubuntu, both available from the Microsoft Store.

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

A demo FASTQ file used in this pipeline can be downloaded here:  
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
