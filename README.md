# Empirical Pricing Kernel Models and the Permanent-Transitory Decomposition via Machine Learning

**Title**:               Double Degree Thesis for M.A. in Banking and Finance (MBF) and MSc. in Finance (MFIN)  
**Institutions**:        University of St. Gallen (HSG) and Stockholm School of Economics (SSE)  
**Author**:              Andreas Karlsson  
**Supervisor (SSE)**:    Prof. Gualtiero Azzalini  
**Supervisor (HSG)**:    Prof. David Preinerstorfer  
**Co-supervisor (HSG)**: Dr. Zeno Adams  

## README Outline

This README file is separated into 11 sections:

1. Introduction
2. Preliminaries
3. Overview of Input Files
4. Full paper replication
5. Where to find paper outputs

## 1. Introduction [TBU]

Description of replication files for the thesis "Empirical Pricing Kernel Models and the Permanent-Transitory Decomposition via Machine Learning".

[Write intro]



## 2. Preliminaries

This section describes the technical specifications used in the thesis. To ensure full replication, please ensure that the same versions of imported packages are forced to be specified to exactly what is stated here as the results may vary on package version and the compatibility across packages.

#### 2.1 Operating System

- Operating system: Windows 10.0.20348
- CPU: Intel(R) Xeon(R) Gold 6132 CPU @ 2.60GHz

#### 2.2 STATA 

The following specifications (versions) of STATA and STATA packages were used for this project:
- STATA/MP (18.0)
- estout (3.31)
- tab2xl (1.0.5)
- reghdfe (6.12.3)
- ftools (2.49.1)
- sxpose (1.0.0)
- listtab (Nov 4th, 2012)
- texsave (1.6.1)
- mdesc (2.1)
- winsor (1.3.0)
- winsor2 (1.1)
- carryforward (4.5)
- rangestat (1.1.1)

*NOTE: if a package is not installed on the computer, you need to install the module first*. 

#### 2.3 PYTHON

The following specifications (version) were used for this project:

- Python (3.11.5)
- IDE: Jupyter Notebook (6.5.4)
- Pandas (2.0.3)
- Numpy (1.24.3)
- statsmodels (0.14.0)
- graphviz (0.20.1)
- matplotlib (3.7.2)
- scipy (1.11.1)
- sklearn (1.3.0)
- linearmodels (5.3)
- IPython version (8.15.0)
- simple_colors (0.1.5)
- import_ipynb (0.1.4)
- Tensorflow & Keras (2.14.0)
- seaborn (0.12.2)
- [need stuff for the plot_model]

*NOTE: if a package is not installed on the computer, you need to install the module first*. 

## 3. Overview of Input Files [TBU]

#### 3.1 Raw Input Data [TBU]

##### 3.1.1 Firm Accounting Data [TBU]

##### 3.1.2 Firm Market Data [TBU]

##### 3.1.3 Exchange Rates [TBU]

##### 3.1.4 Interest Rates [TBU]

##### 3.1.5 Other Data [TBU]
- Time-Series Death

[**brief description**]

#### 3.2 Cleaned Input Data [TBU]

##### 3.2.1 Cleaned Firm Characterstics [TBU]

##### 3.2.2 Cleaned Return Data [TBU]

##### 3.2.3 Cleaned Mask [TBU]

##### 3.2.4 Bond Data [TBU]

[**brief description about importing with Python**]

## 4. Full Paper Replication [TBU]

### 4.1 STATA Data Cleaning Replication

The first step of the replication is to change the path in the STATA master .do file ("Master.do") for the STATA code, see image below. Change this path to the directory where the entire project is stored. All other folder paths are set relative to this path so make sure it's correctly specified. The master file is located in the "Library" folder and all other subfolders are located in the "Library/Code" folder. 

![Alt text](image/replication_setup.png)

After having completed this step, the user can replicate the entire data cleaning procedure by running the master file. Running the master file ensures all sub-programs are executed in the correct and intended order. This process takes the raw input files stored in the "Input" folder and stores cleaned datasets in the "Output" folder (more specifically, the "Output/Temporary" folder). These output files are to be used for machine learning estimation using Python at the next stage. Because of this, the user must ensure full write permissions locally. In detail, this STATA data cleaning process follows 3 overall steps:

#### 4.1.1 Cleaning Input Data

All programs located in the "FCC1_Company_List" folder are related to the importation and cleaning of the underlying firm-level accounting and market data.

- **FCC1_0**: Runs all .do files in the folder "FCC1_Company_List"
- **FCC1_1**: Imports additional Refinitiv Eikon firm data that was omitted by the author in the first data downloading process
- **FCC1_2**: Imports and cleans FX variables
- **FCC1_3**: Imports and cleans risk-free rates
- **FCC1_4**: Imports and cleans gross profit for all firms
- **FCC1_5**: Imports and cleans dividend yield for all firms
- **FCC1_6**: Imports and cleans accounting and market data for delisted firms
- **FCC1_7**: Imports and cleans shareholder's equity for all firms
- **FCC1_8**: Consolidates all firm-level accounting data for all firms
- **FCC1_9**: Consolidates all firm-level accounting and market data for all firms

*Detailed descriptions of the code is left to in-program comments*

#### 4.1.2 Creating Firm Characteristics

All programs located in the "FCC2_Create_Firm_Chars" folder are related to building the information set of *firm* characteristics $I_{t,i}$ and the macroeconomic information set relating to the *firm* characteristics $I_t$

- **FCC2_0**: Runs all .do files in the folder "FCC2_Create_Firm_Chars"
- **FCC2_1**: Creates the auxiliary metrics from firm-level data required for constructing the complete firm characteristics later
- **FCC2_2**: Creates 41 of 46 total firm characteristics, masked and unmasked
- **FCC2_3**: Creates final 5 firm characteristics, masked and unmasked
- **FCC2_4**: Combines firm characteristic dataset and performs quantile-normalization (QN) of firm characteristics
- **FCC2_5**: Creates macroeconomic information set by aggregating firm characteristics and performing stationarity transformations

*Detailed descriptions of the code is left to in-program comments*

#### 4.1.3 Cleaning and Creating Bond Characteristics

All programs located in the "FCC3_Bond_Chars" folder are related to building the information set of *bond* characteristics $I_{t,b}^{(b)}$ and the macroeconomic information set relating to the *bond* characteristics $I_t^{(b)}$

- **FCC3_0**: Runs all .do files in the folder "FCC3_Bond_Chars"
- **FCC3_1**: Imports and initial cleans underlying bond time series data
- **FCC3_2**: Further cleaning of bond time series data
- **FCC3_3**: Adjust bond data for currency differences
- **FCC3_4**: Create bond characteristics
- **FCC3_5**: Combines bond characteristics and lags by 9 weeks
- **FCC3_6**: Performs quantile-normalization (QN) of bond characteristics
- **FCC3_7**: Creates macroeconomic information set by aggregating bond characteristics and performing stationarity transformations

*Detailed descriptions of the code is left to in-program comments*

### 4.2 Python Machine Learning Replication

The Python code is stored in a notebook format (.ipynb) for easier user understanding. In particular, text and LaTeX code is rendered within the notebook to give detailed descriptions of what goes on within each section of the code. I reference to these specific descriptions for users looking for in depth explanations of blocks of code. Furthermore, there are also within-code comments for code-line specific explanations. The code is combined into a single file, and is to be run from top to bottom. Naturally, this has to be done *after* the STATA cleaning procedure has been completed as the Python code refers to outputs from the data cleaning procedure. After the user has ensured that the machine is compatible with all the package-specifications in section 2.3, the user needs to again set the project directory (PROJ_DIR) in the Python code. This needs to be the same project directory as specified previously for the STATA master file:

![Alt text](image/replication_setup_python.PNG)

After the user changes the project directory path to the correct local path, run the code from top to bottom to replicate the results. All paper outputs will be stored in the "Output/Results" folder locally. Therefore, full replicability also requires write permissions from local. 

The code has [**insert number of sections in python code here**] sections of code in total, each performing different tasks. [**continue**]

- **Section 1: Reproducibility, Delimitation and Paper Colors**:
    - (1.1) Creates seed-functionality for reproducible machine learning estimations.
    - (1.2) Specifies all relevant folder paths and the dates delimiting the training-validation-test split used.
    - (1.3) Creates firm characteristic category labels and defines the primary colors (hexidecimal) for figure outputs.
    - (1.4) Selects study period and specifies select parameters: e.g. LSTM lookback period and number of moment conditions for the GAN-type models. 
- **Section 2: Python Preliminaries and Packages**:
    - (2.0) Imports required packages for the machine learning estimation.
    - (2.1) Prints versions of packages so user can cross-check compatibility to the required package versions stated in this paper.
- **Section 3: Import Data**: [TBU]
- **Section 4: Model Building**: [TBU]

## 5. Where to find paper outputs

This section describes which files produced by the Python code corresponds to which output in the final paper. *All* output figures are stored as .pdf files in subfolders within the "Output/Results" folder. Likewise, *all* output tables are stored as LaTeX files (.tex) in subfolders within the "Output/Results" folder. Therefore, I am detailing here the filenames of each .pdf and .tex files that correspond to each Figure and Table in the paper here. The user can then find where in the code this file is created, and the procedure going into producing these outputs.

### 5.1 Table Outputs

| Name           | Description        |
|:---------------|:-------------------|
| **Table I**    | main_table_v240425.tex                   |
| **Table II**   |                    |
| **Table III**  |                    |
| **Table A7**   | (**Non-empirical output**) Parts 1-3 Created using LaTeX |
| **Table A8**   | (**Non-empirical output**) Created using LaTeX           |
| **Table A9**   | (**Non-empirical output**) Parts 1-2 Created using LaTeX |
| **Table A10**  | (**Non-empirical output**) Parts 1-2 Created using LaTeX |
| **Table A11**  | (**Non-empirical output**) Created using LaTeX           |
| **Table A20**  | (**Non-empirical output**) Created using LaTeX           |

### 5.2 Figure Outputs

| Name            | Description                                           |
|:----------------|:------------------------------------------------------|
| **Figure I**    | (**Non-empirical output**) Created using Powerpoint   |
| **Figure II**   | (**Non-empirical output**) Created using Powerpoint   |
| **Figure III**  | (**Non-empirical output**) Created using Powerpoint   |
| **Figure IV**   | **Panel A (left to right)**: PK_time_series_train_vRep.pdf, PK_time_series_valid_vRep.pdf, PK_time_series_test_vRep.pdf. \ **Panel B (left to right)**: AJ_PK_time_series_train_vRep.pdf, AJ_PK_time_series_valid_vRep.pdf, AJ_PK_time_series_test_vRep.pdf |
| **Figure V**    |                                                       |
| **Figure VI**   |                                                       |
| **Figure VII**  |                                                       |
| **Figure VIII** |                                                       |
| **Figure A14**  | (**Non-empirical output**) Panel A and B Created using Powerpoint  |
| **Figure A15**  | (**Non-empirical output**) Panel A and B Created using Powerpoint  |

### 5.3 Algorithm Outputs

| Name               | Description                                |
|:-------------------|:-------------------------------------------|
| **Algorithm 1**    | (**Non-empirical output**) Created using LaTeX |
| **Algorithm 2**    | (**Non-empirical output**) Created using LaTeX |

***Fin!***
