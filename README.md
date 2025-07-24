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
