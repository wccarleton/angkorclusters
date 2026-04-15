# Project
## Overview
This repo contains the data and code used for the study presented in the following paper:

[*Comparative spatial analysis reveals important structural similarities between ancient Angkor and Late Anglo-Saxon Hampshire*]()

## Abstract
Angkor (800-1450 CE) is considered the type-site for “low-density agrarian urbanism”, a loosely defined archaeological label used to describe settlements with urban traits but dispersed spatial structure. Angkor’s abandonment from the 15th century has fueled concerns that low-density cities, now common globally, may be inherently unstable. The spatial distinctiveness of Angkor relative to other pre-modern rural-urban systems, however, has never been quantitatively tested. Using ChronoCluster, a Python package for novel spatiotemporal archaeological analysis, we compared Angkor’s spatial structure to that of Anglo-Saxon Hampshire as recorded in the Domesday survey (mid-11th century CE), a rural-urban system not described as low-density agrarian urbanism. Surprisingly, both cases showed similar multiscale spatial clustering. Despite their different appearances, they may reflect scaled variants of the same underlying urban-rural dynamics. This targeted comparison between the “low-density” type-site and a non-low-density comparator challenges the idea that low-density cities like Angkor form a distinct type, raises questions about what drives variation in urban form across time and space, and opens new questions about the impact of spatial structure on urban sustainability.

## Software
The scripts and notebooks contained in this repository are intended for replication efforts and to improve the transparency of research. They are, of course, provided without warranty or technical support. That said, questions about the code can be directed to me, Chris Carleton, at ccarleton@protonmail.com.

### Python
This analysis described in the associated manuscript was performed in using Python in VS Code with a Jupyter Notebook. It also heavily used a new package called [ChronoCluster](https://wccarleton.me/chronocluster/). The version of ChronoCluster relevant to this repository and the associated paper has been archived with Zenodo and can be referenced as follows:

Carleton and Song. (2025). wccarleton/chronocluster: Initial Release (v0.1.0). Zenodo. https://doi.org/10.5281/zenodo.15342410

### Reproduction
To reproduce the analyses described in the associated paper, follow the steps below.

#### 1. Create the conda environment
Use the `environment.yml` file located in the `Src` directory to create the required environment:

```bash
cd Src
conda env create -f environment.yml
conda activate <env-name>
```

> Replace `<env-name>` with the name specified in `environment.yml`.

---

#### 2. Install local dependencies (if required)
If the project depends on local packages (e.g., `chronocluster`), install them after activating the environment:

```bash
pip install -e .
```

or, if installing from GitHub:

```bash
pip install git+https://github.com/wccarleton/chronocluster.git
```

---

#### 3. Render the analysis notebook
Use Quarto to render the main analysis notebook:

```bash
cd Src
quarto render analysis.ipynb
```

This will:

- execute the notebook (unless `--execute=false` is specified)
- generate a PDF of the Supplementary Information
- (optionally) produce intermediate LaTeX files if `keep-tex: true` is set

---

#### 4. Output location
By default, output files (e.g., `.pdf`, `.tex`, figures) are written either:

- to the notebook directory (`Src/`), or  
- to a specified output directory (e.g., `Supplement/`) if configured

---

#### 5. Optional: skip re-execution
If the notebook has already been executed and you only want to regenerate the PDF:

```bash
quarto render analysis.ipynb --execute=false
```

---

#### 6. Requirements
Ensure the following are installed:

- Conda (Miniconda or Anaconda)
- Quarto (`quarto --version`)
- A LaTeX distribution (e.g., TeX Live)

```bash
quarto --version
pdflatex --version
```

---

#### Notes
- Some steps (e.g., model fitting) may be computationally intensive and take several minutes to complete.
- Output formatting (tables, figures) depends on the LaTeX preamble (`preamble.tex`) included in the project.
- Minor differences in numerical results may occur depending on system and library versions.

### Archive
This repository has been archived with Zenodo for replication and review. It may be updated after peer review of the associated paper and any updates will be reflected by repo releases that will be automatically archived with versioning. The history can be tracked on Zenodo as well and this repo referenced as follows:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15371728.svg)](https://doi.org/10.5281/zenodo.15371728)

## Contact
[ORCID](https://orcid.org/0000-0001-7463-8638) |
[Google Scholar](https://scholar.google.com/citations?hl=en&user=0ZG-6CsAAAAJ) |
[Website](https://wccarleton.me)

## License
Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
