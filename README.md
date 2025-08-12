![image alt](https://github.com/fran-cornachione/Databricks-ETL/blob/9c19ecf5be783626881439feb9d13173bc446d90/Cover.png)

# ¡IMPORTANT!

This Workflow is meant to be run on **Databricks**. If you try running it on Visual Studio Code, Google Colab, or any other environment, It will not work properly.

(No need to install PySpark since it comes pre-installed in Databricks)

---

## Project Structure

**raw_data:** Contains the raw `.csv` files, with default schema
**bronze_layer:** Contains the `.csv` files, with **defined schema**


## Virtual Environment

* **Create a virtual environment:** `python -m venv <virtual-environment-name>`
* **Activate it:** `.\<virtual-environment-name>\Scripts\Activate.ps1`
* **Clone repo:** `git clone https://github.com/fran-cornachione/Databricks-ETL`
* **Install requirements:** `pip install -r requirements.txt`


## AWS

* Go to AWS --> Users --> Create User
* **Username:** Insert any name (e.g: `boto3-user`)
* **Permissions:** Select "Attach policies directly"
* Select `AmazonS3FullAccess`
* Click on the user you just created
* Select "**Create Access key**"
* Select "**Application running outside AWS**"

## Databricks

It will provide you the **Access Key** and **Secret Access Key** (you can only see it **once**, make sure to **save it**)

1. Go to Databricks --> User --> Settings --> Developer --> Access Tokens --> Manage
2. Click **"Generate new token"**
3. Copy your token (you can only see it once)

`databricks configure --token`

"**Databricks Host (should begin with https://):**" Insert your Databricks host (`https://<your-workspace>.cloud.databricks.com`)

**Token:** Insert your Databricks Token

1. `databricks secrets create-scope <scope-name>`
2. `databricks secrets put-secret <scope-name> AWS_ACCESS_KEY_ID`
3. Insert your **AWS Access Key**
4. `databricks secrets put-secret <scope-name> AWS_SECRET_ACCESS_KEY`
5. Insert your **AWS Secret Access Key**

Now, in the `Load.ipynb` script, replace with your credentials:

```
scope_name = <your-scope-name>
ACCESS_KEY = dbutils.secrets.get(scope=scope_name, key="AWS_ACCESS_KEY_ID") # Your AWS Access Key
SECRET_KEY = dbutils.secrets.get(scope=scope_name, key="AWS_SECRET_ACCESS_KEY") # Your AWS Secret Key
AWS_BUCKET_NAME = "bucket-name" # Your S3 Bucket Name
```
