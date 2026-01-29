# DHFR Mutation Analysis Project

## Project Overview
This project analyzes DHFR (Dihydrofolate Reductase) resistance markers in malaria parasites, specifically examining three key mutations: Asn51Ile, Cys59Arg, and Ser108Asn.

## Discussion Summary

### Initial Brainstorming Phase

**Objective:** Create a script to analyze DHFR mutation data from `dhfr_prevalences_input_table_1.csv` and produce visualizations similar to `dhfr_no_het.png`.

**Data Understanding:**
- **Sample IDs** from different populations (MSY, PCD, PK3W, PK4W, PK5W, ND)
- **Three mutations**: Asn51Ile, Cys59Arg, Ser108Asn
- **Values**: 1 (mutation present), 0 (wild type), or missing/empty
- **"no_het"** means "no heterozygous" - treating only as present (1) or absent (0)

**Proposed Analyses:**

1. **Mutation Prevalence**
   - Calculate % of samples with each mutation
   - Bar chart showing prevalence of Asn51Ile, Cys59Arg, Ser108Asn

2. **Haplotype/Mutation Combinations**
   - Identify common patterns (e.g., triple mutant 1-1-1, double mutants, wild type 0-0-0)
   - Frequency of each combination
   - Stacked or grouped bar chart

3. **Prevalence by Population**
   - Compare mutation frequencies across MSY, PCD, PK3W, PK4W, PK5W, ND groups

4. **Heatmap**
   - Visual representation of mutation patterns across all samples
   - Color-coded presence/absence

**Data Handling Decisions:**
- Exclude samples with any missing mutation values
- Focus on complete mutation profiles only
- Count combinations as separate haplotypes

### Package Requirements

**Essential packages installed:**
```bash
pip install pandas matplotlib seaborn
```

**Package versions (from requirements.txt):**
- pandas==3.0.0
- matplotlib==3.10.8
- seaborn==0.13.2
- numpy==2.4.1

**Why these packages:**
- `pandas` - for reading and manipulating CSV data
- `matplotlib` - for creating plots and visualizations
- `seaborn` - for enhanced statistical visualizations
- `numpy` - for numerical operations

### Implementation Steps

The analysis notebook includes the following sections:

1. **Load and Explore Data**
   - Read CSV file
   - Display basic information about the dataset
   - Check for missing values

2. **Data Cleaning and Preparation**
   - Remove samples with incomplete mutation data
   - Convert mutation columns to integers
   - Report number of samples excluded

3. **Calculate Individual Mutation Prevalence**
   - Calculate percentage of samples with each mutation
   - Create prevalence summary dataframe

4. **Calculate Haplotype Frequencies**
   - Create haplotype strings (e.g., "1-1-1" for triple mutant)
   - Count frequency of each haplotype
   - Add descriptive names to haplotypes:
     - `1-1-1`: Triple Mutant (51I+59R+108N)
     - `0-0-0`: Wild Type
     - `0-1-1`: Double Mutant (59R+108N)
     - `1-0-1`: Double Mutant (51I+108N)
     - And others...

5. **Visualization: Haplotype Prevalence Bar Chart**
   - Create bar chart showing haplotype distribution
   - Include count and percentage labels
   - Save as `RESULTS/dhfr_no_het.png`

6. **Additional Visualization: Individual Mutation Prevalence**
   - Bar chart for each individual mutation
   - Color-coded bars
   - Save as `RESULTS/dhfr_individual_mutations.png`

7. **Summary Statistics**
   - Print comprehensive summary of analysis
   - Include total samples, exclusions, and all prevalence data

8. **Combined Visualization: Haplotype Distribution with Mutation Matrix**
   - Top panel: Bar chart of haplotype counts with color coding
     - Orange for triple mutant (1-1-1)
     - Black for double mutants
     - Green for wild type (0-0-0)
   - Bottom panel: Multi-component visualization
     - Left: Red hatched bars showing wild type counts per mutation
     - Middle: Mutation labels with prevalence percentages
     - Right: Dot plot matrix showing mutation patterns
   - Save as `RESULTS/dhfr_no_het_combined.png`

## Project Structure

```
JULIEN_YANOGO/
├── index.ipynb                          # Main analysis notebook
├── README.md                            # This file
├── requirements.txt                     # Python dependencies
├── DATA/
│   ├── csv/
│   │   └── dhfr_prevalences_input_table_1.csv  # Input data
│   └── images/                          # Reference images
└── RESULTS/                             # Output visualizations
    ├── dhfr_no_het.png                  # Haplotype bar chart
    ├── dhfr_individual_mutations.png    # Individual mutation chart
    └── dhfr_no_het_combined.png         # Combined visualization
```

## Data Description

**Input file:** `DATA/csv/dhfr_prevalences_input_table_1.csv`

**Columns:**
- `Sample ID`: Unique identifier for each sample
- `Asn51Ile`: Mutation at position 51 (0=wild type, 1=mutant)
- `Cys59Arg`: Mutation at position 59 (0=wild type, 1=mutant)
- `Ser108Asn`: Mutation at position 108 (0=wild type, 1=mutant)

**Sample populations:**
- MSY: Population prefix
- PCD: Population prefix  
- PK3W, PK4W, PK5W: Population prefixes
- ND: Population prefix

## How to Run the Analysis

### Option 1: Standard Python Environment

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Open the notebook:**
   ```bash
   jupyter notebook index.ipynb
   ```
   Or open in VS Code

3. **Run all cells sequentially** (Cell 1 through Cell 16)

4. **Check outputs:**
   - Visualizations will be saved in `RESULTS/` folder
   - Summary statistics will be printed in the notebook

### Option 2: Anaconda Environment

1. **Create a new conda environment (recommended):**
   ```bash
   conda create -n dhfr_analysis python=3.11
   conda activate dhfr_analysis
   ```

2. **Install packages using conda:**
   ```bash
   conda install pandas matplotlib seaborn numpy jupyter
   ```
   
   Or using pip within conda environment:
   ```bash
   pip install pandas matplotlib seaborn numpy jupyter
   ```

3. **Install packages directly in Jupyter Notebook:**
   
   Add and run this cell at the beginning of the notebook:
   ```python
   # Install required packages (run once)
   import sys
   !{sys.executable} -m pip install pandas matplotlib seaborn numpy
   ```
   
   Or using conda in notebook:
   ```python
   # Install using conda (run once)
   import sys
   !conda install --yes pandas matplotlib seaborn numpy
   ```

4. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook index.ipynb
   ```
   
   Or from Anaconda Navigator:
   - Launch Jupyter Notebook
   - Navigate to project folder
   - Open `index.ipynb`

5. **Run all cells sequentially** (Cell 1 through Cell 16)

6. **Check outputs:**
   - Visualizations will be saved in `RESULTS/` folder
   - Summary statistics will be printed in the notebook

## Key Findings

The analysis reveals:
- **Individual mutation prevalence** for each of the three DHFR mutations
- **Haplotype distribution** showing the most common mutation combinations
- **Triple mutant (1-1-1)** typically represents the highest prevalence
- **Wild type (0-0-0)** and various double mutant combinations at lower frequencies

## Visualization Outputs

1. **dhfr_no_het.png**: Simple bar chart showing haplotype prevalence
2. **dhfr_individual_mutations.png**: Bar chart showing individual mutation rates
3. **dhfr_no_het_combined.png**: Comprehensive visualization combining:
   - Haplotype count distribution
   - Wild type vs mutant counts per mutation
   - Dot matrix showing mutation patterns

## Technical Notes

- Missing data is excluded from analysis
- Only samples with complete mutation data (all three mutations) are included
- Haplotypes are defined as unique combinations of the three mutations
- Visualizations use color coding to distinguish mutation patterns
- All plots are saved at 300 DPI for publication quality

## Author

Analysis developed for Julien Yanogo's research project on antimalarial resistance markers.

## Date

January 28-29, 2026
