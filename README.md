# DBT Delta Lake Integration
Databricks Delta Lake Integration Demo

- [DBT Delta Lake Integration](#dbt-delta-lake-integration)
- [Follow up Sources](#follow-up-sources)
- [Libraries Used](#libraries-used)
- [Setup](#setup)
  - [Install requirements](#install-requirements)
    - [Install DBT](#install-dbt)
    - [Install Databricks ODBC Driver](#install-databricks-odbc-driver)
  - [Start a DBT Project](#start-a-dbt-project)
  - [Configure Databricks Profile](#configure-databricks-profile)

# Follow up Sources
* [dbt + Databricks : Bringing analytics engineering to the lakehouse](https://blog.getdbt.com/analyticsengineeringwithdbtanddatabricks/)
* [dbt-spark Github](https://github.com/fishtown-analytics/dbt-spark)

# Libraries Used
* dbt-core
* dbt-spark
* pyodbc==4.0.30

# Setup

## Install requirements

### Install DBT
DBT is a python based framework that allows execution of SQL against different data warehouse backends. The requirements for DBT are listed in a `requirements.txt` in the top level of this repo. See [dbt installation guide](https://github.com/fishtown-analytics/dbt-spark#installation) for more details. 

Run the following code below to install the tested requirements.

```sh
pip3 install -r requirements.txt
```

### Install Databricks ODBC Driver
Go to [Databricks Driver Download](https://databricks.com/spark/odbc-driver-download?_ga=2.129606796.1443837543.1614615613-1207879976.1601929408) to download the needed `simba driver`. Extract the ODBC driver and install it. 

## Start a DBT Project
DBT repos are organized with a projects hieararchy. Hence the top level of any DBT repo will be a project. See [creating a dbt project](https://docs.getdbt.com/docs/building-a-dbt-project/projects) for more details.

Run the following code below to create a new project named `delta_lake_demo` 

```sh
dbt init delta_lake_demo --adapter spark
```

A new folder named `delta_lake_demo` should now appear. Note, a project will already exist in this folder for demonstration purposes.

## Configure Databricks Profile
DBT spark configuration requires changing the following values in your `~/.dbt/profiles.yml`. See [configuring your profile](https://github.com/fishtown-analytics/dbt-spark#configuring-your-profile) for more details.

Change the following values in your `~/.dbt/profiles.yml` to configure your DBT connection.

|field|Description|Value|
|-----|-----------|-----|
|method| Method to connect to Databricks|spark|
|schema| Database to connect to| dbt|
|port| Port on Databricks cluster to connect to | 443|
|token | Databricks login token | Obtain this token from the Databricks UI or from `~/.databrickscfg`|
|cluster | ID of running cluster to connect to| See [cluster details](https://docs.databricks.com/integrations/bi/jdbc-odbc-bi.html#get-server-hostname-port-http-path-and-jdbc-url) for more details.|