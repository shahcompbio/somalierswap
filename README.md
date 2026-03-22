# shahcompbio/somalierswap

[![Open in GitHub Codespaces](https://img.shields.io/badge/Open_In_GitHub_Codespaces-black?labelColor=grey&logo=github)](https://github.com/codespaces/new/shahcompbio/somalierswap)
[![GitHub Actions CI Status](https://github.com/shahcompbio/somalierswap/actions/workflows/nf-test.yml/badge.svg)](https://github.com/shahcompbio/somalierswap/actions/workflows/nf-test.yml)
[![GitHub Actions Linting Status](https://github.com/shahcompbio/somalierswap/actions/workflows/linting.yml/badge.svg)](https://github.com/shahcompbio/somalierswap/actions/workflows/linting.yml)[![Cite with Zenodo](http://img.shields.io/badge/DOI-10.5281/zenodo.XXXXXXX-1073c8?labelColor=000000)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![nf-test](https://img.shields.io/badge/unit_tests-nf--test-337ab7.svg)](https://www.nf-test.com)

[![Nextflow](https://img.shields.io/badge/version-%E2%89%A525.04.0-green?style=flat&logo=nextflow&logoColor=white&color=%230DC09D&link=https%3A%2F%2Fnextflow.io)](https://www.nextflow.io/)
[![nf-core template version](https://img.shields.io/badge/nf--core_template-3.5.2-green?style=flat&logo=nfcore&logoColor=white&color=%2324B064&link=https%3A%2F%2Fnf-co.re)](https://github.com/nf-core/tools/releases/tag/3.5.2)
[![run with conda](http://img.shields.io/badge/run%20with-conda-3EB049?labelColor=000000&logo=anaconda)](https://docs.conda.io/en/latest/)
[![run with docker](https://img.shields.io/badge/run%20with-docker-0db7ed?labelColor=000000&logo=docker)](https://www.docker.com/)
[![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c.svg?labelColor=000000)](https://sylabs.io/docs/)
[![Launch on Seqera Platform](https://img.shields.io/badge/Launch%20%F0%9F%9A%80-Seqera%20Platform-%234256e7)](https://cloud.seqera.io/launch?pipeline=https://github.com/shahcompbio/somalierswap)

## Introduction

**shahcompbio/somalierswap** is a bioinformatics pipeline for detecting sample swaps in BAM files using [somalier](https://github.com/brentp/somalier). It accepts a samplesheet of BAM files organized by subject (e.g., tumor/normal pairs), extracts genomic fingerprints at known polymorphic sites, and computes pairwise relatedness within each subject group to identify unexpected sample relationships.

Pipeline steps:

1. Extract somalier fingerprints from BAM files ([`somalier extract`](https://github.com/brentp/somalier))
2. Compute pairwise relatedness within subject groups ([`somalier relate`](https://github.com/brentp/somalier))
3. Aggregate and visualize relatedness results ([`MultiQC`](http://multiqc.info/))

## Usage

> [!NOTE]
> If you are new to Nextflow and nf-core, please refer to [this page](https://nf-co.re/docs/usage/installation) on how to set-up Nextflow. Make sure to [test your setup](https://nf-co.re/docs/usage/introduction#how-to-run-a-pipeline) with `-profile test` before running the workflow on actual data.

First, prepare a samplesheet with your input data that looks as follows:

`samplesheet.csv`:

```csv
subject,sample,bam,bai
patient1,tumor,/path/to/patient1_tumor.bam,/path/to/patient1_tumor.bam.bai
patient1,normal,/path/to/patient1_normal.bam,/path/to/patient1_normal.bam.bai
```

Each row represents a BAM file for one sample. The `subject` column groups samples together for relatedness analysis — all samples sharing the same `subject` value will be compared to each other.

Now, you can run the pipeline using:

```bash
nextflow run shahcompbio/somalierswap \
   -profile <docker/singularity/.../institute> \
   --input samplesheet.csv \
   --outdir <OUTDIR> \
   --fasta /path/to/reference.fasta \
   --fai /path/to/reference.fasta.fai \
   --sites /path/to/somalier_sites.vcf.gz
```

> [!WARNING]
> Please provide pipeline parameters via the CLI or Nextflow `-params-file` option. Custom config files including those provided by the `-c` Nextflow option can be used to provide any configuration _**except for parameters**_; see [docs](https://nf-co.re/docs/usage/getting_started/configuration#custom-configuration-files).

For more details, see the [usage documentation](docs/usage.md) and the [output documentation](docs/output.md).

## Credits

shahcompbio/somalierswap was originally written by Asher Preska Steinberg.

## Contributions and Support

If you would like to contribute to this pipeline, please see the [contributing guidelines](.github/CONTRIBUTING.md).

## Citations

An extensive list of references for the tools used by the pipeline can be found in the [`CITATIONS.md`](CITATIONS.md) file.

This pipeline uses code and infrastructure developed and maintained by the [nf-core](https://nf-co.re) community, reused here under the [MIT license](https://github.com/nf-core/tools/blob/main/LICENSE).

> **The nf-core framework for community-curated bioinformatics pipelines.**
>
> Philip Ewels, Alexander Peltzer, Sven Fillinger, Harshil Patel, Johannes Alneberg, Andreas Wilm, Maxime Ulysse Garcia, Paolo Di Tommaso & Sven Nahnsen.
>
> _Nat Biotechnol._ 2020 Feb 13. doi: [10.1038/s41587-020-0439-x](https://dx.doi.org/10.1038/s41587-020-0439-x).
