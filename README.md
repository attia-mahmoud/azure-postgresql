# Setting up a PostgreSQL server on Azure

All steps assume Linux.

## 1. Setup Environment

Download Azure Developer CLI
```bash
curl -fsSL https://aka.ms/install-azd.sh | bash
```

Download project code
```bash
mkdir azure-postgresql
cd azure-postgresql
azd init -t azure-postgres-pgvector-python
```

Create a Python virtual environment and install the required packages
```bash
python -m venv venv
source venv/bin/activate
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

Copy the default environment variables into you local `.env` and configure them to your liking before provisioning.
```bash
azd env get-values > .env
```

Create a new resource group with the PostreSQL server inside. 
```bash
azd provision
```

## 3. Access the server
```bash
psql -h [server FQDN] -p 5432 -U [username] [database name]
```













