# Model Training Explanation

## Criteria Applied for Training the Model

To predict whether a product in the marketplace is **new** or **used**, the following protocol was followed:

1. **Data Loading**  
   - Started from the `clean_data.csv` file, produced by the EDA and cleaning of `MLA_100k.jsonlines`.

2. **Data Preprocessing**  
   - **Target Encoding**:  
     - The `condition` column was converted to numeric values (0 = used, 1 = new) using `LabelEncoder`.  
   - **One-Hot Encoding**:  
     - Categorical variables (`listing_type_id`, `buying_mode`, `status`, `mode`) were turned into dummy variables.  
   - **Train/Test Split**:  
     - Data were split into 80% train and 20% test using `train_test_split(random_state=42)`.

3. **Features Used**  
   The model was trained on the following features derived from the cleaned dataset:  
   - **Numeric & Boolean**  
     - `price`  
     - `accepts_mercadopago`  
     - `automatic_relist`  
     - `initial_quantity`  
     - `available_quantity`  
     - `free_shipping`  
     - `local_pick_up`  
   - **One-Hot Encoded Categories**  
     - `listing_type_id_<type>`  
     - `buying_mode_<mode>`  
     - `status_<status>`  
     - `mode_<shipping_mode>`

4. **Model Selection**  
   Four “out-of-the-box” algorithms were evaluated:

   - **Logistic Regression** (`LogisticRegression(max_iter=1000)`)  
   - **Decision Tree** (`DecisionTreeClassifier(random_state=42)`)  
   - **Random Forest** (`RandomForestClassifier(n_estimators=100, random_state=42)`)  
   - **XGBoost** (`XGBClassifier(use_label_encoder=False, eval_metric='mlogloss')`)

5. **Training and Prediction**  
   Each classifier was fit on the training data and then made predictions on the test set.

6. **Evaluation Metrics**  
   The following metrics were computed for each model:  
   - **Accuracy** (`accuracy_score`)  
   - **Precision** (`precision_score`)  
   - **Recall** (`recall_score`)  
   - **F1-Score** (`f1_score`)

---

## Model Performance

| Model                  | Accuracy | Precision | Recall | F1-Score |
|------------------------|:--------:|:---------:|:------:|:--------:|
| **Logistic Regression**| 0.5338   | 0.0000    | 0.0000 | 0.0000   |
| **Decision Tree**      | 0.8216   | 0.7825    | 0.8551 | 0.8172   |
| **Random Forest**      | 0.8243   | 0.7819    | 0.8642 | 0.8210   |
| **XGBoost**           | **0.8285** | **0.8049** | **0.8344** | **0.8194** |

---

## Conclusion

The model training and evaluation process identified XGBoost as the most suitable algorithm for predicting whether an item in the marketplace is new or used. This model not only struck the best balance between accuracy, precision, recall, and F1-score, but also proved resilient to non-linear patterns and mild class imbalance. 