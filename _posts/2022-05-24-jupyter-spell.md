---
layout: post
title: Spell Checker in Jupyter
categories: [Programming, Python]
---

In this post, I will show you how to automatically check for spell mistakes in your Jupyter notebooks. The steps to follow are those:

## Jupyter Notebook

Install [Jupyter notebook extensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions). This a is repository that contains a collection of extensions that add functionality to the Jupyter notebook.

To install the nbextensions using PIP, type the following in a terminal.

    pip install jupyter_contrib_nbextensions

If you are using Anaconda the recommended method is to use conda, as shown below.

    conda install -c conda-forge jupyter_contrib_nbextensions

Now, install the javascript and css files.

    jupyter contrib nbextension install --user

This should install the plugins and also the [configuration interface](https://github.com/Jupyter-contrib/jupyter_nbextensions_configurator). Open a new notebook from your terminal using the jupyter notebook command. It should open a window like this one. Click on "Nbextensions" at the top of the screen.

[![nbextensions](\assets\2022-05-24-jupyter-spell\nbextensions.png)](\assets\2022-05-24-jupyter-spell\nbextensions.png){:.glightbox}

## Jupyter Lab

Install [jupyterlab-spellchecker](https://github.com/jupyterlab-contrib/spellchecker).

For JupyterLab 3.x:

    pip install jupyterlab-spellchecker

or

    conda install -c conda-forge jupyterlab-spellchecker

Check [this](https://github.com/jupyterlab-contrib/spellchecker)
link for more information.
