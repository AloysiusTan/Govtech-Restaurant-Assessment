# Govtech-Restaurant-Assessment

This project extracts and processes restaurant event data from a JSON dataset, focusing on events that occurred in April 2019. The results are stored in a CSV file for further analysis.

## 1. Instructions on How to Run the Source Code Locally

### Prerequisites
- Python 3.x installed on your system.
- `pip` package manager to install dependencies.
- Internet connection to download the required data files.

### Installation
1. **Clone the Repository**:
    ```bash
    git clone https://github.com/AloysiusTan/Govtech-Restaurant-Assessment
    cd Govtech-Restaurant-Assessment
    ```

2. **Create a Virtual Environment (Optional but Recommended)**:
    ```bash
    python -m venv venv
    source venv/bin/activate   # On Windows use: venv\Scripts\activate
    ```

### Running the Code

1. **Running in Jupyter Notebook**:
    - Open the Jupyter notebook (`main.ipynb`) in your Jupyter environment.
    - Simply click **Run All** to execute all cells. The notebook will automatically retrieve the necessary data files, process them, and generate the `restaurants.csv` and `restaurant_events.csv` file in the project directory.

2. **Running as a Python Script**:
    - If you prefer to run the code as a script or plan to deploy it in a production environment, convert the notebook to a `.py` script.
    - To convert the notebook to a script:
        ```bash
        jupyter nbconvert --to script main.ipynb
        ```
    - Once converted, you can run the script using:
        ```bash
        python main.py
        ```
    - The script will perform the same operations, retrieving data, processing it, and saving the output as `restaurants.csv` and `restaurant_events.csv`.
  
## 2. Summary of Cloud Design and Deployment

### Design Overview
To design and deploy this solution using cloud services, the following architecture would be considered:

- **Data Ingestion**:
    - The `restaurant_data.json` and `country_codes.xlsx` files would be stored in an Amazon S3 bucket. S3 provides durable, scalable, and highly available storage for the data.
  
- **Data Processing**:
    - AWS Lambda functions can be used to process the data. Lambda is a serverless compute service that can automatically scale and handle the data processing tasks.
    - The JSON data would be processed and filtered in Lambda to extract events occurring in April 2019.
    - The processed data would then be converted to a CSV file and stored back in the S3 bucket.

- **Storage and Access**:
    - The output CSV file will be stored in another S3 bucket or a designated folder in the same bucket. This will allow easy access and integration with other services, such as AWS Athena or Redshift for querying and further analysis.

- **Deployment Considerations**:
    - **Scalability**: AWS Lambda automatically scales based on the load, ensuring that the solution can handle large datasets without manual intervention.
    - **Cost**: Since Lambda is serverless, costs are incurred only when the code is running. S3 storage is also cost-effective and scalable.
    - **Security**: Access to the S3 bucket would be controlled using IAM roles and policies, ensuring that only authorized users and services can access the data.

### Decisions and Considerations
- **Serverless Approach**: Using AWS Lambda and S3 allows for a fully serverless architecture, which reduces management overhead and automatically scales with usage.
- **Data Durability**: S3's inherent durability ensures that the data is safe from loss.
- **Flexibility**: The use of S3 and Lambda allows for easy integration with other AWS services like Athena, Redshift, or even SageMaker for further analysis or machine learning tasks.

## 3. Architecture Diagram

Below is a diagram describing the infrastructure components and how they interact:

<insert image>
    
### Explanation:
- **Amazon S3 (Raw Data Storage)**: Stores the raw data files such as `restaurant_data.json` and `country_codes.xlsx`.
- **AWS Lambda (Data Processing)**: Handles the processing of the raw data to extract relevant events, filter by date, and generate a CSV file.
- **Amazon S3 (Processed Data Storage - CSV)**: Stores the final processed data in a CSV format, ready for further analysis or download.

