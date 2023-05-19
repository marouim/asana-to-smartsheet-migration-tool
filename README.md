# Transfer from Asana to SmartSheet using Ansible


This project aim to help people transfer tasks from Asana to Smartsheet using Ansible. 
<p>
The project contains 4 playbooks to help migrate the tasks. 
<p>

### 1 - Set the variables in group_vars/all.yaml

You need to populate your Asana and Smartsheet tokens in the variable file. 

### 2 - Get all portfolios IDs from Asana

Before you start the migration, you need to get the ID of the porfolios you want to transfer. 

```
ansible-playbook get-all-portfolios-from-asana.yaml
```

Set group_vars/all.yaml/portfolio_id with the portfolio you want to import. 

### 3 - Get all workspaces IDs from SmartSheet

I recommend that you create empty workspaces to host the projects that will be imported. 

Example, if your workspace name is supposed to be ANSIBLE, then create a workspace ANSIBLE-import directly in SmartSheet. 

Create the workspace in SmartSheet before running the following playbook. 

```
ansible-playbook get-all-workspace-from-smartsheet.yaml
```

Set group_vars/all.yaml/dest_workspace_id with the destination workspace in SmartSheet.

### 4 - Get the SmartSheet template ID

New SmartSheets will be created based on a template. I recommand you create a template that has, at least the following column: 

Name:
Create date:
Due date:
Assigned to:
Status:
Comments: 

Once created, run the following playbook. 

```
ansible-playbook get-all-template-from-smartsheet.yaml
```

Set group_vars/all.yaml/dest_template_id with the ID of the template you want to use for your imported projects. 

### 5 - Launch portfolio migration

Once all variables are set in group_vars/all.yaml, launch the migration playbook. 

The following playbook will create one SmartSheet per Asana project from the specified Asana Portfolio. 

All the tasks of the project will be convert into a Row in SmartSheet and all the comments of each task will be placed in the Comments column. 

Attachment will be added as line at the end of the new sheet. 

Note: Some attachement such as PDF and image need to be transfered manually. Google drive links works. 

```
ansible-playbook migrate-portfolio-to-workspace.yaml
```

### 6 - Wait and go get a coffee

The process can takes few minutes depending of the number of projects and tasks. 


