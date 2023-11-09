# GCP_Batch_Nextflow
Samples for using Nextflow with GCP Batch

After install Nextflow, Create the nextflow.config. Example is provided in this repo.

Hello World example:
```
./nextflow -c nextflow.config run nextflow-io/hello -profile gbatch
```

Chipseq example:
```
./nextflow run nf-core/chipseq -profile test,gbatch --outdir output
```

Nextflow-io/rnaseq-nf example:
Update the rnaseq-nf/nextflow.config. Update the google.project, workDir, google.region
```
  gcb {
      params.transcriptome = 'gs://rnaseq-nf/data/ggal/transcript.fa'
      params.reads = 'gs://rnaseq-nf/data/ggal/gut_{1,2}.fq'
      params.multiqc = 'gs://rnaseq-nf/multiqc'
      google.project='service-hpc-project2'
      process.executor = 'google-batch'
      process.container = 'quay.io/nextflow/rnaseq-nf:v1.2.1'
      workDir = 'gs://thomashk-test2/nextflow' // <- replace with your own bucket!
      google.region  = 'us-central1-a'
  }
```
Then submit the job by 
```
./nextflow -c rnaseq-nf/nextflow.config run nextflow-io/rnaseq-nf -profile gcb
```
