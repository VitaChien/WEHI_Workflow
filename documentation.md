# Overview

REDMANE aims to streamline data processing and access across labs, teams, and organizations. Given that raw data can be massive—reaching terabytes in size—and may contain sensitive patient information or proprietary data, REDMANE ensures secure handling while maintaining accessibility for authorized users. 
This document focuses on the Workflow that data go through to be transformed from Raw to processed and eventually summarised.
An explanatation of the different data types is provided for further clarification.

REDMANE uses Sythetic data because it can be used when real data is limited, sensitive, or unavailable. It allows for testing, training machine learning models, and validating workflows without privacy concerns. It also helps simulate rare events, improve model generalization, and ensure reproducibility in research.

## Data types:
The field of bioinformatics is now expanding to include various types of experiments, such as Whole Genome Sequencing (WGS), RNA Sequencing, single-cell RNA Sequencing, spatial omics, and others.

Each experiment's data analysis starts with **raw data**, which is processed using different bioinformatics tools for specific purposes. These tools perform intermediate steps such as quality control and alignment, producing **processed files** that are then used to generate **summarized data**. This summarized data is typically what interests researchers for further analysis and visualization.

For example, in WGS, Variant Call Format (.vcf) files are generated, containing detected variants for the genome sequence of a specific sample.

# Workflow Team: 

As the **Workflow Team**, our role is central to transforming raw sequencing data into meaningful processed and summarized data. Collaboration with other teams ensures smooth data flow and integration.  

## Clinical Dashboard Team (Input Providers)  
- We rely on the **Clinical Dashboard Team** to provide **synthetic or real raw data** (e.g., WGS/RNA-Seq).  
- We maintain communication to ensure data quality, proper formatting, and metadata consistency.  
- Any preprocessing or data standardization requirements are discussed to streamline workflow compatibility.  

## Data Registry Team (Processed Data Managers)  
- Once data is processed, we hand it over to the **Data Registry Team** in formats such as **BAM/CRAM**.  
- We collaborate to ensure data storage, versioning, and accessibility align with research needs.  
- We also coordinate on **summarized outputs (e.g., VCF, MAF)**, ensuring the necessary transformations are performed for downstream analysis.  

## Overall Collaboration  
- We serve as the bridge between raw data providers and data consumers.  
- Regular communication ensures workflow efficiency, error handling, and data integrity.  
- Feedback loops help refine processing pipelines and improve output usability.  

![Workflow Chart](/Users/daniaistwani/Desktop/workflow_chart.png)

Our collaboration ensures that **raw data is efficiently processed, stored, and made available for meaningful analysis**, ultimately supporting research advancements. 🚀

# Summer-2025 intake focus:

# Whole Genome Sequencing (WGS) Workflow  

Whole Genome Sequencing (WGS) involves processing raw sequencing data to extract meaningful biological insights. This process typically transforms raw reads in **FASTQ** format into aligned and processed data in **BAM** or **CRAM** format, which is then further analyzed to produce variant call data in **VCF** format.  

Our team implemented this workflow using two different tools: **Galaxy** and **Nextflow**, each with distinct advantages and trade-offs.  

## Tool Comparison  

### Galaxy  
- User-friendly with an intuitive graphical interface  
- Provides a broad selection of bioinformatics tools  
- Ideal for users with minimal programming experience  
- Limited scalability for large-scale datasets and high-throughput sequencing  

### Nextflow  
- Designed for scalability, reproducibility, and automation  
- Enables efficient parallel execution across cloud platforms and HPC clusters  
- Requires scripting knowledge but offers greater flexibility and performance  
- Well-suited for large-scale sequencing analyses  

## Galaxy for WGS:

Galaxy was initially chosen for its ability to deliver quick results and provide processed and summarized data to teams awaiting analysis. Due to the extensive troubleshooting and steep learning curve associated with Nextflow, Galaxy was prioritized for primary analysis to accelerate data turnaround. This approach allowed for immediate data processing while Nextflow was gradually integrated for scalable and automated workflows.

### Galaxy analysis: 

  **Step 1: Read Mapping with BWA-MEM**
*Input:* FASTQ files, Reference genome
*Output:* CRAM/BAM files

1. Upload raw sequencing reads (FASTQ files) to Galaxy.
2. Select the corresponding reference genome.
3. Run BWA-MEM to align reads to the reference genome. 


**Step 2: Variant Calling with FreeBayes**

*Input:* BAM file, Reference genome
*Output:* VCF file (Variant Call Format)

Filter and annotate the VCF file if needed.

**Step 3: VCF to MAF Conversion**

*Input:* VCF file, Reference genome
*Output:* MAF file (tabular)

Convert the VCF file to MAF (Mutation Annotation Format) using the appropriate tool (e.g., vcf2maf).

![Galaxy Diagram](https://github.com/VitaChien/WEHI_Workflow/blob/add/screenshots/screenshots/Galaxy%20workflow%20diagram.png)


## Nextflow for WGS
Nextflow was adopted to overcome the limitations of Galaxy, particularly in handling large-scale datasets and ensuring workflow scalability. While Galaxy offered a quick and accessible solution for initial analyses, its constraints in automation, reproducibility, and resource management were an issue in dealing with a large dataset.

Upon research, **Nextflow** emerged as a robust alternative, enabling the automation and optimization of complex workflows while efficiently utilizing high-performance computing (HPC) and cloud resources. Despite the learning curve and troubleshooting challenges, the adoption of Nextflow showed better workflow reproducibility and scalability. This transition provides long-term sustainability and efficiency in Whole Genome Sequencing (WGS) pipelines.

### Nextflow analysis:

For Whole Genome Sequencing (WGS), Nextflow provides an integrated nf-core pipeline called **Sarek**. Sarek is specifically designed for germline and somatic variant calling in WGS and Whole Exome Sequencing (WES) data. It supports various aligners, preprocessing steps, and variant callers, making it a well-structured and scalable solution for genomic analysis.

#### Setting Up Sarek on Seqera:

1. Request an access to Milton HPC refer to this link: [https://wehieduau.sharepoint.com/sites/rc2/SitePages/using-milton.aspx]
2. Submit tickets to ask for access to Seqera
3. Upload raw data to /vast/scratch/users/yourname/ + any subfolder you desire
4. Generate access token on Seqera and fill it in the Nextflow Tower Agent page
5. Select Sarek_344 from Lanchpad and launch it
6. Fill in Run setup configuration and launch the pipeline

##### Sarek Input:
The input file that Sarek takes is in CSV format with metadata. Listing sample information and corresponding FASTQ file paths. Each row represents a sample, with columns for patient ID, sample ID, sequencing lane, and paths to paired-end FASTQ files (fastq_1 and fastq_2). The FASTQ files must be gzip-compressed (.fastq.gz) for compatibility with bioinformatics tools. Additional columns like sex, status, and spring file paths may provide further metadata or alternative file formats.
more information can be found here: [https://nf-co.re/sarek/latest/docs/usage/]




```sh
