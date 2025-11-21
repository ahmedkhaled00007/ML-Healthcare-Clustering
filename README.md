# Healthcare Patient Clustering Analysis

## Project Overview
This project performs **unsupervised machine learning** on healthcare data to identify distinct patient groups based on their medical characteristics, admission patterns, insurance coverage, and medication usage. Using **K-Means clustering**, the analysis segments patients into 4 meaningful clusters to help healthcare providers understand patient populations better.

---

## Dataset
**Source:** `healthcare_dataset.csv`

### Original Features
- **Patient Demographics:** Name, Age, Gender, Blood Type
- **Admission Details:** Date of Admission, Discharge Date, Admission Type, Room Number
- **Medical Information:** Medical Condition, Test Results, Medication
- **Healthcare Providers:** Doctor, Hospital, Insurance Provider
- **Financial:** Billing Amount

---

## Technologies Used
- **Python 3.x**
- **Libraries:**
  - `pandas` - Data manipulation and analysis
  - `numpy` - Numerical computations
  - `matplotlib` - Data visualization
  - `seaborn` - Statistical visualizations
  - `scikit-learn` - Machine learning algorithms
    - KMeans clustering
    - PCA (Principal Component Analysis)
    - StandardScaler for normalization
    - LabelEncoder for categorical encoding

---

## Project Workflow

### 1. Data Loading & Exploration
- Load dataset using pandas
- Create a copy for safe preprocessing
- Examine data structure, shape, and data types
- Check for missing values

### 2. Exploratory Data Analysis (EDA)
- **Statistical Summary:** Generate descriptive statistics for numerical and categorical features
- **Missing Values:** Identify null values
- **Outlier Detection:** Use IQR (Interquartile Range) method to detect outliers
  - Calculate Q1 (25th percentile) and Q3 (75th percentile)
  - Define outliers as values outside [Q1 - 1.5×IQR, Q3 + 1.5×IQR]

### 3. Data Preprocessing

#### Feature Removal
Dropped irrelevant or high-cardinality features:
- `Test Results` - Not useful for clustering
- `Name` - Personally identifiable information
- `Room Number` - Not medically significant
- `Doctor` - High cardinality
- `Hospital` - High cardinality

#### Feature Engineering
- **Date Features:** Extracted year and month from:
  - Date of Admission → `Admission_Year`, `Admission_Month`
  - Discharge Date → `Discharge_Year`, `Discharge_Month`
- Dropped original date columns after extraction

#### Encoding
- **Label Encoding:** Applied to `Gender` (binary categorical)
- **One-Hot Encoding:** Applied to remaining categorical features using `pd.get_dummies()`
- **Boolean Conversion:** Converted boolean columns to integers (0/1)

#### Normalization
- **StandardScaler:** Applied to numerical features to standardize values
  - Ensures features are on the same scale
  - Improves K-Means performance

### 4. Data Visualization
- **Histograms:** Distribution of all features
- **Correlation Heatmap:** Identify relationships between variables
- **Correlation Analysis:** Flag strong correlations (|r| > 0.4)

### 5. Clustering

#### Optimal Cluster Selection
- **Elbow Method:** Tested K values from 1 to 10
  - Plotted inertia (sum of squared distances) vs. number of clusters
  - Selected **K=4** based on elbow point

#### K-Means Clustering
- Applied K-Means with 4 clusters
- Random state set to 42 for reproducibility
- Assigned cluster labels to each patient

#### Cluster Visualization
- **PCA Reduction:** Reduced dimensions to 2D for visualization
- **Scatter Plot:** Visualized clusters in 2D space with distinct colors

### 6. Cluster Interpretation
Analyzed mean values of features for each cluster to identify patterns:

#### **Cluster 0: Urgent_BlueCross_HighMed**
- **Admission Type:** Urgent
- **Insurance:** Primarily Blue Cross
- **Medication:** High usage of Ibuprofen and Lipitor
- **Profile:** Urgent care patients with specific insurance using common medications

#### **Cluster 1: Emergency_MixedInsurance_Chronic**
- **Admission Type:** Emergency
- **Insurance:** Mixed providers
- **Medical Conditions:** Higher rates of chronic conditions (Arthritis, Asthma, Obesity)
- **Profile:** Emergency patients with diverse insurance and chronic health issues

#### **Cluster 2: Elective_LowMed_Healthy**
- **Admission Type:** Elective
- **Insurance:** Low insurance utilization
- **Medication:** Low usage
- **Profile:** Generally healthier patients with planned admissions

#### **Cluster 3: Urgent_MultiInsurance_HighMed**
- **Admission Type:** Urgent
- **Insurance:** Cigna, Medicare, UnitedHealthcare, Aetna
- **Medication:** High usage across multiple medications
- **Conditions:** Slightly higher diabetes prevalence
- **Profile:** Urgent patients with diverse insurance and high medication needs

### 7. Cluster Naming
Created meaningful cluster names using a mapping dictionary for easier interpretation and communication.

---

## Key Findings

1. **4 Distinct Patient Segments** identified based on admission urgency, insurance type, and medication patterns
2. **Emergency vs. Elective** admissions show clear separation in clustering
3. **Insurance Provider** plays a significant role in patient grouping
4. **Medication Usage** is a strong differentiator between clusters
5. **Cluster 2** represents the healthiest patient population with elective procedures

---

## Usage

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Running the Analysis
1. Ensure `healthcare_dataset.csv` is in the project directory
2. Open `Healthcare.ipynb` in Jupyter Notebook or JupyterLab
3. Run all cells sequentially

### Output
- Cluster assignments for each patient
- Visualizations (histograms, heatmaps, PCA scatter plots)
- Cluster characteristics and interpretations
- Named clusters in `cluster_name` column

---

## Business Applications

1. **Resource Allocation:** Allocate medical resources based on patient cluster needs
2. **Insurance Planning:** Tailor insurance packages to specific patient segments
3. **Preventive Care:** Identify high-risk clusters for targeted interventions
4. **Medication Management:** Optimize medication inventory based on cluster patterns
5. **Operational Efficiency:** Predict admission types and prepare accordingly

---

## Future Improvements

- Try alternative clustering algorithms (DBSCAN, Hierarchical Clustering)
- Incorporate temporal patterns (length of stay, readmission rates)
- Build predictive models to classify new patients into clusters
- Validate clusters with domain experts
- Perform deeper statistical analysis on cluster stability
- Add cost analysis per cluster

---

## Project Structure
```
Healthcare/
│
├── Dataset.txt               # Source data
├── Healthcare.ipynb          # Main analysis notebook
|__ Metadata.md               # metadata of the dataset
└── README.md                 # Project documentation
```

---

## Author
Data Science & Machine Learning Project

## License
This project is for educational and analytical purposes.
