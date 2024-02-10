## System requirements
- Software dependencies:
  - Windows/Linux/Mac OS (tested on Windows 10)
  - R (>=4.0.0; tested on 4.3.1)
  - Seurat (>=5.0.0; tested on 5.0.0)

## Installation
- R can be downloaded here: https://www.r-project.org/. We recommend R studio for easier data exploration: https://www.rstudio.com/categories/rstudio-ide/. (~5 minutes)
- Seurat can be installed here (~5 minutes)
- LAD does not require installation. It can be run directly by loading it with `source("R/lad_seurat.R")` and run with `RunALT` (see examples for details).

## Examples
| Dataset  | Item                               | File                                                |
|----------|------------------------------------|-----------------------------------------------------|
|          |Implementation of BCD for Seurat    |bcd_seurat.R                                         |
|          |                                    |                                                     |
|	   |BCD and Euclidean			|simulation.Rmd/nb.html                               |
|Simulation|Seurat integration		 	|simulation_seurat_integration.Rmd/nb.html            |
|	   |Harmony				|simulation_harmony_integration.Rmd/nb.html           |
|          |                                    |                                                     |
|	   |BCD and Euclidean			|gse118614_10x_all.Rmd/nb.html                        |
| Retina   |Seurat integration			|gse118614_10x_all_seurat_integration.Rmd/nb.html     |
|	   |Harmony				|gse118614_10x_all_harmony_integration.Rmd/nb.html    |
|          |                                    |                                                     |
|	   |BCD and Euclidean			|gse145926.Rmd/nb.html                                |
| Covid-19 |Seurat integration			|gse145926-seurat-integration.Rmd/nb.html             |
|	   |Harmony				|gse145926-harmony.Rmd/nb.html                        |
|          |                                    |                                                     |
|	   |BCD and Euclidean			|lung.Rmd/nb.html                                     |
| Lung	   |Seurat integration			|lung_seurat_integration.Rmd/nb.html                  |
|	   |Harmony				|lung_harmony_integration.Rmd/nb.html                 |

## Data
Processed data for the Lung example can be found [here](https://drive.google.com/drive/folders/1-Fh9ZYkXAiwcr-RXvtzHaCtNThXFg72X?usp=drive_link).
