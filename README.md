# Run to the bus 

In this lab you will create a Node-RED application that uses HSL (Helsingin seudun liikenne) API. The outcome is a visual representation of the bus line you select in the map of Helsinki. 
Once you have completed this lab you will never be late for the bus again! :smile:

  - [Need to know](#need-to-know)
  - [Create an IBM Cloud account](#create-an-ibm-cloud-account)
  - [Create your first Node-RED app](#create-your-first-node-red-app)
  - [Check HSL API](#check-hsl-api)
  - [Build your flow](#build-your-flow)
  - [Summary](#summary)
  

## Need to know

**IBM Cloud**: 

**Node-RED**: 

**HSL**:

<img src="/images/create-resource.png" width="100%" height="100%">

## Create an IBM Cloud account

1. Go to https://cloud.ibm.com/registration and click Create an IBM Cloud account.

2. Enter your IBMid email address. If you don't have an existing IBMid, an ID is created based on the email that you enter.

3. Complete the remaining fields with your information, and click Create account.

4. Confirm your account by clicking the link in the confirmation email that's sent to your provided email address.

## Create your first Node-RED app

### Find the Node-RED Starter in the IBM Cloud catalog

5. Log-in to IBM Cloud.
- https://cloud.ibm.com/login

6. Click the _**Create Resource**_ button at the top right. This action will take you to the 'Catalog'.

<img src="/images/create-resource.png" width="100%" height="100%">

7. Search for node-red and go to the Software tab. Then click on the node-red app box.

<img src="/images/node-red-catalog.png" width="100%" height="100%">

8. Click on the Create app button to continue.

<img src="/images/create-app.png" width="100%" height="100%">

### Configure your application

9. Now you need to configure the Node-RED Starter application.

On the App details page, a randomly generated name will be suggested – Node RED RANDOM_NAME. Either accept that default name or provide a unique name for your application. This will become part of the application URL. 
Note: If the name is not unique, you will see an error message and you must enter a different name before you can continue.

<img src="/images/name-app.png" width="100%" height="100%">

10. The Node-RED Starter application requires an instance of the Cloudant database service to store your application flow configuration. Select the region the service should be created in and what pricing plan it should use. 

<img src="/images/db-app.png" width="100%" height="100%">

Note: You can only have one Cloudant instance using the Lite plan. If you have already got an instance, you will be able to select it from the Pricing plan select box. You can have more than one Node-RED Starter application using the same Cloudant service instance.

11. Click the **Create** button to continue. This will create your application, but it is not yet deployed to IBM Cloud.

### Enable the Continuous Delivery feature

12. At this point, you have created the application and the resources it requires, but you have not deployed it anywhere to run. This step shows how to setup the Continuous Delivery feature that will deploy your application into the Cloud Foundry space of IBM Cloud.

On the next screen, click the Deploy your app button to enable the Continuous Delivery feature for your application.

<img src="/images/deploy-app.png" width="100%" height="100%">

13. You will need to create an IBM Cloud API key to allow the deployment process to access your resources. Click the **New** button to create the key. A message dialog will appear. Read what it says and then confirm and close the dialog.

The Node-RED Starter kit only supports deployment to the Cloud Foundry space of IBM Cloud. Select the region to deploy your application to. This should match the region you created your Cloudant instance in.

<img src="/images/configure-app.png" width="100%" height="100%">

Select the region to create the DevOps toolchain. Click Create. This will take you back to the application details page.

<img src="/images/configure-app2.png" width="100%" height="100%">

After a few moments, the Continuous Delivery section will refresh with the details of your newly created Toolchain. The Status field of the Delivery Pipeline will show In progress. That means your application is still being built and deployed.

<img src="/images/deploy-inprogress.png" width="100%" height="100%">

14. Click on the In progress link to see the full status of the Delivery Pipeline.

The Deploy stage will take a few minutes to complete. You can click on the View logs and history link to check its progress. 

<img src="/images/stage-running.png" width="100%" height="100%">

Eventually the Deploy stage will go green to show it has passed. This means your Node-RED Starter application is now running.

<img src="/images/stage-passed.png" width="100%" height="100%">

### Open and configure the Node-RED application

Now that you’ve deployed your Node-RED application, let’s open it up!

15. Click on the **View console** top open the application details page.

<img src="/images/stage-passed.png" width="100%" height="100%">

16. From the details page, click the Visit App URL link to access your Node-RED Starter application.

<img src="/images/visit-app.png" width="100%" height="100%">

17. The first time you open your Node-RED app, you’ll need to configure it and set up security. A new browser tab will open with the Node-RED start page. On the initial screen, click Next to continue.

<img src="/images/configure-nodered.png" width="100%" height="100%">

Secure your Node-RED editor by providing a username and password. Click Next to continue.

<img src="/images/configure-nodered2.png" width="100%" height="100%">

Note: If you need to change your username/password at any point, you can either edit the values in the Cloudant database, or override them using environment variables.(LINK)

18. The final screen summarizes the options you’ve made and highlights the environment variables you can use to change the options in the future. Click Finish to proceed.

<img src="/images/configure-nodered3.png" width="100%" height="100%">

<img src="/images/configure-nodered4.png" width="100%" height="100%">

Node-RED will save your changes and then load the main application. From here you can click the Go to your Node-RED flow editor button to open the editor.

<img src="/images/start-nodered.png" width="100%" height="100%">

You will need to login with the credentials you entered in the previous step and then the Node-RED editor opens showing the default flow.

<img src="/images/login-nodered.png" width="100%" height="100%">

<img src="/images/flow-nodered.png" width="100%" height="100%">

### Add extra nodes to your Node-RED palette

Node-RED provides the palette manager feature that allows you to install additional nodes directly from the browser-based editor. This is convenient for trying nodes out, but it can cause issues due to the limited memory of the default Node-RED starter application.

The recommended approach is to edit your application’s package.json file to include the additional node modules and then redeploy the application.

This step shows how to do that in order to add the node-red-dashboard module.

On your application’s details page, click the url in the Continuous Delivery box. This will take you to a git repository where you can edit the application source code from your browser.

Scroll down the list of files and click on package.json. This file lists the module dependencies of your application.

Click the Edit button

Add the following entry to the top of the dependencies section (1):

Note: Do not forget the comma (,) at the end of the line to separate it from the next entry.

Add a Commit message (2) and click Commit changes (3)

At this point, the Continuous Delivery pipeline will automatically run to build and deploy that change into your application. If you view the Delivery Pipeline you can watch its progress. The Build section shows you the last commit made (1) and the Deploy section shows the progress of redeploying the application (2).

Once the Deploy stage completes, your application will have restarted and now have the node-red-dashboard nodes preinstalled.

Congratulations! You have now created a Node-RED application that is hosted in the IBM Cloud. You have also learned how to edit the application source code and automatically deploy changes.


## Check HSL API
## Build your flow




## Summary

Awesome! 
