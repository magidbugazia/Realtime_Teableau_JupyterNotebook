# Realtime_Teableau_JupyterNotebook
Real-time connection between Tableau and Jupyter Notebook allowing for dynamic access to data

## Jupytab has two components; `Jupytab` and `Jupytab-server`:

###### We will be installing each component in a separate environment

### 1. Setup jupytab notebook environment:

   - In Terminal, we first create a virtual environment. Run the commands: 

```conda create -n jupytab-notebook-env python=3.9.6```

```conda activate jupytab-notebook-env```

   - Install jupytab and the ipykernel library to make our Jupyter kernel available in notebooks:

```conda install jupytab=0.9.11```

```conda install ipykernel```

```python -m ipykernel install --user --name jupytab-notebook-env --display-name "jupytab-outlook-python-tableau"```

###### here "--name" is the name of the env we want to install the kernel to, then "--display-name" is the kernel name we want to see inside jupyter notebook

   - Install and launch jupyter notebook:

``conda install jupyter``

``jupyter notebook``

  - In Jupyter Notebook, open the new kernel and run the following code to test that jupytab has been installed correctly

```python
import jupytab
print(jupytab.__version__)
```

### 2. Setup jupytab-server environment:

 - In terminal, deactivate current running environment: `conda deactivate`
 - Create new server environment: `conda create -n jupytab-server-env python` `conda activate jupytab-server-env`
 - Install jupytab-server: `conda install jupytab-server`

### 3. In Jupyter Notebook 

In your new Jupyter Notebook kernel we created, Upload your own dataframe/frames that you're trying to push into Tableau. I will be using this project as a sequel to my [Fetching-attachements-Microsoft-Outlook](https://github.com/magidbugazia/Fetching-attachements-Microsoft-Outlook.git) repository to form a real-time 3-way connection between my `Outlook-365 email`, `Python Jupyter Notebook`, and `Tableau Server`.


### 4. Connect to Tableau Server

 - Load the dataframe in a Jupytab Tables dictionary, to indicate that we want to expose it to Tableau:

```python
tables = jupytab.Tables()
tables['Data'] = jupytab.DataFrameTable("Data", dataframe=Data, include_index=True)
tables
```

Expose tables schema:- In order to allow jupytab-server to retrieve data

  - generates a schema that declares all our Dataframes

```python
# GET /schema
tables.render_schema()
```
   - Where data is exported:

In Terminal: `conda install flask`

In Jupyter Notebook:

```python
# GET /data
try:
    tables.render_data(REQUEST)
except NameError:
    print("Not available outside jupytab context")
```

### 5. Configure and Launch the Jupytab server

In the Jupytab server environment, we need to create a `configuration file` that will allow us to configure a few parameters like the server port, a secret token and of course the list of notebooks that the server must exposes. The `config.ini` file tells Jupytab which notebooks contain the tables that should be published for Tableau

  - Write a config.ini file in any text editer. Put it anywhere you want. preferrably in the same environment you're working in:


```[main]
listen_port = 8123
notebooks = SalesData_Outlook_Python_Tableau

[YOUR_PYTHON_NOTEBOOK_NAME]
path = /Users/PATH_TO_YOUR_PYTHON_NOTRBOOK/YOUR_PYTHON_NOTEBOOK.ipynb
description = GIVE THE CONNECTION A BRIEF DESCRIPTION
```

 - in terminal: In the jupytab server environment, Launch the jubytab: 

```jupytab --config=/Users/PATH_TO_YOUR_config_FILE/config.ini```

The ouput contains two important pieces of information:

1. The list of published notebooks.
2. The URL to be used in Tableau in order to access the data (including any security token declared in the configuration file).

###### `NOTE:` this migh give a jupytab command not found in terminal. this is because the intended command you’re attempting to use is located in a nonstandard directory or in another location (/usr/local/sbin/ etc).

##### Quick Fix: 
  - a. In terminal run print out the current paths in use: 

(jupytab-server-env) `echo $PATH`

  - b. add the new directory (where jupytab exists) to our path lits using:

(jupytab-server-env) `export PATH=$PATH:/Users/YOUR_JUPYTAB_PATH`

- back to ourout put from launching Jupytab:

Grab the link from the output

