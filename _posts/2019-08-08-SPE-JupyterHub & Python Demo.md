---
layout:     post
title:      JupyterHub & Python Demo.md
subtitle:     
date:       2019-08-08
author:     Jiashu Miao
header-img: 
catalog: true
tags:
    - Python
    - Linux
    - Jupyter Server
    
---

# Jupyter on remote Linux server
------------------------------------------------
*Jupyter is an online service that all interactive computing using different programming languages across multiple users.*
##### Jupyter Notebook
[JupyterNotebook](http://localhost:8888/login)
- Accessibility & Security
    - access anywhere with internect connection 
    - username/password protect and secure files remotely [password protect](http://localhost:8888/login)
    - configure network, authtication, etc.  [config](https://github.com/michaelmiaomiao/SPE/blob/master/jupyter_notebook_config.py)
- Work Efficiency
	- file transformation, share and edit 
    - work as individuals / groups 
    - multiple programming languages Python, R, Julia etc. 
    - easy coding and running in cells
    - version controls with checkpoints 
    - visulization and interaction functiongs with Lab [Jupyterlab](https://hub.gke.mybinder.org/user/jupyterlab-jupyterlab-demo-dxmskblw/lab)
    - customization and preference setting 
    - good for demo / 

### JupyterHub 
[JupyterHub](http://usdl646.spe.sony.com:8888/hub/login)

- admin and general user 
- username folder / project fold [file name](http://usdl646.spe.sony.com:8888/user/tom/terminals/1)
- create/ban users generation (without neet to create system users) 
- users with third party and connection to github, sql, tableau etc. 
- ![img](https://jupyterhub.readthedocs.io/en/stable/_images/jhub-fluxogram.jpeg)

# Web-automation for data scraping: 
------------------------------------------------------------
[Code](http://localhost:8888/notebooks/Documents/web_automation.ipynb)
- easy to run and user frinedly 
- really convenient and can work on big data 
- efficent and customization 
- [data stored] (http://localhost:8888/tree/Documents/demodata)
