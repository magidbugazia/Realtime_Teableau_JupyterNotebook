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
