# Install necessary packages

```python
%pip install -r requirements.txt
```
# Part 1: Introduction to Classification & Evaluation

**Objective:** Load the synthetic health data, train a Logistic Regression model, and evaluate its performance.

## 1. Setup

Import necessary libraries.

```python
import pandas as pd
import numpy as np
import os
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix
from sklearn.impute import SimpleImputer
```

## 2. Data Loading

Implement the `load_data` function to read the dataset.

```python
def load_data(file_path):
    """
    Load the synthetic health data from a CSV file.
    
    Args:
        file_path: Path to the CSV file
        
    Returns:
        DataFrame containing the data
    """ 
    return pd.read_csv(file_path)
```

## 3. Data Preparation

Implement `prepare_data_part1` to select features, split data, and handle missing values.

```python
def prepare_data_part1(df, test_size=0.2, random_state=42):
    """
    Prepare data for modeling: select features, split into train/test sets, handle missing values.
    
    Args:
        df: Input DataFrame
        test_size: Proportion of data for testing
        random_state: Random seed for reproducibility
        
    Returns:
        X_train, X_test, y_train, y_test
    """
    # YOUR CODE HERE
    # 1. Select relevant features (age, systolic_bp, diastolic_bp, glucose_level, bmi)
    # 2. Select target variable (disease_outcome)
    # 3. Split data into training and testing sets
    # 4. Handle missing values using SimpleImputer
    
    rel_features = ['age', 'systolic_bp', 'diastolic_bp', 'glucose_level', 'bmi']
    target ='disease_outcome' 

    X = df[rel_features]
    y = df[target]

    # do imputation to deal with missing values
    imputer = SimpleImputer(strategy='mean')
    X_imputed = pd.DataFrame(imputer.fit_transform(X), columns=features)

    # Split
    X_train, X_test, y_train, y_test = train_test_split(
        X_imputed, y, test_size=test_size, random_state=random_state, stratify=y
    )

    # Placeholder return - replace with your implementation
    return X_train, X_test, y_train, y_test
```

## 4. Model Training

Implement `train_logistic_regression`.

```python
def train_logistic_regression(X_train, y_train):
    """
    Train a logistic regression model.
    
    Args:
        X_train: Training features
        y_train: Training target
        
    Returns:
        Trained logistic regression model
    """
    model = LogisticRegression(max_iter=1000)
    model.fit(X_train, y_train)
    
    return model  
```

## 5. Model Evaluation

Implement `calculate_evaluation_metrics` to assess the model's performance.

```python
def calculate_evaluation_metrics(model, X_test, y_test):
    y_pred = model.predict(X_test)
    y_proba = model.predict_proba(X_test)[:, 1]

    metrics = {
        'accuracy': accuracy_score(y_test, y_pred),
        'precision': precision_score(y_test, y_pred),
        'recall': recall_score(y_test, y_pred),
        'f1': f1_score(y_test, y_pred),
        'auc': roc_auc_score(y_test, y_proba),
        'confusion_matrix': confusion_matrix(y_test, y_pred).tolist()
    }
    return metrics
```

## 6. Save Results

Save the calculated metrics to a text file.

```python
# Create results directory and save metrics
def save_results(metrics, output_path='results/results_part1.txt'):
    os.makedirs(os.path.dirname(output_path), exist_ok=True)
    with open(output_path, 'w') as f:
        for key, value in metrics.items():
            if key != 'confusion_matrix':
                f.write(f"{key}: {value:.4f}\n")
            else:
                f.write(f"{key}:\n{np.array(value)}\n")

# 1. Create 'results' directory if it doesn't exist
# 2. Format metrics as strings
# 3. Write metrics to 'results/results_part1.txt'
```

## 7. Main Execution

Run the complete workflow.

```python
# Main execution
if __name__ == "__main__":
    # 1. Load data
    data_file = 'data/synthetic_health_data.csv'
    df = load_data(data_file)
    
    # 2. Prepare data
    X_train, X_test, y_train, y_test = prepare_data_part1(df)
    
    # 3. Train model
    model = train_logistic_regression(X_train, y_train)
    
    # 4. Evaluate model
    metrics = calculate_evaluation_metrics(model, X_test, y_test)
    
    # 5. Print metrics
    for metric, value in metrics.items():
        if metric != 'confusion_matrix':
            print(f"{metric}: {value:.4f}")
    
    # 6. Save results
    # (Your code for saving results)
    
    # 7. Interpret results
    interpretation = interpret_results(metrics)
    print("\nResults Interpretation:")
    for key, value in interpretation.items():
        print(f"{key}: {value}")
```

## 8. Interpret Results

Implement a function to analyze the model performance on imbalanced data.

```python
def interpret_results(metrics):
    """
    Analyze model performance on imbalanced data.
    
    Args:
        metrics: Dictionary containing evaluation metrics
        
    Returns:
        Dictionary with keys:
        - 'best_metric': Name of the metric that performed best
        - 'worst_metric': Name of the metric that performed worst
        - 'imbalance_impact_score': A score from 0-1 indicating how much
          the class imbalance affected results (0=no impact, 1=severe impact)
    """
    metric_values = {k: v for k, v in metrics.items() if k != 'confusion_matrix'}
    best_metric = max(metric_values, key=metric_values.get)
    worst_metric = min(metric_values, key=metric_values.get)

    # Estimate imbalance impact: large drop from accuracy to f1/recall implies more impact
    imbalance_impact = (
        abs(metrics['accuracy'] - metrics['f1']) +
        abs(metrics['accuracy'] - metrics['recall'])
    ) / 2
    imbalance_impact_score = min(1.0, round(imbalance_impact * 2, 2))
    # 1. Determine which metric performed best and worst
    # 2. Calculate an imbalance impact score based on the difference
    #    between accuracy and more imbalance-sensitive metrics like F1 or recall
    # 3. Return the results as a dictionary
    
    # Placeholder return - replace with your implementation
    return {
        'best_metric': best_metric,
        'worst_metric': worst_metric,
        'imbalance_impact_score': imbalance_impact_score
    }