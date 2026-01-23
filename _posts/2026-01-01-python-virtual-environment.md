---
title: Python Virtual Environment
date:  2026-01-01 22:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on creating a virtual environment for Python.
---

Virtual environment is a tool used to create isolated, self-contained directories for each Python project, which prevents conflicts between different project dependencies.

## Creating the virtual environment
Enter the command line and proceed to the folder with the Python script to create a virtual environment.
In the example below, the virtual enviroment with the name "myenv" will be created in the same directory.

```shell
python -m venv myenv
```

## Activating the virtual environment
Before staring any project, activate the virtual enviroment and pip install the necessary libraries to be used for the project. 
This virtual enviroment should always be activated when developing or running the Python script.

```shell
myenv\Scripts\activate
```

## Deactivating the virtual environment
To deactivate the virtual enviroment, simply type "deactivate" inside the command prompt.

```shell
deactivate
```

## Creating a snapshot of the virutal enviroment
After development has been completed and all relevant packages and libraries have been installed inside the virutal enviroment, perform a snapshot of the project's dependencies which will allow easy replication of the same exact environment on another machine for deployment.
```shell
pip freeze > requirements.txt
```

## Recreating the environment
To install the packages listed in the generated `requirements.txt` file in a new virtual environment, activate the new virtual environment and use the following command.
```shell
pip install -r requirements.txt
```
