## Black Friday Sales Prediction on GCP

This document outlines the design and implementation of a Black Friday sales prediction solution using Google Cloud Platform (GCP) services.

**1. Data Source and Storage:**

- **Dataset:** Black Friday sales data.
- **Storage:** Google BigQuery serves as the data warehouse for storing the raw dataset.

**2. Data Preprocessing:**

Data preprocessing is performed using the following techniques:

- **One-hot Encoding:** Categorical features in the dataset are converted into numerical representations using one-hot encoding, making it suitable for machine learning algorithms.
- **Random Sampling:** To ensure efficient model training and evaluation, random sampling is applied to the dataset. This technique selects a representative subset of the data.

**3. Model Training:**

- **Algorithm:** Random Forest Regressor, a powerful ensemble learning method, is employed for sales prediction due to its ability to handle complex relationships within the data.

**4. Model Evaluation:**

- **Metrics:** The performance of the trained Random Forest Regressor is evaluated using the following metrics:
- **R-squared (R2):** Measures the proportion of variance in the target variable (sales) that is explained by the model.
- **Mean Absolute Error (MAE):** Represents the average absolute difference between the predicted sales values and the actual sales values.

**5. Pipeline Automation and Training:**

- **Vertex AI Pipelines:** Vertex AI Pipelines orchestrates the entire machine learning workflow, automating the process of data preprocessing, model training, and model evaluation. This automation ensures reproducibility and simplifies the retraining process.
- **Recurrent Training:** Vertex AI Pipelines enables recurrent training, allowing the model to stay updated with new data and maintain prediction accuracy over time.

**6. Model Deployment and Serving:**

- **Vertex AI Endpoints:** Trained Random Forest Regressor model is deployed to Vertex AI Endpoints for real-time prediction serving. This deployment option provides a scalable and managed environment for making sales predictions on new, unseen data.

**Workflow Diagram:**

```
+-----------------+
| BigQuery Dataset |
+-----------------+
|
| Data Extraction
v
+-----------------+
| Data Preprocessing |
| - One-hot Encoding |
| - Random Sampling |
+-----------------+
|
v
+-----------------+
| Model Training |
| - Random Forest |
+-----------------+
|
v
+-----------------+
| Model Evaluation |
| - R2, MAE |
+-----------------+
|
v
+--------+----------+
| Vertex AI Pipeline |
+--------+----------+
|
+------+-------+
| Deployment |
+------+-------+
|
v
+-----------------+
| Vertex AI Endpoint |
+-----------------+
|
| Real-time Predictions
v
+-----------------+
| Applications |
+-----------------+
```

**7. How to run:**

- **Dependencies:** install dependencies using 
``` pip install -r requirements.txt ```

- **Auth:** Please use your own Service Account on GCP

- **Run the Pipeline**

    - **Run all the kubeflow notebook code with this additional information:**
    -   **PROJECT_ID**: Google Cloud project id.
    -   **display_name**: The name displayed in the AI Platform for this pipeline job.
    -   **template_path**: The path to the pipeline YAML file which defines the structure and components of the pipeline.
    -   **PIPELINE_ROOT**: The root directory in Google Cloud Storage where the pipeline artifacts will be stored.
    -   **enable_caching**: A boolean flag to disable caching of pipeline steps to ensure the pipeline runs from scratch each time.
    -   **config.yaml**: A config file for customizing your pipeline, in this case just adding project id, region, and model name.

- **Vertex AI Endpoints:** Trained Random Forest Regressor model is deployed to Vertex AI Endpoints for real-time prediction serving. This deployment option provides a scalable and managed environment for making sales predictions on new, unseen data.