# DataFellowship8-Airflow
Deploy Airflow on Google Cloud Platform with Docker
by Yuditya Mulia Insani - DF8

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
