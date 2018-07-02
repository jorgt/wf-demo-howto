
# Workflow demo

Recently I demoed a small end-to-end proof of concept for SCP Workflow at UI5con 2018 in Walldorf, Germany. Since it seems to have been fairly well received and people have expressed interest in it, I decided to write a how-to guide on how to set up SAP Cloud Platform workflow and optionally deploy the demo apps that I have prepared to get you started. 

For the SAP spiel about workflow and pricing options, have a look at the [introduction page](https://cloudplatform.sap.com/dmp/capabilities/us/product/SAP-Cloud-Platform-Workflow/df696e5a-d973-4ecd-8d8d-532d60aa1921) here. 

### This document covers:
1. activating workflow on your trial account dashboard and WebIDE
1. allocating all workflow authorisation roles to your user
1. optionally, installing the demo applications consisting of
    1. an app you can deploy to the launchpad to start a workflow
    1. an inbox application for your approve and reject scenarios
    1. a small but complete workflow with service-, user- and script tasks
    1. the setup of a destination on your account if you want to showcase an API call I have prepared
1. How does everything fit together
    1. Starting a workflow
    1. Birds eye view of the workflow
    1. What does that service do
    1. Monitoring a workflow
1. Usefull resources

### 1. Activating workflow

##### On the dashboard
Workflow is provided as a service on your SCP Dashboard like everything else. Its prerequisites are the activation of the portal (launchpad) and the WebIDE so head over to the services link and check that all of these are enabled. 

First, make sure the portal is activated. If you haven't set it up fully yet, make sure to head into the configuration and set up a default site so you can deploy the started application, and to have a spot for the workflow monitoring apps. 

![portal service](img/1-services-portal.png?raw=true "Activate portal service")

Next, enable the WebIDE. Make sure to pick the full stack one, the 'normal' one will be depricated at some point.

![webide service](img/2-services-webide.png?raw=true "Activate webide service")

Once the other two are active, flip the switch on the workflow.
![workflow service](img/3-services-workflow.png?raw=true "Activate workflow service")

##### In the WebIDE

Once you're in the WebIDE, be sure to activate the workflow plugin. SCP workflow has a neat drag-and-drop style editor which will not be available until you do.

![workflow service](img/7-webide-activate.png?raw=true "Activate workflow plugin")

### 2. Workflow authorisations

Workflow comes with a fairly fine grained set of authorisations. For the purpose of your demos, I suggest you give your user everything in the `wfs` category. I haven't done much with authorisations so maybe there's an existing group. Whatever the case, I just went and added the whole lot. This will give you the access to create, launch and monitor all workflows. You'll notice after this is activated that you have three new apps on your launchpad:
- Inbox
- Workflow definitions
- Workflow monitoring

![workflow service](img/4-auth-workflow.png?raw=true "Activate workflow service")

## You're ready to create a workflow. 

That's the whole setup. If you're happy to go and have a play you can stop reading and have a dig. If you like to install my small demo to get you going, please read on. 

### 3. Install the demo applications

##### Clone these repositories

Go forth and clone the following repositories in your WebIDE (feel free to fork them before you clone them so you can save your changes back to Github):

- The [starter application](https://github.com/jorgt/wf-demo-app.git).
- The [inbox application](https://github.com/jorgt/wf-demo-inbox-screen)
- The [workflow](https://github.com/jorgt/wf-demo-workflow) itself. 

After cloning, deploy all apps to the cloud platform. For the starter application don't forget to deploy it and *add it to the launchpad*. The workflow is deployed like anything else, but the definition itself is deployed slightly differently:

[screen]

##### Create a destination

Using script tasks alone is a great way to build an MVP of your workflow. You're not dependent on anything and you can develop entirely within the confines of the WebIDE. However as a full stack demo this is kind of boring so I'm providing a stupidly simple service. You send it the workflow requestor details (that's you!) and it will return those details twice as approvers. More details below. 

In order to call it, create a destination on your dashboard that looks like this:


### Usefull resources

1. The complete API documentation for workflow can be found [here](https://api.sap.com/api/SAP_CP_Workflow). Handy for developers!
2. A more in-depth series of blog posts produced by DJ Adams, which starts [here](https://blogs.sap.com/2018/01/08/discovering-scp-workflow-the-monitor/). 
