# Project 3 Nextflow Template

For this project, remember to keep in a few things:

You can find the general directions here: https://bu-bioinfo.github.io/bf528/projects/project_3_report/

1. Most of the required references and files can be found in your `nextflow.config`

2. Make sure you give each process a label to request an appropriate amount of resources

3. Use the singularity containers provided on the website directions for the project

4. Each module is a blank process that uses Nextflow static typing (`nextflow.enable.types = true`). The `stub:` block
is left empty. Fill it in so you can check your workflow logic with `-stub-run`.
- See `EXPECTED_OUTPUTS.md` for the files each step should produce and whether it runs per sample, per replicate, or once

5. Use the subsampled data to start out with - you may need to eventually switch to the full data before your
pipeline is technically complete as sometimes peak calling may fail if not given enough input reads. 
- When the pipeline is working, change the `params` value in the original channel to the params encoding the
location of the full_samplesheet.csv

6. To remove regions using the blacklist, there are optional flags available in the `bedtools intersect` command

7. Use the provided jupyter notebook for your findings and plots

You may use any resource available to you as long as you validate what your workflow is doing and understand
the key choices made during the analysis. You can copy old workflow modules or publicly available ones or have
an LLM assist you in writing it. 

The `specifications.md` is meant to help you organize and think about which steps need to be reviewed in your pipeline.