# DataFellowship8-Airflow
![image](https://user-images.githubusercontent.com/85284506/207533681-cff7d5fe-3703-45eb-816b-c390169f7619.png)

Deploy Airflow on Google Cloud Platform with Docker and create DAG script for ingesting data to Google Cloud Storage + Bigquery External Table


## Create access credentials
*   Go to https://cloud.google.com/iam/docs/creating-managing-service-accounts
*   Rename your gcp-service-accounts-credentials file to `google_credentials.json` & store it in your `$HOME` directory
*   cd ~ && mkdir -p ~/.google/credentials/
*   mv <path/to/your/service-account-authkeys>.json ~/.google/credentials/google_credentials.json

## Docker-compose settings
in your `docker-compose.yaml`:
   * In `x-airflow-common`: 
     * Remove the `image` tag, to replace it with your `build` from your Dockerfile, as shown
     * Mount your `google_credentials` in `volumes` section as read-only
     * Set environment variables: `GCP_PROJECT_ID`, `GCP_GCS_BUCKET`, `GOOGLE_APPLICATION_CREDENTIALS` & `AIRFLOW_CONN_GOOGLE_CLOUD_DEFAULT`, as per your config.
   * Change `AIRFLOW__CORE__LOAD_EXAMPLES` to `false` (optional)
   
 ## Run 'docker compose up'
![WebUI](https://user-images.githubusercontent.com/85284506/206387162-4550fac3-0b91-4a2d-903e-8946c22c7509.jpg)

## DAG Task
```call_dataset_task >> save_as_csv_task >> format_to_parquet_task >> local_to_gcs_task >> bigquery_external_table_task```
+ call_dataset_task: Extracing `.json` data from a URL
+ save_as_csv_task: format `.json` downloaded files to `.csv`
+ format_to_parquet_task: format format `.csv` file to `.parquet`
+ local_to_gcs_task: Load the data to Google Cloud Storage
+ bigquery_external_table_task: Create external table on Bigquery from Google Cloud Storage file
