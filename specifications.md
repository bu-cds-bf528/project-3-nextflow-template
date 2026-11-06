> **Note:** Sections marked **Instructions:** are scaffolding to guide you. Delete every
> instruction block (and the Example Table) once you've filled in the section, so the final
> document contains only your specifications.

# Provided Diagram

```mermaid
flowchart TD
    samples[/"samplesheet.csv<br>IP & INPUT, rep1 & rep2"/]
    genome[/"params.genome<br>hg38 FASTA"/]
    gtf[/"params.gtf"/]
    blacklist[/"params.blacklist<br>ENCODE blacklist BED"/]
    genebed[/"UCSC hg38 gene BED"/]

    FASTQC["FASTQC"]
    TRIM["TRIMMOMATIC"]
    BUILD["BOWTIE2_BUILD"]
    ALIGN["BOWTIE2_ALIGN"]
    SORT["SAMTOOLS_SORT"]
    INDEX["SAMTOOLS_INDEX"]
    FLAGSTAT["SAMTOOLS_FLAGSTAT"]
    MULTIQC["MULTIQC"]
    BAMCOV["BAMCOVERAGE"]
    MBWS["MULTIBWSUMMARY"]
    PLOTCOR["PLOTCORRELATION"]
    CMATRIX["COMPUTEMATRIX"]
    PROFILE["PLOTPROFILE"]
    TAGDIR["MAKETAGDIR"]
    PEAKS["FINDPEAKS"]
    POS2BED["POS2BED"]
    INTERSECT["BEDTOOLS_INTERSECT"]
    FILTER["BEDTOOLS_REMOVE_BLACKLIST"]
    ANNOTATE["ANNOTATEPEAKS"]
    MOTIFS["FINDMOTIFSGENOME"]

    samples --> FASTQC
    samples --> TRIM
    genome --> BUILD
    TRIM -- trimmed reads --> ALIGN
    BUILD -- index --> ALIGN
    ALIGN -- BAM --> SORT
    SORT --> INDEX
    SORT --> FLAGSTAT
    FASTQC -- zip --> MULTIQC
    TRIM -- log --> MULTIQC
    FLAGSTAT --> MULTIQC
    INDEX -- sorted BAM + BAI --> BAMCOV
    BAMCOV -- all bigWigs --> MBWS
    MBWS --> PLOTCOR
    BAMCOV -- IP bigWigs only --> CMATRIX
    genebed --> CMATRIX
    CMATRIX --> PROFILE
    SORT --> TAGDIR
    TAGDIR -- IP + INPUT per replicate --> PEAKS
    PEAKS --> POS2BED
    POS2BED -- rep1 + rep2 BEDs --> INTERSECT
    INTERSECT --> FILTER
    blacklist --> FILTER
    FILTER --> ANNOTATE
    FILTER --> MOTIFS
    genome --> ANNOTATE
    gtf --> ANNOTATE
    genome --> MOTIFS
```


# Objective

> **Instructions:** Based on the diagram above, write a short paragraph describing the
> workflow. You can use the template from the first project as inspiration.
>
> *Delete this instruction block once you've completed this section.*

# Inputs

> **Instructions:** Describe the starting data, including:
>
> 1. How many samples?
> 2. Where and how are the samples recorded? (i.e. a samplesheet with columns named X, Y, Z, etc.)
>
> *Delete this instruction block once you've completed this section.*

# Outputs

Per Sample:




Per pipeline run:




# Pipeline Steps

> **Instructions:** Fill in one row per process in the pipeline. Derive the step list from the
> Objective and Outputs sections above. "Depends on" should name the upstream step(s) whose output
> this step consumes (used for wiring channels). Try to list only the minimum set of files needed
> for the next step. 
>
> The Example Table below is a simple worked example (not from this pipeline) showing the expected
> format: a process that downloads a genome, followed by a process that runs a script on it.
> **Delete the Example Table and this instruction block before you submit.**

## Example Table

| Step | Input type | Depends on *(sample)* |
|---|---|---|
| Download genome *(sample)* | Accession ID | - |
| Run script on genome *(sample)* | Genome FASTA | Download genome |

## Pipeline Table

| Step | Input type | Depends on |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

# Development Workflow

Every process defines a `stub:` run that produces placeholder output files. All of
the stub runs should use the name from the CSV to identify outputs by their name.

# Environment and Reproducibility
For this project, we are switching over to using Docker containers through Singularity.

> **Instructions:** Look at the [Pipeline Containers](https://github.com/bu-cds-bf528/pipeline_containers)
> repository and fill in which versions of tools were used in your pipeline.
>
> *Delete this instruction block once you've completed this section.*


| Tool | Env file | Version |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |


# Resource Requirements

| CPUs | RAM | Label | Rationale |
|---|---|---|---|
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

# Success Criteria

The stub-run correctly produces named placeholder outputs for each row in the original CSV.

# Out of Scope


# Validation Table

| Step | Parameter justification | Confidence | Validation |
|---|---|---|---|
| Adapter & quality trimming (Trimmomatic) |  |  |  |
| Alignment (Bowtie2) |  |  |  |
| Alignment QC (samtools flagstat + MultiQC) |  |  |  |
| Coverage tracks (deepTools bamCoverage) |  |  |  |
| Sample correlation (multiBigwigSummary + plotCorrelation) |  |  |  |
| Peak calling (HOMER findPeaks) |  |  |  |
| Reproducible peaks (bedtools intersect) |  |  |  |
| Blacklist filtering (bedtools intersect -v) |  |  |  |
| Peak annotation (HOMER annotatePeaks) |  |  |  |
| Motif finding (HOMER findMotifsGenome) |  |  |  |

