# Proteome-Wide Association Study for UKB proteomics database

This project is created for proteome-wide association study (PWAS) on UK Biobank database

# Study Design

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Installation

```bash
# Example installation steps
git clone https://github.com/clu89/PWAS_UKB.git
setwd("PWAS_UKB")
install.packages("renv")
renv::restore() # Restores the R package environment from renv.lock
```

## Usage

```bash
## Install R first
Module load R
Rscript PWAS_UKB.R
```

## Features

- *Data cleaning and management*

Data cleaning was conducted with tidyverse

- *Calculate incidence time to enrollment*

Incidence time to enrollment is calculated by subtracting enrol_date from pneumonia_onset with difftime function as followed

analysis$pneumonia_ite <- difftime(as.Date(analysis$pneumonia_onset), as.Date(analysis$enrol_date), unit = "days")

- *Linear model construction*
1. Input data should contain exposure variable, covariates, and all columns for proteomics data
2. Proteomics data matrix should only contain all columns for proteomics data
3. Mode specifies the exposure variable and plot layout
4. The exported table (PWAS result) should contain protein, beta coefficient, standard error, raw p-value, and Bonferroni-adjusted p-value

lm_pro(data = data, protein = proteomics_data_matrix, mode = "full", fill = "file_name")

Output:

[Insert top 20 associated proteins table]

- *Volcano plot*
1. Volcano plot serves as a visualization tool to indicate p-value distribution of associated proteins against beta coefficients
2. Input data is the PWAS result table
3. The output of this function is a scatter plot with upregulated proteins highlighted in red while downregualted proteins highlighted in blue
4. Protein name of the top associations are attached nearby

Volcano(data = PWAS_data, file = "file_name")

Output:

[Insert a volcano plot here]

- *GSEA analysis*
1. GSEA analysis interpret the biological functions of proteins from PWAS result
2. Top associated proteins are ranked according to the product of the sign of beta coefficient and -log10 transformed raw p-value
3. msig_collection and subcollection specifies the collection of pathways that will be used for the analysisin humans
4. database specifies which database will be used (ex. KEGG, GO, etc.)
5. range defines the number of pathways that will be plotted in the inverted bar chart
6. All pathways were ranked by FDR-adjusted p-values

GSEA(data = PWAS_data, msig_collection = , subcollection, database, range)

[Insert a GSEA plot here]

- Correlation analysis
# Correlation plot
## Correlation plot compares the beta coefficient across different models (full vs short pneumonia ITE)
## Correlation plot contains pearson correlation coefficient, reference line, regression line and all the proteins association plotted in scatter plot

## Configuration

Describe any configuration options or environment variables.

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

For questions or support, contact [your.email@example.com](mailto:your.email@example.com).
