# Lab

## API Consumption

### Connect Applications and APIs

* Audience: API Consumers, Developers, Architects

### Overview

APIs provide the building blocks for applications, but it is applications which deliver functionality to the end users. hence to see APIs in action it helps to see how applications can call APIs to provide new functionality. In this lab you'll be able to create a simple web application which consumes the API you built earlier ojn in the exercises.  

### Why Red Hat?

Applications can be built from many technologies. In this case we use a simple web application, but a wide range of Red Hat and non-Red Hat technologies could be used.


## Lab Instructions

### Step 1: Deploying International Inc Web Page

International Inc web development create a Node.js application for the company home page. They added a map service to locate the offices around the world. In this step you will deploy that application.

1. Open a browser window and navigate to:

    ```bash
    https://www.openshift.com
    ```
    
1. Log into OpenShift using your designated user and password. Click on **Sign In**.

    ![01-login](images/deploy-01.png "OpenShift Login")

1. You are now in OpenShift's main page. Enter to your project

    ![02-user-project](images/deploy-02.png "User Project")

1. From your main project page, click **Browse Catalog**.

    ![03-browse-catalog](images/deploy-03.png "Catalog")

1. Scroll down the page and search for the **Node.js** template. Click on the link.

    ![04-nodejs-template](images/consume-08.png "Template")

1. Click the **Next >** button.

    ![05-template-information](images/consume-09.png "Information")

1. Fill in the configuration information with your API implementation github repo details:

    * Version: **8**
    * Application Name: **web**
    * Git Repository URL: **https://github.com/YOUR_REPO/3scaleworkshop-ui**

1. Click **Create**.
  
1. Your service will be provisioned in a moment. Click the **Continue to the project overview** link.

1. From your overview page, click the white space next to the **web** link to expand the deployment information.

1. Scroll down and click in the **web** link in the *BUILDS* section.

    ![10-builds](images/deploy-10.png "Builds")

1. In the build configuration page, change to the **Environment** tab. Fill in the available row with the following information:

    * Name: **API\_BACKEND\_URL**
    * Value: **http://YOUR_API_URL_FROM_API_MANAGER**

    ![11-environment](images/deploy-11.png)

    _Click the **Add Value** link to enable a new row if not already present_.

1. Click **Save** button to persist the changes. A green pop up will show you that the changes were saved.

1. Click the **Start Build** button to trigger a new build using the new environment variables pointing to your service.

    ![12-start-build](images/deploy-12.png "Start Build")

1. Click the **Overview** menu option on the left side to go back to the your project overview page.

1. In the overview page, wait until the running *Build is complete* and the pod circle stays blue continously. This means the application was successfully deployed and now is ready to listen to requests.

    ![13-build-complete](images/deploy-13.png "Build Complete")

1. Click the **Routes** to open a new tab and connect to *International Inc* new website.

1. You should now see what the development team created for International Inc. Click **LOCATIONS** to check the locations page.

    ![10-application-page](images/consume-13.png "Webpage")

1. This pages uses the unsecured Location API service. It displays the different International Inc offices around the world.

    ![11-locations-page](images/consume-14.png "Locations Page")

1. In the next step we will update the Locations page to use the 3scale protected API.

## Steps Beyond

So, you want more? You can explore in detail the documentation on the Javascript Adapter to check what other things can you get from your authenticated user.

## Summary

In total you should now have been able to follow all the steps from designing and API, deploying it's code, issuing keys, connecting OpenID connect and calling it from an application. This gives you a brief overview of the creation and deployment of an API. There are many variations and extensions of these general principles to explore!

This is the last lab of this workshop.

## Notes and Further Reading

* [Red Hat 3scale API Management](http://microcks.github.io/)
* [Setup OIDC with 3scale](https://developers.redhat.com/blog/2017/11/21/setup-3scale-openid-connect-oidc-integration-rh-sso/)
