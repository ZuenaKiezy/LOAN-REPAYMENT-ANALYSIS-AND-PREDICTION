# LOAN-REPAYMENT-ANALYSIS-AND-PREDICTION

This repository contains a project that focuses on analyzing loan data and building predictive models to forecast loan outcomes. The analysis includes exploring various factors that influence loan approval, repayment, and defaults. A predictive model is developed to predict whether a loan will be approved or if a borrower will default on the loan based on historical data.

## Project Overview

The goal of this project is to:
- Perform exploratory data analysis (EDA) on loan data to identify trends, patterns, and key factors influencing loan outcomes.
- Build and evaluate machine learning models to predict loan repayment and borrower default.
- Gain insights from the data that can help in decision-making for financial institutions.

## Data

The dataset contains information about various loan status and borrower details, including:
- **Loan Status**: The status of the loan amount requested by the borrower.
- **Principal**: The amount loaned out to the borrower.
- **Terms**: The length of the loan.
- **Age**: The borrower's age, which influences loan repayment.
- **Education**: Whether the borrower is in collage, High School and Below, Bachelor or has a Masters and Above.
- **Gender**: Whether the borrower of the loan is male or female.     |

## Steps to Reproduce the Analysis

1. **Install Dependencies:**

   Clone the repository and install the required libraries.

   ```bash
   git clone https://github.com/ZuenaKiezy/LOAN-REPAYMENT-ANALYSIS-AND-PREDICTION.git
   cd LOAN-REPAYMENT-ANALYSIS-AND-PREDICTION
   pip install -r requirements.txt
   ```

   Dependencies may include:
   - `pandas`: For data manipulation and analysis.
   - `numpy`: For numerical operations.
   - `matplotlib` and `seaborn`: For data visualization.
   - `scikit-learn`: For building machine learning models.
   - `xgboost`: For advanced boosting models.

2. **Data Preprocessing:**

   Load the dataset and preprocess it:
   - Handle missing values.
   - Parse dates and calculate past due days
   - Convert categorical features into numerical form (e.g., using one-hot encoding).
   - Split the data into training and testing sets.

   Example:

   ```python
   import pandas as pd
   from sklearn.model_selection import train_test_split
   from sklearn.preprocessing import StandardScaler

   # Load dataset
   data = pd.read_csv('Loan payments data.csv')

   # Handle missing values
   data = data.dropna()

   # Convert categorical data
   data = pd.get_dummies(data, drop_first=True)

   # Split data into features and target variable
   X = data.drop('Loan Status', axis=1)
   y = data['Loan Status']

   # Train-test split
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

   # Feature scaling
   scaler = StandardScaler()
   X_train = scaler.fit_transform(X_train)
   X_test = scaler.transform(X_test)
   ```

3. **Exploratory Data Analysis (EDA):**

   Use various visualization techniques to analyze the data and look for patterns.
   - Distribution of loan amounts and income.
   - Correlation heatmaps to check relationships between features.
   - Visualizing loan approvals and defaults.

   Example:

   ```python
   import seaborn as sns
   import matplotlib.pyplot as plt

   # Plot the distribution of loan amounts
   sns.histplot(data['Loan Amount'], kde=True)
   plt.title('Loan Amount Distribution')
   plt.show()

   # Correlation heatmap
   correlation_matrix = data.corr()
   sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
   plt.title('Correlation Heatmap')
   plt.show()
   ```

4. **Model Building:**

   Choose an appropriate machine learning algorithm to predict loan defaults or approval. Common algorithms include:
   - Logistic Regression
   - Random Forest
   - Support Vector Machines (SVM)
   - XGBoost

   Example:

   ```python
   from sklearn.ensemble import RandomForestClassifier
   from sklearn.metrics import classification_report, confusion_matrix

   # Train a random forest classifier
   model = RandomForestClassifier(n_estimators=100, random_state=42)
   model.fit(X_train, y_train)

   # Predictions
   y_pred = model.predict(X_test)

   # Evaluate the model
   print(classification_report(y_test, y_pred))
   print(confusion_matrix(y_test, y_pred))
   ```

5. **Model Evaluation:**

   Evaluate the performance of your model using various metrics:
   - Accuracy
   - Precision, Recall, F1-score
   - Confusion Matrix
   - ROC Curve

   Example:

   ```python
   from sklearn.metrics import roc_auc_score

   # Calculate ROC-AUC score
   roc_auc = roc_auc_score(y_test, model.predict_proba(X_test)[:, 1])
   print(f'ROC-AUC Score: {roc_auc}')
   ```

## Conclusion

This project serves as an in-depth guide to analyzing loan data and predicting loan outcomes. By using machine learning techniques, we can gain insights into the loan approval process and help financial institutions make better decisions.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- The dataset is from Kaggle datasets.
- Special thanks to the contributors and libraries that made this project possible.
