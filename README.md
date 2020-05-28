# AzureSecurityBaseline
Azure Security Baseline


We are going to Use Red Hat Software Ansible to help with the Security Baseline Deployment & AZ-500 Deployment. 

First open up and AzureCLI. 

and create a file deploy.yml and include the following text. I have also already completed them within this repo for you. 

First we are going to start with 

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
