---
title: Python Virtual Environment
date:  2026-01-01 22:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on creating a virtual environment for Python.
---

Virtual environment is a tool used to create isolated, self-contained directories for each Python project, which prevents conflicts between different project dependencies.

## Code 
Enter the command line and proceed to the folder with the Python script to create a virtual environment.
In the example below, the virtual enviroment with the name "myenv" will be created in the same directory.

```shell
python -m venv myenv
```

Before staring any project, activate the virtual enviroment and pip install the necessary libraries to be used for the project. 
This virtual enviroment should always be activated when developing or running the Python script.

```shell
myenv\Scripts\activate
```

To deactivate the virtual enviroment, simply type "deactivate" inside the command prompt.

```shell
deactivate
```
