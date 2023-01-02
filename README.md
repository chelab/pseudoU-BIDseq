[![Docker](https://img.shields.io/docker/pulls/y9ch/bidseq.svg)](https://hub.docker.com/r/y9ch/bidseq)

# &Psi;-BID-seq

## Overview of the workflow

<p align="center">
  <a href="https://y9c.github.io/pseudoU-BIDseq/Overall-Workflow#gh-light-mode-only">
    <img src="./docs/scheme.svg" />
  </a>
  <a href="https://y9c.github.io/pseudoU-BIDseq/Overall-Workflow#gh-dark-mode-only">
    <img src="./docs/scheme_dark.svg" />
  </a>
</p>

## How to use?

A [docker image](https://hub.docker.com/r/y9ch/bidseq) containing the source code and dependencies has been published for reproducibility. You can run it using the [apptainer](https://apptainer.org/help) container runtime.

The entire analysis can be completed in just three steps:

1. **Specific the path of references (_.fasta_) and samples (_.fastq_) in a configure file (_.YAML_).**

   <details>
     <summary><code>data.yaml</code> for example<sup>(Click to expand)</sup></summary>

   ```yaml
   reference:
     contamination:
       fa: ./ref/contamination.fa
     genes:
       fa: ./ref/genes.fa
     genome:
       fa: /data/reference/genome/Mus_musculus/GRCm39.fa
       star: /data/reference/genome/Mus_musculus/star/GRCm39.release108

   samples:
     mESCWT-rep1-input:
       data:
         - R1: ./test/IP16.fastq.gz
       group: mESCWT
       treated: false
     mESCWT-rep1-treated:
       data:
         - R1: ./test/IP4.fastq.gz
       group: mESCWT
       treated: true
     mESCWT-rep2-treated:
       data:
         - R1: ./test/IP5.fastq.gz
       group: mESCWT
       treated: true
   ```

   You can copy and edit from this [template](test/data.yaml).

   _Read the [documentation](https://y9c.github.io/pseudoU-BIDseq/Run-the-pipeline.html#refer-rawdata-and-references-in-the-configuration-file) on how to customize._

   </details>

2. **Run all the analysis by one command**:

   ```bash
   apptainer run docker://y9ch/bidseq:v1
   ```

    <details>
      <summary>default settings<sup>(Click to expand)</sup></summary>

   - default config file: `data.yaml`
   - default output dir: `./workspace`
   - default jobs in parallel: `48`

   _Read the [documentation](https://y9c.github.io/pseudoU-BIDseq/Run-the-pipeline.html#customized-analysis-parameters) on how to customize._

   </details>

3. **View the analytics report and pileup table.**

    <details>
      <summary>output files in working directory.<sup>(Click to expand)</sup></summary>

   - trimming, mapping, deduping reports are in `report_reads` folder, with key numbers in all the steps reported in one webpage<sup>([example](https://y9c.github.io/pseudoU-BIDseq/readsStats.html))</sup>.
   - deleted sites for &Psi; sites detection are in `pileup_adjusted` folder
   </details>

## Documentation

(**⚠ Not yet published.**)

...

[Read more](https://y9c.github.io/pseudoU-BIDseq)

## Citation

- Dai Q. _et al_. Quantitative sequencing using BID-seq uncovers abundant pseudouridines in mammalian mRNA at base resolution. Nat Biotechnol (2022). https://doi.org/10.1038/s41587-022-01505-w

&nbsp;

<p align="center">
  <img
    src="https://raw.githubusercontent.com/catppuccin/catppuccin/dev/assets/footers/gray0_ctp_on_line.svg?sanitize=true"
  />
</p>
<p align="center">
  Copyright &copy; 2021-present
  <a href="https://github.com/y9c" target="_blank">Chang Y</a>
</p>
<p align="center">
  <a href="https://github.com/y9c/pseudoU-BIDseq/blob/master/LICENSE"
    ><img
      src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=GPLv3&logoColor=d9e0ee&colorA=282a36&colorB=c678dd"
  /></a>
</p>
