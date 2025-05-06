# Dissertation Analysis: Judge Ratings and Internal Structure Validity (`dissertation_analyzes.Rmd`)

## Overview

This repository contains the R Markdown script (`dissertation_analyzes.Rmd`) used for conducting key statistical analyses for the Assessment Scale for Group Music Therapy in Substance Use Disorders (MTDQ) dissertation. The script performs two main sets of analyses:

1.  **Content Validation Analysis:** Summarizes and analyzes ratings provided by expert judges on the items of the [Brief Instrument Description, e.g., assessment scale].
2.  **Internal Structure Validity Analysis:** Investigates the factor structure of the instrument using participant data via Confirmatory Factor Analysis (CFA).

## File Structure

*   **`dissertation_analyzes.Rmd`:** The main R Markdown file containing all the code and explanations for the analyses.
*   **`comp_reliability.R` (Potentially Required):** A custom R script likely containing functions to calculate specific reliability metrics (e.g., Composite Reliability). This script needs to be present in the same directory as `dissertation_analyzes.Rmd` or sourced using the correct path within the Rmd file.

## Prerequisites

To run the `dissertation_analyzes.Rmd` script successfully, you need the following:

1.  **R:** A recent version of R installed.
2.  **RStudio (Recommended):** An IDE like RStudio makes working with R Markdown files easier.
3.  **R Packages:** Install the following packages in R:
    ```R
    # Run these lines in your R console if you don't have the packages installed
    install.packages("readxl")     # For reading Excel files
    install.packages("dplyr")      # For data manipulation
    install.packages("psych")      # For descriptive statistics and reliability
    install.packages("MVN")        # For Multivariate Normality tests
    install.packages("lavaan")     # For Confirmatory Factor Analysis (CFA)
    install.packages("semTools")   # For additional SEM tools (like reliability)
    install.packages("semPlot")    # For plotting SEM models
    ```
5.  **Custom Reliability Script:** The `comp_reliability.R` file (if used by the Rmd script).

## Data

*   This repository **does not include** the raw data files (`dados.xlsx`, judge response file) due to potential privacy concerns.
*   You need to obtain these files separately and place them in a location accessible by the R script.
*   **Crucially, you MUST update the file paths** inside the `dissertation_analyzes.Rmd` script to point to the correct locations of your data files:
    *   Look for lines using `read_excel("path/to/your/file.xlsx")` and modify the path accordingly.

## Usage

1.  **Install Prerequisites:** Ensure R and all required R packages are installed.
2.  **Prepare Data:** Place your `dados.xlsx` file and the judge response Excel file in an accessible directory.
3.  **Place Custom Script:** If `comp_reliability.R` is used, ensure it's in the same directory as the Rmd file or update the `source()` path within the Rmd.
4.  **Update File Paths:** Open `dissertation_analyzes.Rmd` in RStudio or a text editor and modify the file paths within the `read_excel()` functions to match the location of your data files.
5.  **Run Analysis:** Open `dissertation_analyzes.Rmd` in RStudio. You can run the analysis by:
    *   Running individual code chunks sequentially.
    *   Using the "Run" -> "Run All" command in RStudio.
    *   Knitting the document (e.g., to HTML or PDF) which will execute all code chunks.

## Analysis Sections in `dissertation_analyzes.Rmd`

The script is organized into the following main sections:

1.  **Judge Content Validation Analysis:**
    *   Loads and prepares the judge rating data.
    *   Calculates descriptive statistics (means or frequencies) for judge responses on various items.
    *   Visualizes judge agreement/ratings using bar plots, potentially including reference lines for agreement thresholds.
    *   Analyzes specific items (like Q12, Q13 regarding comprehensibility) separately if they used different response formats.

2.  **Internal Structure Validity (CFA):**
    *   Loads and prepares the participant data (`dados.xlsx`).
    *   Performs descriptive statistics on participant demographics (age, gender).
    *   Tests for multivariate normality using Mardia's test (identifying non-normality).
    *   Fits several CFA models using the `lavaan` package with the `WLSMV` estimator (appropriate for the identified non-normal, likely ordinal data):
        *   Unidimensional (Single General Factor) Model
        *   Two Correlated Factors Model (`cog` and `com`)
        *   Orthogonal Bifactor Model (General factor + `cog` + `com`)
        *   Constrained Orthogonal Bifactor Model
    *   Evaluates model fit using standard indices (CFI, RMSEA, etc.).
    *   Calculates reliability coefficients (e.g., Cronbach's Alpha, potentially McDonald's Omega via `psych` or `semTools`, and potentially custom metrics via `comp_reliability.R`).
    *   Visualizes the factor models using `semPlot`.
    *   Compares the fit of the different CFA models.

## Outputs

The script will primarily produce output within the R console or the rendered R Markdown document, including:

*   Data summaries and descriptive statistics tables.
*   Multivariate normality test results.
*   CFA model fit statistics tables.
*   Standardized factor loadings tables.
*   Reliability coefficient estimates.
*   Bar plots summarizing judge ratings.
*   Path diagrams visualizing the fitted CFA models.
*   Model comparison results (LRT or fit index tables).
*   Session information detailing the R version and packages used.

## Important Notes

*   **File Paths:** Remember to update the paths to your data files within the `.Rmd` script.
*   **WLSMV Estimator:** The CFA uses the WLSMV estimator because the data was found to violate multivariate normality assumptions and is likely ordinal. When interpreting results, particularly fit indices, using the `.scaled` versions (e.g., `cfi.scaled`, `rmsea.scaled`) provided by `lavaan` is generally recommended for WLSMV.
*   **Model Comparison:** Comparing models estimated with WLSMV should ideally use scaled chi-square difference tests (e.g., via `anova(model1, model2)` in `lavaan`) or comparison of fit indices, rather than the standard Likelihood Ratio Test (`lavTestLRT`).
*   **`comp_reliability.R`:** The functionality of this custom script is unknown without seeing its content but is required if sourced in the Rmd.

## How to Cite

### Citing this Function/Code:
Pedrosa, F. G. (2023). Dissertation Analysis: Judge Ratings and Internal Structure Validity. Retrieved from https://github.com/FredPedrosa/dissertation_data_analyzes

## Author

*   **Prof. Dr. Frederico G. Pedrosa**
*   fredericopedrosa@ufmg.br

## License

This project is licensed under a modified version of the GNU General Public License v3.0.  
Commercial use is not permitted without explicit written permission from the author.
