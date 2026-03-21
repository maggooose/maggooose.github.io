---
title: Creating a Scheduled Task using Window Task Scheduler
date:  2026-01-02 22:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on creating a scheduled task using windows task scheduler.
---

Windows task scheduler is used to run a python script on a scheduled time.

## Create a task
Open windows task scheduler and select `Create Task...` under Actions.

![img-description](../assets/images/windows-task-scheduler/actions_dropdown.jpg)
_Select "Create Task..."_

## General tab
![img-description](../assets/images/windows-task-scheduler/step_one_general.jpg)
_Select "Run whether user is logged on or not"_

## Triggers tab
![img-description](../assets/images/windows-task-scheduler/step_two_triggers.jpg)
_Select "New..." to create a new trigger_

![img-description](../assets/images/windows-task-scheduler/step_two_creating_schedule.jpg)
_Create a schedule_

## Actions tab
![img-description](../assets/images/windows-task-scheduler/step_three_actions.jpg)
_Select "New..." to create a new action_

![img-description](../assets/images/windows-task-scheduler/step_three_creating_actions.jpg)
_Fill in batch file and folder to start_

## Conditions tab
![img-description](../assets/images/windows-task-scheduler/step_four_conditions.jpg)
_Disable all options_

## Settings tab
![img-description](../assets/images/windows-task-scheduler/step_five_settings.jpg)
_Settings configuration_
