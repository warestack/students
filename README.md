## Part 1: Create a Virtual Machine (VM)

* Follow the instructions to create a VM.

### Install Jupyter Notebook on GCP.

Ensure you have Python installed on your machine. Jupyter Notebook supports Python 3.3 or later. You can install Python 3 by executing:

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
```

### Step 1: Install pip

`pip` is a package manager for Python. It's used to install and manage Python libraries. Execute the following command to install pip for Python 3:

```
sudo apt install python3 python3-pip -y
```

### Step 2: Upgrade pip (Optional)

It’s a good practice to have the latest version of pip. Upgrade pip using the following command:

```
pip install --upgrade pip
```

### Step 3: Install Jupyter Notebook

Now, install Jupyter Notebook using pip:

```
pip3 install jupyter
```

>  **Close your SSH windows, and start again.**

### Step 4: Start and Access Jupyter Notebook

Launch Jupyter Notebook by executing the following command:

```
jupyter notebook --ip='*' --NotebookApp.token='' --NotebookApp.password=''
```

Or

```
~/.local/bin/jupyter-notebook --ip='*' --NotebookApp.token='' --NotebookApp.password=''
```

If you like you can setup a token or password:

```
~/.local/bin/jupyter-notebook --ip='*' --NotebookApp.token='supersecret1234' --NotebookApp.password=''
```

On GCP, open port `8888` or allow access to all.

* Click on `default`

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/assets/1-network.png)

* Acces the firewall

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/assets/2-Firewalls.png)

* Add a new rule.

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/assets/3-Filrewall-rule.png)

* Create the rule and save it.

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/assets/4-Create-rule.png)

* Return back to your VM instances.

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/students/assets/5-VM instances.png)

* Open your web browser and type the following URL:

![1-network](/Users/steliossotiriadis/Dropbox/AA-Birkbeck/AA-Training/students/assets/5-VM-instances.png)

```
http://{your-ip}:8888/
```

## Part 2: Create a bucket

* Follow the instructions to create a Bucket.
* Load the following data:
  * https://www.dropbox.com/scl/fi/q016d9qrxfu3jh41sz3df/Biostats.csv?rlkey=792o3g9s6c0f9plw1kl7ispz0&dl=0

## Part 3: Create a new dataset on BigQuery

* Follow the instructions to create a dataset in BigQuery.

## Part 4: Access the data from Python

* Create a new IAM policy for BigQuery
  * Create a new service account.
  * Create a new principal for the service account.
  * Generate a new key for the new service account.
* Create a new script to extract data.

```
!pip install google-cloud-bigquery

from google.cloud import bigquery
from google.oauth2 import service_account

credentialsPath = r'YOUR_KEY.json'

credentials = service_account.Credentials.from_service_account_file(credentialsPath)

client = bigquery.Client(credentials=credentials)

query = 'CALL YOUR_PROJECT_ID.mydata.biostats'

results = client.query(query)

print(results)

query = client.query("""
  SELECT * FROM `YOUR_PROJECT_ID.mydata.biostats` LIMIT 1000
 """)
 
results = query.result()
for row in results:
	print(row)
```

## Part 5: Access the data from Python

1. Update your VM

```
sudo apt-get update
```

2. Install python

```
sudo apt-get install python3-pip
```

3. Download Ollama

```
curl -fsSL https://ollama.com/install.sh | sh
```

4. Run the model

```
ollama run llama2
```

5. Ask a question!

6. Create a Modelfile

```
FROM llama2

# set the temperature to 1 [higher is more creative, lower is more coherent]
PARAMETER temperature 1

# set the system message
SYSTEM """
You are Mario from Super Mario Bros. Answer as Mario, the assistant, only.
"""
```

7. Next, create and run the model:

```
ollama create mario -f ./Modelfile
```

Then

```
ollama run mario
```

Discuss with Mario!

8. Install Ollama library

```
pip install ollama
```

9. Create a new Python script

```
import ollama
response = ollama.chat(model='llama2', messages=[
  {
    'role': 'user',
    'content': 'Who is Bowser',
  },
])
print(response['message']['content'])
```

10. Run it!
