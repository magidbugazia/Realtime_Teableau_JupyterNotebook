# Realtime_Teableau_JupyterNotebook
Real-time connection between Tableau and Jupyter Notebook allowing for dynamic access to data

## Jupytab has two components; `Jupytab` and `Jupytab-server`:

###### We will be installing each component in a separate environment

- Environment 1 - jupytab notebook environment:

  - In Terminal, we first create a virtual environment. Run the commands: 

```conda create -n jupytab-notebook-env python=3.9.6```

```conda activate jupytab-notebook-env```

  - Install jupytab and the ipykernel library to make our Jupyter kernel available in notebooks:

```conda install jupytab=0.9.11```

```conda install ipykernel```

```python -m ipykernel install --user --name jupytab-notebook-env --display-name "jupytab-outlook-python-tablea"```

###### here "--name" is the name of the env we want to install the kernel to, then "--display-name" is the kernel name we want to see inside jupyter notebook

- Install and launch jupyter notebook:


``conda install jupyter``

``jupyter notebook``
