# AzureSecurityBaseline
Azure Security Baseline


We are going to Use Red Hat Software Ansible to help with the Security Baseline Deployment. 

First open up and AzureCLI. 

and create a file deploy.yml  and include the following text

<p> 
---

- name: setup system

   hosts: localhost

   tasks:

     - name: azure create

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


</p>

The next set of inscrutions are located here. 


https://github.com/microsoft/MCW-Security-baseline-on-Azure/blob/master/Hands-on%20lab/Before%20the%20HOL%20-%20Security%20baseline%20on%20Azure.md#task-1-deploy-resources-to-azure
