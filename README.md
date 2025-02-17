[![Docker](https://img.shields.io/docker/pulls/y9ch/bidseq.svg)](https://hub.docker.com/r/y9ch/bidseq)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8158036.svg)](https://doi.org/10.5281/zenodo.8158036)

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

## How to use it?

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

   _Read the [documentation](https://y9c.github.io/pseudoU-BIDseq/Step-by-step-instruction.html#define-settings-in-the-configure-file) on how to customize._

   </details>

2. **Run all the analysis by one command**:

   ```bash
   apptainer run docker://y9ch/bidseq
   ```

   <details>
       <summary>The pipeline will load configure file named `data.yaml` under the current directory.<sup>(Click to expand)</sup></summary>

   - Customized configure file with `-c` argument. (default: `data.yaml`)
   - Customized number of jobs/cores in parallel `-j` argument. (default: `48`)

   </details>

3. **View the analytics reports and filtered sites.**

   <details>
      <summary>3 folders are will be created in the working directory (default: `workspace`).<sup>(Click to expand)</sup></summary>

   <code>
   ├── align_bam
   ├── <b>report_reads</b>
   └── <b>filter_sites</b>
   </code>

   - trimming, mapping, and deduping reports are in `report_reads` folder, with key numbers in all the steps reported in one webpage<sup>([example](https://y9c.github.io/pseudoU-BIDseq/readsStats))</sup>.
   - filtered sites for &Psi; detection are in the `filter_sites` folder. These sites are only passed the _simplest filtering_, you can apply customized thresholds to them based on your data type and quality.
   - processed mapping results (_.bam_) are in `align_bam` folder. You can zoom into a location that you are interested in IGV.

   </details>

## Documentation

[Read more](https://y9c.github.io/pseudoU-BIDseq)

## Citation

- cite this software

  ```BibTex
  @misc{y_y9cpseudou-bidseq_2022,
    title = {y9c/{pseudoU}-{BIDseq}: v1.0},
    url = {https://zenodo.org/record/8158036},
    urldate = {2023-07-18},
    publisher = {Zenodo},
    author = {Ye, Chang},
    month = dec,
    year = {2022},
    doi = {10.5281/zenodo.8158036},
  }
  ```

- cite the protocol

  ```BibTex
  @article{dai2023quantitative,
  title={Quantitative sequencing using BID-seq uncovers abundant pseudouridines in mammalian mRNA at base resolution},
  author={Dai, Qing and Zhang, Li-Sheng and Sun, Hui-Lung and Pajdzik, Kinga and Yang, Lei and Ye, Chang and Ju, Cheng-Wei and Liu, Shun and Wang, Yuru and Zheng, Zhong and others},
  journal={Nature Biotechnology},
  volume={41},
  number={3},
  pages={344--354},
  year={2023},
  publisher={Nature Publishing Group US New York}
  }
  ```

- cite the method

  ```BibTex
  @article{dai_quantitative_2022,
    title = {Quantitative sequencing using {BID}-seq uncovers abundant pseudouridines in mammalian {mRNA} at base resolution},
    issn = {1087-0156},
    doi = {10.1038/s41587-022-01505-w},
    journal = {Nature Biotechnology},
    author = {Dai, Qing and Zhang, Li-Sheng and Sun, Hui-Lung and Pajdzik, Kinga and Yang, Lei and Ye, Chang and Ju, Cheng-Wei and Liu, Shun and Wang, Yuru and Zheng, Zhong and Zhang, Linda and Harada, Bryan T. and Dou, Xiaoyang and Irkliyenko, Iryna and Feng, Xinran and Zhang, Wen and Pan, Tao and He, Chuan},
    year = {2022},
    pages = {1--11},
  }
  ```

&nbsp;

<p align="center">
  <img
    src="https://raw.githubusercontent.com/y9c/y9c/master/resource/footer_line.svg?sanitize=true"
  />
</p>
<p align="center">
  Copyright &copy; 2021-present
  <a href="https://github.com/y9c" target="_blank">Chang Y</a>
</p>
<p align="center">
  <a href="https://github.com/y9c/pseudoU-BIDseq/blob/master/LICENSE">
  <img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=GPLv3&logoColor=d9e0ee&colorA=282a36&colorB=c678dd" />
  </a>
</p>
