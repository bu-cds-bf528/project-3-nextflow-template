# Expected Outputs by Step

Each module's `stub:` block is left empty for you to fill in. Use this table to write a
stub that creates placeholder files with `touch` or `mkdir`, then check your workflow logic
with `nextflow run main.nf -stub-run`.

`sample_id` means the sample name from the first column of the samplesheet. `rep` means the
replicate name (`rep1` or `rep2`). The exact filenames are suggestions and you can change them.
What matters is the **number** of files each step makes and whether it runs **once per sample,
once per replicate, or once in total**.

| Step | Module | Process | Runs | Files produced |
|------|--------|---------|------|----------------|
| QC | `fastqc` | `FASTQC` | per sample | `${sample_id}_fastqc.zip`, `${sample_id}_fastqc.html` |
| Trimming | `trimmomatic` | `TRIM` | per sample | `${sample_id}_trimmed.fastq.gz`, `${sample_id}_trim.log` |
| Index genome | `bowtie2_build` | `BOWTIE2_BUILD` | once | `bowtie2_index/` (directory) |
| Alignment | `bowtie2_align` | `BOWTIE2_ALIGN` | per sample | `${sample_id}.bam` |
| Sort | `samtools_sort` | `SAMTOOLS_SORT` | per sample | `${sample_id}.sorted.bam` |
| Index BAM | `samtools_idx` | `SAMTOOLS_IDX` | per sample | `${sample_id}.sorted.bam.bai` |
| Alignment stats | `samtools_flagstat` | `SAMTOOLS_FLAGSTAT` | per sample | `${sample_id}_flagstat.txt` |
| Aggregate QC | `multiqc` | `MULTIQC` | once | `multiqc_report.html` |
| Coverage tracks | `deeptools_bamcoverage` | `BAMCOVERAGE` | per sample | `${sample_id}.bw` |
| Summarize bigWigs | `deeptools_multibwsummary` | `MULTIBWSUMMARY` | once | `bw_all.npz` |
| Correlation plot | `deeptools_plotcorrelation` | `PLOTCORRELATION` | once | `correlation_plot.png` |
| Fingerprint plot | `deeptools_plotfingerprint` | `PLOTFINGERPRINT` | per sample | `${sample_id}_fingerprint.png` |
| Tag directories | `homer_maketagdir` | `TAGDIR` | per sample | `${sample_id}_tags/` (directory) |
| Peak calling | `homer_findpeaks` | `FINDPEAKS` | per replicate (IP + INPUT pair) | `${rep}_peaks.txt` |
| Peaks to BED | `homer_pos2bed` | `POS2BED` | per replicate | `${rep}_peaks.bed` |
| Reproducible peaks | `bedtools_intersect` | `BEDTOOLS_INTERSECT` | once | `repr_peaks.bed` |
| Blacklist filtering | `bedtools_remove` | `BEDTOOLS_REMOVE` | once | `repr_peaks_filtered.bed` |
| Annotate peaks | `homer_annotatepeaks` | `ANNOTATE` | once | `annotated_peaks.txt` |
| Motif finding | `homer_findmotifsgenome` | `FIND_MOTIFS_GENOME` | once | `motifs/` (directory) |
| Signal matrix | `deeptools_computematrix` | `COMPUTEMATRIX` | per IP sample | `${sample_id}_matrix.gz` |
| Signal profile | `deeptools_plotprofile` | `PLOTPROFILE` | per IP sample | `${sample_id}_signal_coverage.png` |

## Notes

- **Peak calling uses pairs.** Run `FINDPEAKS` on (IP_rep1 + INPUT_rep1) and
  (IP_rep2 + INPUT_rep2). Name the outputs by replicate (`rep1_peaks.txt`, `rep2_peaks.txt`),
  not by `sample_id`.
- **Keep the sample name with the files.** For processes that run once per sample, keep the sample
name in the record

- **Directory outputs.** In the stub, use `mkdir` for outputs that are directories
  (`bowtie2_index/`, `${sample_id}_tags/`, `motifs/`). Use `touch` for everything else.
