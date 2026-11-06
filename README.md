## NYC Multifamily Building Energy Consumption Prediction
Hackathon — Use Case 2 | Predictive Analysis of NYC Building Energy Usage
Project overview
Can we use what we know about a New York City apartment building to predict how much energy it consumes in a year?

Our team will analyze multifamily-building data, identify patterns in energy use, and build models that predict weather-normalized annual site energy consumption (kBtu). We will then compare predicted consumption with actual consumption to flag buildings that may deserve a closer look for possible energy-efficiency opportunities.
Important: A building using more energy than predicted is not automatically inefficient. The result signals a need for further investigation, not proof of waste.

Goals
1. Clean and validate the data: inspect data types, missing values, duplicates, unusual values, and consistency across the training and testing datasets.
2. Explore energy consumption: calculate Energy Use Intensity (EUI) and visualize how it varies with building characteristics.
3. Build predictive models: start with a simple baseline, then compare linear regression and more advanced machine-learning models.
4. Evaluate performance: compare predictions against actual energy use on the provided test dataset.
5. Explain the results: identify the strongest predictors, discuss unexpected energy use, and communicate findings and limitations through a report, presentation, and optional dashboard.
The problem in one sentence
Predict a building's annual energy consumption from its characteristics, then identify buildings consuming more energy than the model expects.
Dataset
The project uses two CSV files provided for Use Case 2:
File	Purpose	Records
multifamily_building_energy_consumption_training_dataset.csv	Train the prediction models	9,976
multifamily_building_energy_consumption_testing_dataset.csv	Evaluate models on held-out data	2,495


The provided files contain 17 original columns. Examples of building attributes include gross floor area, construction year, occupancy, bedrooms, residential units, heating/cooling coverage, laundry hookups, and resident population type.

Prediction target: Weather Normalized Site Energy Use (kBtu).
Energy Use Intensity (EUI)
EUI helps compare energy use across buildings of different sizes:
EUI (kBtu/ft²) = Annual site energy consumption (kBtu) / Gross floor area (ft²)
EUI is used for exploratory analysis and the baseline prediction. Do not include EUI or actual energy use as input features when predicting energy use, since that would leak the answer into the model.
Project workflow
1. Data cleaning
- Verify column names and data types in both datasets.
- Treat Not Available as missing, rather than as the number zero.
- Convert laundry-hookup counts stored as text into numeric values.
- Check duplicates and extreme values; document decisions rather than deleting records automatically.
- Fit any missing-value imputations on training data only, then apply the learned transformations to testing data.
- Preserve the original CSV files.
2. Exploratory Data Analysis (EDA)
We will calculate average and median EUI, inspect the EUI distribution, and visualize relationships with:
- Construction year / decade
- Building floor area
- Reported high-rise and mid-rise residential-unit categories
- Number of bedrooms
We will explain the patterns observed, not just display the charts. Height categories are proxies based on the provided unit-count fields, not direct measurements of the building's height.
3. Predictive modeling
Models to compare:
- Baseline: floor area × median training EUI
- Linear regression: a straightforward, interpretable comparison
- Random Forest / Extra Trees: models that can capture nonlinear relationships
Models predict annual energy consumption in kBtu.
4. Evaluation
We compare predictions with actual values in the held-out test set using:
Metric	Meaning	Preferred direction
MAE	Average absolute difference between predicted and actual energy	Lower
RMSE	Similar to MAE but penalizes large errors more	Lower
MAPE	Average percentage error; sensitive to very small actual values	Lower
R²	Amount of variation explained relative to a mean baseline	Higher


We will also create a predicted-versus-actual chart, inspect residuals, and review buildings with the largest positive prediction errors.
Preliminary findings (subject to final verification)
Earlier exploratory work on the provided training data found:
- Mean EUI: approximately 76.00 kBtu/ft²
- Median EUI: approximately 75.41 kBtu/ft²
- EUI patterns varied across building-size groups, construction periods, and reported height categories.
- Tree-based models performed better than a simple EUI baseline in an earlier test-set comparison.
These are preliminary results from earlier analysis, not a claim that the latest notebook has been rerun and all outputs have been independently verified. Update this section with the team's final reproducible metrics and charts before the hackathon presentation.
Repository structure
The structure below is a suggested organization as the team adds files:
.
├── README.md
├── requirements.txt                 # Python dependencies (if added)
├── .gitignore
├── Use_Case_2_End_to_End_Analysis.ipynb
├── multifamily_building_energy_consumption_training_dataset.csv  # local only
├── multifamily_building_energy_consumption_testing_dataset.csv   # local only
├── charts/                          # EDA and modeling visualizations
├── reports/                         # Written report and final slides
└── dashboard/                       # Optional interactive dashboard
Note: The notebook currently expects both CSV files to be in the same working directory when you run it. If the team later moves them into data/raw/, update the TRAIN and TEST paths in the notebook.

Do not commit raw datasets unless your hackathon's sharing rules explicitly allow it. If the data cannot be shared publicly, each teammate should obtain the files through the approved team channel.
Getting started
1. Clone the repository and enter the project folder:
   git clone <YOUR-REPOSITORY-URL>
   cd <YOUR-REPOSITORY-NAME>
2. Create and activate a virtual environment (recommended):
   python -m venv .venv
   # macOS / Linux:
   source .venv/bin/activate
   # Windows PowerShell:
   # .venv\Scripts\Activate.ps1
3. Install the main Python packages:
   pip install pandas numpy matplotlib scikit-learn jupyter
   If the repo includes requirements.txt, you can instead run pip install -r requirements.txt.
4. Place the original training and testing CSV files alongside the notebook (unless you update its input paths).
5. Start Jupyter and run the notebook from top to bottom:
   jupyter notebook Use_Case_2_End_to_End_Analysis.ipynb
The notebook should handle data checks, EUI calculation, charts, model training, evaluation, and prediction exports. Do not use test-set results to repeatedly tune your modeling decisions.
Team collaboration on GitHub
To avoid conflicting changes, use a separate branch for each task:
git checkout -b feature/eda-analysis
# Make your changes, then:
git add .
git commit -m "Add EDA charts and findings"
git push -u origin feature/eda-analysis
Then open a Pull Request (PR) into main so at least one teammate can review it before merging.

Suggested workstreams:
Workstream	Responsibilities
Data preparation	Cleaning decisions, validation, feature definitions
EDA	Summary statistics, charts, explanations
Modeling	Baseline and ML models, error metrics, residual analysis
Presentation / integration	Align report, dashboard, slides, and final results


Team rules: Keep main working; write descriptive commit messages; do not overwrite teammates' notebooks; never commit credentials or private data; and document important decisions in PRs or GitHub Issues.
Deliverables checklist
- [ ] Data cleaning documented and reproducible
- [ ] EUI calculated and summarized
- [ ] Required EDA charts generated and explained
- [ ] Baseline prediction method evaluated
- [ ] At least one regression/ML prediction method evaluated
- [ ] All model metrics verified on the provided test dataset
- [ ] Predicted-versus-actual plot and error analysis completed
- [ ] Main findings and limitations written up
- [ ] Final report and slides reviewed by the team
- [ ] Optional interactive dashboard ready for demonstration
Limitations
- Findings show associations, not causal effects.
- Important building-system factors (e.g., equipment condition or renovations) may be absent.
- A large positive residual is a review signal, not proof of energy waste.
- The supplied data does not provide a reliable unique building/address identifier for matching flagged rows to real buildings.
- Results may not generalize to other cities, property types, or time periods without new validation.
Team
Add teammates and GitHub handles here as responsibilities are confirmed.
Member	GitHub	Role
TBD	@username	TBD
TBD	@username	TBD
TBD	@username	TBD


Created for the hackathon's Use Case 2. Replace preliminary results and checklist entries with verified team outputs before final submission.
