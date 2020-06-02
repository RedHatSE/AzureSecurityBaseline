# AzureSecurityBaseline
Azure Security Baseline

Welcome to Our Demo of Ansible on Azure. 
    - What is Ansible
    - The basics of writing a playbook
    - How to use Azure Resource Manager 
    - Using Azure Resource Manager to handle templetes in Ansible. 

We are going to Use Red Hat Software Ansible to help with the Security Baseline Deployment & AZ-500 Deployment. 

Login to your Azure infrastructure & open up and AzureCLI. 
![image](images/azurecli.png)


and create a file .yml and include the following text. I have also already completed them within this repo for you. 

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
         

The Second File Below is AZ Security Baseline and includes the ability to pass parameters.


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

The next set of inscrutions are located here for the AZ Security Baseline. 


https://github.com/microsoft/MCW-Security-baseline-on-Azure/blob/master/Hands-on%20lab/Before%20the%20HOL%20-%20Security%20baseline%20on%20Azure.md#task-1-deploy-resources-to-azure
