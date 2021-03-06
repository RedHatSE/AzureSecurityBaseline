# AzureSecurityBaseline
Azure Security Baseline

Welcome to Our Demo of Ansible on Azure. 
    <br>- What is Ansible
    <br>- The basics of writing a playbook
    <br>- How to use Azure Resource Manager 
    <br>- Using Azure Resource Manager to handle templetes in Ansible. 

We are going to Use Red Hat Software Ansible to help with the Security Baseline Deployment & AZ-500 Deployment. 

Login to your Azure infrastructure & open up and AzureCLI. 

![image](images/azurecli.png)

After you click the shell you need to ensure it is in bash. You will see the following as Ansible is already installed.  

![image2](images/Azureansible.png)

I am going to Break Down a sample on an Ansible YAML File

``` 
- name: setup system 
# Above is a name comment and can be named whatever you would like

  hosts: localhost
# the Hosts: is an indication of were ansible is going to run the commands from. In this scenario we are going to run it right from the AzureCLI

  tasks:
# Everything Below this task line will be indented as it will be nested under Tasks. 

   - name: azure create resource group
# the name once again can be whichever we would like to help us understand what is happening later on

     azure_rm_resourcegroup:
     # this task above is the Azure Resource Manager and can be used to help manage your azure infrastructure

         resource_group: aztestsynnex
     # this will be the name of the test resource group we are going to create
         location: east US
     
         state: present
     # we can use another flag as present to create and is idempotent and will not be able to be ran if another is present or we can run absent to remove the azure Resource Group altogether. 
        
```         
Below is an Example of a Ansible playbook built to Deploy your Azure template. az500mod2lab2

please create a file az500mod2.yml and include the following text. 

I have also already completed them within this repo for you. 

 ``` 
- name: setup system

  hosts: localhost

  tasks:

   - name: azure create

     azure_rm_deployment:

         resource_group: AZ500mod2lab2

         location: east US

         state: present

         name: az500mod2lab2

         template_link: 'https://raw.githubusercontent.com/MicrosoftLearning/AZ-500-Azure-Security/master/Allfiles/Labs/Mod2_Lab02/template.json'

```
         

The Second File Below is AZ Security Baseline template within an ansible plays and includes the ability to pass parameters.

I have completed this for you above or you can create a template named azbaseline.yml. Also you can change the paramaters and you will need your user object id which is empty below. 


<div class="yaml"> 

```

- name: Ansible prereqs 

  hosts: localhost

  tasks:

   - name: azure create 
#Azure Resource Manager Deployment
     azure_rm_deployment:

         resource_group: resourcetempl

         location: east US

         state: present

         name: resourcetempl

         template_link: 'https://raw.githubusercontent.com/microsoft/MCW-Security-baseline-on-Azure/master/Hands-on%20lab/AzureTemplate/template.json'

         parameters:

              adminUsername:

                      value: wsadmin

             adminPassword:

                      value: p@ssword1rocks

             databaseName:

                      value: microsoftbaselinesecurity

             userObjectId:

                     value: 

             vmSize:

                     value: Standard_E2s_v3

             sqlservername:

                     value: synnexdbtest1     

```
</div>

We can also deploy multiple templates. I have created a playbook template x2 two files deploy.yml and the vars.yml file to 

be modified as to fit your template need. feel free to modify as needed.

Deploy.yml

```
---
- name: setup all labs

  hosts: localhost

  vars_files:
    - vars.yml

  tasks:

   - name: azure create

     azure_rm_deployment:

         resource_group: "{{item.value.labname}}"

         location: east US

         state: present

         name: "{{item.value.labname}}"

         template_link: "{{item.value.name}}"

     with_dict: "{{labs}}"
     
```  

vars.yml file
(This File includes all of the variables to pass to the Deploy.yml above.)
```
---
labs:
  mod2lab2:
    name: https://raw.githubusercontent.com/MicrosoftLearning/AZ-500-Azure-Security/master/Allfiles/Labs/Mod2_Lab02/template.json
    labname: az500module2lab2
  mod2lab1:
    name: https://raw.githubusercontent.com/MicrosoftLearning/AZ-500-Azure-Security/master/Allfiles/Labs/Mod2_Lab01/template.json
    labname: az500module2lab1
  mod2lab11:
    name: https://raw.githubusercontent.com/MicrosoftLearning/AZ-500-Azure-Security/master/Allfiles/Labs/Mod2_Lab11/template.json
    labname: Test-FW-RG

```

The next set of inscrutions are located here for the AZ Security Baseline. 


https://github.com/microsoft/MCW-Security-baseline-on-Azure/blob/master/Hands-on%20lab/Before%20the%20HOL%20-%20Security%20baseline%20on%20Azure.md#task-1-deploy-resources-to-azure
