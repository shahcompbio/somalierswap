# shahcompbio/somalierswap: Changelog

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v1.0.0 - 2026-03-22

Initial release of shahcompbio/somalierswap, created with the [nf-core](https://nf-co.re/) template.

### `Added`

- Pipeline built from nf-core/tools template v3.5.2
- `SOMALIER_EXTRACT` — extracts somalier fingerprint sites from input BAM files
- `SOMALIER_RELATE` — computes pairwise relatedness between samples within each subject group to detect potential sample swaps
- MultiQC report aggregating somalier relatedness results
- Samplesheet input with `subject`, `sample`, `bam`, and `bai` columns
- Support for Docker, Singularity, Apptainer, Podman, Conda, and Wave container profiles
- nf-test integration for automated testing
