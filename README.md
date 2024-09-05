# Setting up a PostgreSQL server on Azure

All steps assume Linux.

## 1. Setup Environment

Download Azure Developer CLI
```bash
curl -fsSL https://aka.ms/install-azd.sh | bash
```

Download project code. It will ask for an environment name.
```bash
mkdir azure-postgresql
cd azure-postgresql
azd init -t azure-postgres-pgvector-python
```

Create a Python virtual environment and install the required packages
```bash
python -m venv <environment-name>
source <environment-name>/bin/activate
python -m pip install -r requirements.txt
```

## 2. Deploy to Azure

Login to Azure
```bash
azd auth login
```

Create a new azd environment. It will ask you for the environment name.
```bash
azd env new
```

Or entering an existing environment:
```bash
azd env list
azd env select <environment-name>
```

Modify the environment's `.env` file and configure it to your liking before provisioning.
```bash
nano .azure\<environment-name>\.env
```

```
AZURE_ENV_NAME=
ADMIN_LOGIN=
ADMIN_PASSWORD=
AZURE_LOCATION=
AZURE_SUBSCRIPTION_ID=
POSTGRES_DATABASE=
POSTGRES_HOST=
POSTGRES_SSL=
POSTGRES_USERNAME=
```

Create a new resource group with the PostreSQL server inside. 
```bash
azd provision
```

## 3. Access the server
```bash
psql -h [server FQDN] -p 5432 -U [username] [database name]
```


### References
https://github.com/Azure-Samples/azure-postgres-pgvector-python
https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/faq









