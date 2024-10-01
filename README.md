# ChEMBL Bioactivity Data Analysis for HDAC2

## Problem Definition
This project focuses on retrieving, processing, and analyzing bioactivity data for Histone Deacetylase 2 (HDAC2) using the ChEMBL database. HDAC2 is an important target in cancer research, and understanding its interaction with various compounds can help identify potential drug candidates.

## Project Steps

1. **Loading Libraries and Data**:
    - Installed essential libraries including `chembl-webresource-client`, `RDKit`, and `Mordred`.
    - Retrieved target data for HDAC2 using ChEMBL's API.

2. **Bioactivity Data Retrieval**:
    - Queried bioactivity data for HDAC2, focusing on the IC50 metric to measure compound effectiveness.
    - Filtered and cleaned the dataset, removing entries with missing `standard_value` (bioactivity measurements) and `canonical_smiles` (molecular structure).

3. **Data Cleaning and Preprocessing**:
    - Identified and handled missing data by dropping entries without key bioactivity measures.
    - Ensured uniqueness of compounds by filtering based on `canonical_smiles`.

4. **Descriptor Calculation**:
    - Used `RDKit` to calculate molecular descriptors and applied Lipinski’s rule of five to evaluate drug-likeness.
    - Generated molecular fingerprints and calculated 2D descriptors for the compounds using `Mordred`.

5. **Exploratory Data Analysis (EDA)**:
    - Performed basic statistical analysis of bioactivity values.
    - Visualized distributions of IC50 values to understand the range and identify potential outliers.

6. **Model Building**:
    - **Data Splitting**: The dataset was split into training and testing sets using an 80/20 split.
    - **Feature Scaling**: Applied `RobustScaler` to normalize the feature set.
    - **Random Forest Regressor**: Built a Random Forest regression model to predict the pIC50 values of compounds, assessing the importance of molecular descriptors.
    - **Feature Selection**: Important features were identified using the Random Forest model's feature importance metric.
    - **Cross-Validation**: Employed cross-validation to fine-tune the model and select hyperparameters, optimizing using GridSearchCV.
    - **Other Models**: Additionally, experimented with other models such as `XGBoost`, `Linear Regression`, `K-Nearest Neighbors`, and `Ridge Regression`.

7. **Model Evaluation**:
    - The final Random Forest model was trained with optimal hyperparameters (`n_estimators=200`, `max_depth=20`, etc.).
    - The model was evaluated on the test set, yielding the following metrics:
        - **RMSE**: Root Mean Squared Error
        - **MAE**: Mean Absolute Error
        - **R²**: Coefficient of Determination
    - Based on the metrics, the Random Forest model was chosen as the best-performing model for predicting compound bioactivity.

8. **Prediction of New Ligands**:
    - A function was created to input new ligands, retrieve their molecular structure from ChEMBL, and predict their bioactivity (pIC50) using the trained model.

## Conclusions
The project successfully retrieved bioactivity data for HDAC2, cleaned and processed the data, and built several predictive models to assess compound effectiveness based on molecular structure. The Random Forest Regressor demonstrated the best performance, and the model is capable of predicting bioactivity for new ligands, providing valuable insights for drug discovery research.
