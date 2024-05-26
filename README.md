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

*NOTE 1: if a package is not installed on the computer, you need to install the module first*. 
*NOTE 2: it is **very** likely that the python program will not run if the user did not ensure that the plot_model package was properly installed. In particular, ensure that a compatible version of **graphviz** is installed along with plot_model*

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

The code has [**insert number of sections in python code here**] sections of code in total, each performing different tasks:

- **Section 1: Reproducibility, Delimitation and Paper Colors**:
    - (1.1) Creates seed-functionality for reproducible machine learning estimations.
    - (1.2) Specifies all relevant folder paths and the dates delimiting the training-validation-test split used.
    - (1.3) Creates firm characteristic category labels and defines the primary colors (hexidecimal) for figure outputs.
    - (1.4) Selects study period and specifies select parameters: e.g. LSTM lookback period and number of moment conditions for the GAN-type models. 
- **Section 2: Python Preliminaries and Packages**:
    - (2.0) Imports required packages for the machine learning estimation.
    - (2.1) Prints versions of packages so user can cross-check compatibility to the required package versions stated in this paper.
- **Section 3: Import Data**:
    - (3.1) Creates keras mask object (to deal with unbalanced panel) 
    - (3.2) Imports and winsorizes weekly excess return data $R_{t+1}^{e}$
    - (3.3) Imports firm characteristics $I_{t,i}$
    - (3.4) Imports firm macroeconomic dataset $I_t$
    - (3.5) Creates time variables relating to Train-Valid-Test split
    - (3.6) Subsample firm characteristics
    - (3.7) Subsample firm macroeconomic data
    - (3.8) Garbage disposal (free up application memory)
- **Section 4: Machine Learning Model Building**:
    - (4.1) Build custom minimax neural network layer
    - (4.2) Create flexible LSTM Network building functionality
    - (4.3) Create integrated "LSTM-into-FFN" Network building functionality
    - (4.4) Create COND network building functionality
    - (4.5) Create PK network building functionality
    - (4.6) Create 16 GAN model architectures ahead of validation procedure
- **Section 5: Auxiliary Model Training Functionalities**:
    - (5.1) Label and prediction generating functions
    - (5.2) Creates in-training GAN loss function
    - (5.3) Creates in-training Sharpe Ratio metric
    - (5.4) Creates custom callbacks to save model, real-time plot of performance, etc.
- **Section 6: PK Network Validation procedure**:
    - (6.1) Train 16 PK Networks for 256 epoch unconditional fit of Algorithm (1)
    - (6.2) Evaluate validation set Sharpe ratio of 16 GAN models
- **Section 7: Unconditional Fit of validated GAN ensemble**:
    - (7.1) Creates model configurations according to validated model
    - (7.2) Creates 5 validated LSTM and FFN models for PK networks inside ensemble
    - (7.3) Run final unconditional fit of GAN model
    - (7.4) Build COND Network ensemble ahead of conditional fit
- **Section 8: Conditional Fit of GAN Model**:
    - (8.1) Create auxiliary objects for the conditional fit
    - (8.2) Run final conditional fit of GAN model
    - (8.3) Ensemble learning on GAN PK weights estimates $\omega_t^{GAN}$
    - (8.4) Produce final GAN Sharpe ratio estimates by subsample
    - (8.5) Produce GAN performance by epoch plots
- **Section 9: GAN-Beta Network Model Architecture**:
    - (9.1) Create return factor $F_{t+1}$ for GAN model
    - (9.2) Extract LSTM part of network to produce fitted hidden states
    - (9.3) Create custom beta scaling layer
    - (9.4) GAN-Beta Network architecture function
    - (9.5) GAN-Beta ensemble generator function
    - (9.6) Auxiliary objects to GAN-Beta network
    - (9.7) Residualization function using the estimated betas and returns
    - (9.8) Creates additional auxiliary functions for GAN-Beta network 
    - (9.9) Create GAN-Beta in-training callbacks
    - (9.10) Create GAN-Beta in-training metrics
    - (9.11) Create GAN-Beta in-training loss function
    - (9.12) Create additional GAN-Beta in-training $TS-R^2$ metric
- **Section 10: GAN Beta Network Validation Procedure**
    - (10.1) Fit 16 GAN-Beta networks for ensemble procedure
    - (10.2) Extract validated GAN-Beta model
- **Section 11: GAN-Beta Network Ensemble Fit**:
    - (11.1) Fit GAN-Beta Ensemble (5 validated models)
    - (11.2) Plot ensemble GAN-Beta $TS-R^2$ performance by epoch
- **Section 12: Create Final GAN Explained Variation Metrics**:
    - (12.1) Ensemble learning on GAN-Beta predictions
    - (12.2) GAN-Beta final residualization procedure
    - (12.3) Calculate final GAN TS-R2 metric
    - (12.4) Calculate final GAN CS-R2 metric
- **Section 13: Beta Scalings and GAN Predictive Power**:
    - (13.1) Scaling Betas according to $\beta_t'\omega_t = 1$
    - (13.2) Auxiliary scaling functions for sorting stocks into deciles by loadings
    - (13.3) Decile sorting and beta representation (SML) functions
    - (13.4) Create decile sorting plots and beta representation plots
- **Section 14: GAN Variable Importance Analysis**:
    - (14.1) Estimate out-of-sample VI within GAN ensemble and aggregate
    - (14.2) Plot GAN saliency analysis plot
- **Section 15: GAN Linear Interaction Analysis**:
    - (15.1) Extract FFN part of PK network for plotting purposes
    - (15.2) Create auxiliary plotting functions and objects
    - (15.3) Plot linear interation plot for GAN model
- **Section 16: GAN Heatmap Plots**:
    - (16.1) Auxiliary functions and inputs to heatmap
    - (16.2) Create Heatmap plotting function and plot heatmaps
- **Section 17: Fitted GAN Macroeconomic Hidden States**:
    - (17.1) Extract and format hidden state variables
    - (17.2) Plot GAN hidden states as predicted by LSTM model (within PK network)
- **Section 18: Elastic Net Estimation**:
    - (18.1) Create EN-specific characteristic portfolios
    - (18.2) Create Sharpe ratio metric for LARS-EN estimation
    - (18.3) First step LARS-EN fit: validation procedure
    - (18.4) Extract optimal EN hyperparameters
    - (18.5) Second step LARS-EN fit: ensemble fit
    - (18.6) Calculate final ensemble estimates and Sharpe ratios
    - (18.7) Elastic net regularization analysis
- **Section 19: Elastic Net Beta estimation**:
    - (19.1) Project $R_{t+1}^{e}F_{t+1}$ onto information set $I_{t,i}$
    - (19.2) Residualization
    - (19.3) Calculate TS-R2
    - (19.4) Calculate CS-R2
- **Section 20: Elastic Net Beta Scaling**:
    - (20.1) L1-normalize PK weights
    - (20.2) Scale betas according to $\beta_t'\omega_t = 1$
- **Section 21: Elastic Net Variable Importance Analysis**:
    - (21.1) Create inputs for saliency analysis
    - (21.2) Plot variable importance
- **Section 22: Elastic Net Linear Interaction Plot**:
    - (22.1) Creates inputs and auxiliary functions for interaction plot
    - (22.2) Plots linear interactions for the elastic net model
- **Section 23: Elastic Net Heatmap Plots**:
    - (23.1) Creates auxiliary objects and functions for heatmap
    - (23.2) Plot EN heatmap
- **Section 24: Beta Spreads and Beta Representation for EN**:
    - (24.1) Decile sort loadings
    - (24.2) Create plotting functions
    - (24.3) Plot beta spreads and beta representation
- **Section 25: Build Feedforward Network Model (FFN)**:
    - (25.1) FFN architecture functionality
    - (25.2) FFN in-training Sharpe metrics
    - (25.3) FFN ensemble functionality
    - (25.4) FFN validation procedure
    - (25.5) Fit validated FFN ensemble
    - (25.6) Plot FFN Sharpe performance by epoch
- **Section 26: FFN Asset Pricing Performance**:
    - (26.1) FFN Sharpe ratios
    - (26.2) Scale FFN PK weights and loadings
    - (26.3) Residualize returns
    - (26.4) TS-R2
    - (26.5) CS-R2
- **Section 27: FFN Beta Spread and Beta Representation**:
    - (27.1) Decile sort loadings
    - (27.2) Create plotting functions
    - (27.3) Plot beta spreads and beta representation
- **Section 28: FFN Variable Importance Analysis**:
    - (28.1) Estimate variable importance for FFN ensemble
    - (28.2) Plot variable importance for FFN
- **Section 29: FFN Linear Interactions**:
    - (29.1) Create inputs and auxiliary functions for linear interactions
    - (29.2) Plot linear interactions
- **Section 30: FFN Heatmap Plots**:
    - (30.1) Create inputs and auxiliary functions for heatmap
    - (30.2) Plot heatmap
- **Section 31: Fama-French GMM Procedure**:
    - (31.1) Create new characteristic dataset starting in 1999 (for June 1999 characteristic values in particular)
    - (31.2) Sort firms by characteristics in June on annual basis
    - (31.3) Build Fama-French quantile portfolios of characteristics
    - (31.4) Create Fama-French quantile group weights (value-weighted) and returns
    - (31.5) Create Fama-French Factor returns, Standalone
    - (31.6) Create Market Factor
    - (31.7) Combine Fama-French Factors
    - (31.8) Fama-French GMM estimation
    - (31.9) Extract Fama-French PK coefficients and FF-SDF return
- **Section 32: Factor Model Pricing Tests** (baseline models: GAN, FFN, EN):
    - (32.1) Create beta-portfolios (model-generated signals)
    - (32.2) Create Factor model regression functions
    - (32.3) CAPM Regressions
    - (32.4) FF3 Regressions
    - (32.5) FF5 Regressions
    - (32.6) Regression p-values
    - (32.7) GRS test
    - (32.8) Preformatting LaTeX table
    - (32.9) Export factor pricing tests LaTeX tables
- **Section 33: Pricing Characteristically Managed Portfolios** (baseline models: GAN, FFN, EN):
    - (33.1) Combine loadings and characteristic datasets
    - (33.2) Create characteristic sorts
    - (33.3) R-squared function on characteristic managed portfolios
    - (33.4) Pricing 460 Characteristically managed portfolios (GAN)
    - (33.5) Pricing 460 Characteristically managed portfolios (FFN)
    - (33.6) Pricing 460 Characteristically managed portfolios (EN)
    - (33.7) Pre-format LaTeX table
    - (33.8) Export pricing table for 460 characteristically managed portfolios
- **Section 34: Characteristic Pricing by GAN most important characteristics**:
    - (34.1) Create inputs and labellings
    - (34.2) Pre-format LaTeX table
    - (34.3) Export pricing table for most important characteristically managed portfolios (according to GAN)
- **Section 35: Characteristic Pricing by FFN most important characteristics**:
    - (35.1) Pre-format LaTeX table
    - (35.2) Export pricing table for most important characteristically managed portfolios (according to FFN)
- **Section 36: Characteristic Pricing by EN most important characteristics**:
    - (36.1) Pre-format LaTeX table
    - (36.2) Export pricing table for most important characteristically managed portfolios (according to EN)
- **Section 37: Stocks per week plot**:
    - (37.0) Plot the number of stocks in the sample by week
- **Section 38: St. Gallen Main Table**:
    - (38.1) Format table data
    - (38.2) Export LaTeX table
- **Section 39: Baseline Models Factor Time Series**:
    - (39.1) Variance scaling of return factors
    - (39.2) Calculate cumulative excess returns of factors
    - (39.3) Plot cumulative returns of ML models
- **Section 40: Bond Macroeconomic Data**:
    - (40.1) Import and format STATA bond data
    - (40.2) Tensorize bond macroeconomic information set
- **Section 41: Bond Return Mask**:
    - (41.1) Import and format STATA bond mask
    - (41.2) Number of bond indices per week plot
    - (41.3) Pad number of bonds to match stock dimension
- **Section 42: Bond Return Data**:
    - (42.1) Import and format STATA bond return data
    - (42.2) Pad number of bonds to match stock dimension
- **Section 43: Bond Characteristics**:
    - (43.1) Import and format STATA bond characteristic data
    - (43.2) Pad number of bonds to match stock dimension
- **Section 44: Alvarez-Jermann Model Building**:
    - (44.1) AJ GAN type LSTM building functionality
    - (44.2) AJ GAN type Network building functionality
    - (44.3) Component Pricing Kernel Specification Functionality
    - (44.4) Combined Pricing Kernel Network Specification Functionality
- **Section 45: Create AJ labels**:
    - (45.0) creates structure of true labels for extended GAN models
- **Section 46: 




## 5. Where to find paper outputs

This section describes which files produced by the Python code corresponds to which output in the final paper. *All* output figures are stored as .pdf files in subfolders within the "Output/Results" folder. Likewise, *all* output tables are stored as LaTeX files (.tex) in subfolders within the "Output/Results" folder. Therefore, I am detailing here the filenames of each .pdf and .tex files that correspond to each Figure and Table in the paper here. The user can then find where in the code this file is created, and the procedure going into producing these outputs.

### 5.1 Table Outputs

| Name           | Description                                              | Code Section |
|:---------------|:---------------------------------------------------------|:-------------|
| **Table I**    | main_table_v240425.tex                                   | 38 and [add AJ sec] |
| **Table II**   | beta_pricing_vRep.tex                                    | 32.9         |
| **Table III**  | AJ_beta_pricing_vRep.tex                                 |              |
| **Table IV**   | CharsOverallRsquaredTable_v2Rep.tex                      | 33           |
| **Table V**    | CharsDecileTable_GAN_vRep.tex                            | 34           |
| **Table VI**   | AJ_CharsOverallRsquaredTable_v240425.tex                 |              |
| **Table A1**   | M_correl_input3.tex                                      |              |
| **Table A2**   | CharsDecileTable_FFN_vRep                                | 35           |
| **Table A3**   | CharsDecileTable_EN_vRep                                 | 36           |
| **Table A4**   | AJ_CharsDecileTable_GAN_v240425                          |              |
| **Table A5**   | AJ_Phi_CharsDecileTable_GAN_v240425                      |              |
| **Table A6**   | AJ_Disjoint_CharsDecileTable_GAN_v240425                 |              |
| **Table A7**   | (**Non-empirical output**) Parts 1-3 Created using LaTeX |              |
| **Table A8**   | (**Non-empirical output**) Created using LaTeX           |              |
| **Table A9**   | (**Non-empirical output**) Parts 1-2 Created using LaTeX |              |
| **Table A10**  | (**Non-empirical output**) Parts 1-2 Created using LaTeX |              |
| **Table A11**  | (**Non-empirical output**) Created using LaTeX           |              |
| **Table A12**  | See validation sections of code for empirical results of validation procedure, created using LaTeX | 6, 18.3-18.4, 25.4 |
| **Table A13**  | EN_ensemble_tab_vRep.tex                                 | 18.5 - 18.6  |
| **Table A14**  | See validation sections of code for empirical results of validation procedure, created using LaTeX | 10  |
| **Table A15**  | See Fama-French and GMM estimation for empirical results in the table, created using LaTeX | 31.8 |
| **Table A16**  | FF3_beta_pricing_vRep.tex                                | 32.9         |
| **Table A17**  | FF5_beta_pricing_vRep.tex                                | 32.9         |
| **Table A18**  | FF3_AJ_beta_pricing_vRep.tex                             |              |
| **Table A19**  | FF5_AJ_beta_pricing_vRep.tex                             |              |
| **Table A20**  | (**Non-empirical output**) Created using LaTeX           |              |

### 5.2 Figure Outputs

| Name            | Description                                           | Code Section |
|:----------------|:------------------------------------------------------|:-------------|
| **Figure I**    | (**Non-empirical output**) Created using Powerpoint   |              |
| **Figure II**   | (**Non-empirical output**) Created using Powerpoint   |              |
| **Figure III**  | (**Non-empirical output**) Created using Powerpoint   |              |
| **Figure IV**   | **Panel A** (left to right): PK_time_series_train_vRep.pdf, PK_time_series_valid_vRep.pdf, PK_time_series_test_vRep.pdf. <br> **Panel B** (left to right): AJ_PK_time_series_train_vRep.pdf, AJ_PK_time_series_valid_vRep.pdf, AJ_PK_time_series_test_vRep.pdf | 39 and [add AJ secs] |
| **Figure V**    | **Panel A** (left to right): GAN_Beta_rep_Train.pdf, GAN_Beta_rep_Valid.pdf, GAN_Beta_rep_Test.pdf <br> **Panel B** (left to right): FFN_Beta_rep_Train_vReplication.pdf, FFN_Beta_rep_Valid_vReplication.pdf, FFN_Beta_rep_Test_vReplication.pdf <br> **Panel C** (left to right): EN_Beta_rep_Train_vRep.pdf, EN_Beta_rep_Valid_vRep.pdf, EN_Beta_rep_Test_vRep.pdf | 13.4-13.5, 24.2-24.3 and 27.2-27.3 |
| **Figure VI**   | **Panel A**: VariableImportance_firmchars_GAN_vReplication.pdf <br> **Panel B**: VariableImportance_firmchars_FFN_vReplication.pdf <br> **Panel C**: VariableImportance_firmchars_EN_vRep.pdf | 14.2, 21.2 and 28.2 |
| **Figure VII**  | **Panel A** (left to right): VI_AJ_permanent.pdf, VI_AJ_Phi_permanent.pdf <br> **Panel B** (left to right): VI_AJ_transitory.pdf, VI_AJ_Phi_transitory.pdf <br> **Panel C** (left to right): VI_AJ_Full.pdf, VI_AJ_Phi_Full.pdf|              |
| **Figure VIII** | **Panel A**: VI_AJ_Disjoint_permanent.pdf <br> **Panel B**: VI_AJ_Disjoint_transitory.pdf <br> **Panel C**: VI_AJ_Disjoint_Full.pdf |              |
| **Figure IX**   | **(a), (b), (c)**: EN_SUV_interact_Lturnover_v2.pdf, EN_SUV_interact_CF_v2.pdf, EN_SUV_interact_LME_v2.pdf <br> **(d), (e), (f)**: EN_Lturnover_interact_CF_v2.pdf, EN_Lturnover_interact_LME_v2.pdf, EN_CF_interact_LME_v2.pdf | 22             |
| **Figure X**    | **(a), (b), (c)**: GAN_PM_interact_SUV_vRep.pdf, GAN_PM_interact_NOA_vRep.pdf, GAN_PM_interact_AC_vRep.pdf <br> **(d), (e), (f)**: GAN_SUV_interact_NOA_vRep.pdf, GAN_SUV_interact_AC_vRep.pdf, GAN_NOA_interact_AC_vRep.pdf    | 15             |
| **Figure XI**   | **(a), (b), (c)**: FFN_AT_A2ME_heatmap_vR.pdf, FFN_AT_LME_heatmap_vR.pdf, FFN_AT_Q_heatmap_vR.pdf <br> **(d), (e), (f)**: FFN_A2ME_LME_heatmap_vR.pdf, FFN_A2ME_Q_heatmap_vR.pdf, FFN_LME_Q_heatmap_vR.pdf | 30             |
| **Figure XII**  | **(a), (b), (c)**: AJ_Phi_GAN_PROF_NOA_heatmap_vRep.pdf, AJ_Phi_GAN_Lturnover_SUV_heatmap_vRep.pdf, AJ_Phi_GAN_PROF_OA_heatmap_vRep.pdf <br>  **(d), (e), (f)**: AJ_Phi_GAN_Lturnover_E2P_heatmap_vRep.pdf, AJ_Phi_GAN_NOA_OA_heatmap_vRep.pdf, AJ_Phi_GAN_SUV_E2P_heatmap_vRep.pdf |              |
| **Figure A1**   | **(a), (b), (c)**: AJ_PK_comps_train_vRep.pdf, AJ_PK_comps_valid_vRep.pdf, AJ_PK_comps_test_vRep.pdf |              |
| **Figure A2**   | GAN_Beta_spread.pdf                                   | 13.3-13.4    |
| **Figure A3**   | FFN_Beta_spread_vReplication.pdf                      | 27.2-27.3    |
| **Figure A4**   | EN_Beta_spread_vRep.pdf                               | 24.2-24.3    |
| **Figure A5**   | **Model 1-5**: HS_vReplication_1.pdf, HS_vReplication_2.pdf, HS_vReplication_3.pdf, HS_vReplication_4.pdf, HS_vReplication_5.pdf           | 17             |
| **Figure A6**   | **Model 1-5**: AJ_HS_1_vLoaded.pdf, AJ_HS_2_vLoaded.pdf, AJ_HS_3_vLoaded.pdf, AJ_HS_4_vLoaded.pdf, AJ_HS_5_vLoaded.pdf |               |
| **Figure A7**   | **Model 1-5**: AJ_Phi_HS_1_vLoaded.pdf, AJ_Phi_HS_2_vLoaded.pdf, AJ_Phi_HS_3_vLoaded.pdf, AJ_Phi_HS_4_vLoaded.pdf, AJ_Phi_HS_5_vLoaded.pdf |               |
| **Figure A8**   | **Model 1-5**: AJ_Disjoint_HS_1_vLoaded.pdf, AJ_Disjoint_HS_2_vLoaded.pdf, AJ_Disjoint_HS_3_vLoaded.pdf, AJ_Disjoint_HS_4_vLoaded.pdf, AJ_Disjoint_HS_5_vLoaded.pdf |               |
| **Figure A9**   | **(a), (b), (c)**: FFN_AT_interact_A2ME.pdf, FFN_AT_interact_LME.pdf, FFN_AT_interact_Q.pdf <br>  **(d), (e), (f)**: FFN_A2ME_interact_LME.pdf, FFN_A2ME_interact_Q.pdf, FFN_LME_interact_Q.pdf | 29             |
| **Figure A10**  | **(a), (b), (c)**: SUV_Lturnover_heatmap_v2.pdf, SUV_CF_heatmap_v2.pdf, SUV_LME_heatmap_v2.pdf <br> **(d), (e), (f)**: Lturnover_CF_heatmap_v2.pdf, /Lturnover_LME_heatmap_v2.pdf, CF_LME_heatmap_v2.pdf |              |
| **Figure A11**  | **(a), (b), (c)**: GAN_PM_SUV_heatmap_vReplication.pdf, GAN_PM_NOA_heatmap_vReplication.pdf, GAN_PM_AC_heatmap_vReplication.pdf <br> **(d), (e), (f)**: GAN_SUV_NOA_heatmap_vReplication.pdf, GAN_SUV_AC_heatmap_vReplication.pdf, GAN_NOA_AC_heatmap_vReplication.pdf | 16             |
| **Figure A12**  | **(a), (b), (c)**: AJ_GAN_r12_2_LME_heatmap_vRep.pdf, AJ_GAN_LME_SUV_heatmap_vRep.pdf, AJ_GAN_r12_2_ATO_heatmap_vRep.pdf <br> **(d), (e), (f)**: AJ_GAN_LME_Lturnover_heatmap_vRep.pdf, AJ_GAN_LME_ATO_heatmap_vRep.pdf, AJ_GAN_SUV_Lturnover_heatmap_vRep.pdf |              |
| **Figure A13**  | **(a), (b), (c)**: AJ_Disjoint_GAN_Lturnover_SUV_heatmap_vRep.pdf, AJ_Disjoint_GAN_ST_BV_Bond_r12_3_heatmap_vRep.pdf, AJ_Disjoint_GAN_Lturnover_Resid_Var_heatmap_vRep.pdf <br> **(d), (e), (f)**: AJ_Disjoint_GAN_ST_BV_LT_Kurt_heatmap_vRep.pdf, AJ_Disjoint_GAN_SUV_Resid_Var_heatmap_vRep.pdf, AJ_Disjoint_GAN_Bond_r12_3_LT_Kurt_heatmap_vrep.pdf |              |
| **Figure A14**  | (**Non-empirical output**) Panel A and B Created using Powerpoint  |              |
| **Figure A15**  | (**Non-empirical output**) Panel A and B Created using Powerpoint  |              |
| **Figure A16**  |  **Panel A**: Num_stocks_plot_v2.pdf <br>  **Panel B**: Num_bonds_plot_vRep.pdf | 37 and 41.2  |
| **Figure A17**  |  **Panel A** (left to right): Train_GAN_iters_ensemble_new.pdf, /AJ_GAN/Train_AJ_GAN_iters_Sharpe.pdf <br> **Panel B** (left to right): Valid_GAN_iters_ensemble_new.pdf, /AJ_GAN/Valid_AJ_GAN_iters_Sharpe.pdf <br> **Panel C** (left to right): Test_GAN_iters_ensemble_new_TEST.pdf, /AJ_GAN/Test_AJ_GAN_iters_Sharpe.pdf | 8.5 [add AJ-GAN sec.]           |
| **Figure A18**  |  **Panel A** (left to right): /AJ_Phi/Train_AJ_GAN_iters_Sharpe.pdf, /AJ_Disjoint/Train_AJ_GAN_iters_Sharpe.pdf <br> **Panel B** (left to right): /AJ_Phi/Valid_AJ_GAN_iters_Sharpe.pdf, /AJ_Disjoint/Valid_AJ_GAN_iters_Sharpe.pdf <br> **Panel C** (left to right): /AJ_Phi/Test_AJ_GAN_iters_Sharpe.pdf, /AJ_Disjoint/Test_AJ_GAN_iters_Sharpe.pdf |              |
| **Figure A19**  |  **Panel A**: Train_AJ_Phi_Phi_decomp_iters.pdf <br>  **Panel B**: Valid_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel C**: Test_AJ_Phi_Phi_decomp_iters.pdf |              |
| **Figure A20**  |  **Panel A** (left to right): Train_AJ_GAN_iters_Correlation.pdf, Train_AJ_Phi_Phi_decomp_iters.pdf <br> Valid_AJ_GAN_iters_Correlation.pdf, Valid_AJ_Phi_Phi_decomp_iters.pdf **Panel B** (left to right):  <br> **Panel C** (left to right): Test_AJ_GAN_iters_Correlation.pdf, Test_AJ_Phi_Phi_decomp_iters.pdf |              |
| **Figure A21**  |  **Panel A** (left to right): /AJ_Phi_Var_Decomp_Input/Train_AJ_GAN_iters_M-Correlation.pdf, /AJ_Phi_Var_Decomp_Input/Train_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel B** (left to right): /AJ_Phi_Var_Decomp_Input/Valid_AJ_GAN_iters_M-Correlation.pdf, /AJ_Phi_Var_Decomp_Input/Valid_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel C** (left to right):  /AJ_Phi_Var_Decomp_Input/Test_AJ_GAN_iters_M-Correlation.pdf, /AJ_Phi_Var_Decomp_Input/Test_AJ_Phi_Phi_decomp_iters.pdf |              |
| **Figure A22**  |  **Panel A** (left to right): /AJ_Disjoint_Var_Decomp_Input/Train_AJ_GAN_iters_M-Correlation.pdf, /AJ_Disjoint_Var_Decomp_Input/Train_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel B** (left to right): /AJ_Disjoint_Var_Decomp_Input/Valid_AJ_GAN_iters_M-Correlation.pdf, /AJ_Disjoint_Var_Decomp_Input/Valid_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel C** (left to right): /AJ_Disjoint_Var_Decomp_Input/Test_AJ_GAN_iters_M-Correlation.pdf, t/AJ_Disjoint_Var_Decomp_Input/Test_AJ_Phi_Phi_decomp_iters.pdf |              |
| **Figure A23**  |  **Panel A** (left to right): /AJ/Train_AJ_Phi_Phi_decomp_iters.pdf, /AJ_Phi/Train_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel B** (left to right): /AJ/Valid_AJ_Phi_Phi_decomp_iters.pdf, /AJ_Phi/Valid_AJ_Phi_Phi_decomp_iters.pdf <br> **Panel C** (left to right): /AJ/Test_AJ_Phi_Phi_decomp_iters.pdf, /AJ_Phi/Test_AJ_Phi_Phi_decomp_iters.pdf |              |
| **Figure A24**  |  **Panel A** Train_FFN_iters_ensemble_vReplication.pdf <br> **Panel B** Valid_FFN_iters_ensemble_vReplication.pdf <br> **Panel C** <br> Test_FFN_iters_ensemble_vReplication.pdf | 25.6            |
| **Figure A25**  | SR_HyperParams_vReplication.pdf  | 18.3-18.4             |
| **Figure A26**  |  **Panel A**: Coef_by_alpha_vRep.pdf <br> **Panel B**: Coef_by_lambda_vRep.pdf | 18.7           |
| **Figure A27**  |  Xi_valid_iters_v3.pdf                                |              |
| **Figure A28**  |  **Panel A** (left to right): Train_Beta_Iters.pdf, Train_AJ_Beta_Iters.pdf <br> **Panel B** (left to right): Valid_Beta_Iters.pdf, Valid_AJ_Beta_Iters.pdf <br> **Panel C** (left to right): Test_Beta_Iters.pdf, Test_AJ_Beta_Iters.pdf | 11.2 and [add AJ-Beta sec] |
| **Figure A29**  |  **Panel A** (left to right): Train_AJ_Phi_Beta_Iters.pdf, Train_AJ_Disjoint_Beta_Iters.pdf <br> **Panel B** (left to right): Valid_AJ_Phi_Beta_Iters.pdf, Valid_AJ_Disjoint_Beta_Iters.pdf <br> **Panel C** (left to right): Test_AJ_Phi_Beta_Iters.pdf, Test_AJ_Disjoint_Beta_Iters.pdf |              |

### 5.3 Algorithm Outputs

| Name               | Description                                    |
|:-------------------|:-----------------------------------------------|
| **Algorithm 1**    | (**Non-empirical output**) Created using LaTeX |
| **Algorithm 2**    | (**Non-empirical output**) Created using LaTeX |

***Fin!***
