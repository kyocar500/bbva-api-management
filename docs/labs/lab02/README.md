# Lab

## API Deployment

### Deploying APIs to OpenShift

* Audience: Developers, Architects, System Administrators, Operators

## Overview

The code which implements any of the APIs in your organization is part of it's software infrastructure. This code needs to be well managed since it may need to scale to handle high volume, deployed in multiple locations and updated smoothly. In this lab you will learn how to deploy API backend code on the OpenShift container management platform which provides state of the art tools for managing deployed code.

### Why Red Hat?

Red Hat OpenShift is one of the leading container management platforms available in the market. It is based on the highly popular Kubernetes Open Source project which Red Hat is a leading contributor to. 

## Lab Instructions

### Step 1: Deploying Fuse-based APIs

1. Open a browser window and navigate to:

    ```bash
    www.openshift.com
    ```

1. Create a free account

1. Log into OpenShift using your designated [user and password](#environment). Click on **Sign In**.

    ![01-login](images/deploy-01.png "OpenShift Login")

1. You are now in OpenShift's main page. Create a project

1. From your main project page, click **Add and then Import YAML**.

1. Paste the **Red Hat Fuse 7.0 Camel with Spring Boot** template.

1. Click the **Create >** button.

1. Fill in the configuration information with your API implementation github repo details:

    * Application Name: **location-service**
    * Git Repository URL: **https://github.com/YOUR_REPO/3scale-api-workshop**
    * Git Repository context: **/projects/location-service**
    * Git Reference: **master**
    
The command you must run is: 
**oc new-app --template=s2i-fuse70-spring-boot-camel -p APP_NAME=location-service -p GIT_REPO=https://github.com/YOUR_REPO/3scale-api-workshop -p CONTEXT_DIR=/projects/location-service -p GIT_REF=master**


1. Your service will be provisioned in a moment.

    ![08-template-results](images/deploy-08.png "Results")

### Step 2: Configure External Resources

Did you notice your deployment is failing? This is because your API requires information on the database host and port to connect. Let's fix this problem.

There are several ways to provision information of the environment to your OpenShift deployment. Most of the times you will use a combination of [Config Maps](https://docs.openshift.com/container-platform/latest/dev_guide/configmaps.html), [Environment Variables](https://docs.openshift.com/container-platform/latest/dev_guide/environment_variables.html) and, [Secrets](https://docs.openshift.com/container-platform/latest/dev_guide/secrets.html). 

In this lab we will use Environment Variables.

1. From your overview page, click the **location-service** link to access the deployment configuration.

    ![09-deployment-config](images/deploy-09.png)

1. In the deployment configuration page, change to the **Environment** tab. Here click the **Add Value** link *twice* to get two (2) new rows.

    ![10-environment](images/deploy-10.png)

1. Fill in with the following information regarding the location of the International Inc Database.

    * Name: **MYSQL\_SERVICE\_HOST**
    * Value: **mysql.international.svc**
    * Name: **MYSQL\_SERVICE\_PORT**
    * Value: **3306**

    ![11-environment-variables](images/deploy-11.png)

1. Click **Save** to update the configuration and redeploy the service.

1. Go back to the **Overview** page to monitor your updated deployment.

1. You should now see the blue circle in the *location-service* pod. 

    ![12-running-pod](images/deploy-12.png)

### Step 3: Test Location API Service

We now have a working Location API Service implementation listening for requests. We will use an online cURL tool to test it.

1. Open a browser window and navigate to:

    ```bash
    https://onlinecurl.com/
    ```

1. Enter the following URL: 

    ```bash
    http://location-service-userX.apps.GUID.openshiftworkshop.com/locations/1
    ```

    Remember to replace the GUID with your [environment](#environment) values and your user number. It should look like this:

1. Click the **START YOUR CURL** button.

    ![13-curl-service](images/deploy-13.png "cURL Service")

1. The page will load the response information from the service. You will be able to see the *RESPONSE HEADERS* and the actual *RESPONSE_BODY*.

    ![14-curl-response](images/deploy-14.png "cURL Response")

*Congratulations!* You successfully deployed your teams Location API Service implementations into OpenShift using Red Hat Fuse 7.0 Spring Boot template.

## Steps Beyond

Sometimes, something more complex could be making your deployment fail. You can take a deeper look in to the log by clicking the pod and changing to the *Logs* tab. From OpenShift you can also connect to the container through the provided *Terminal* tab.

## Summary

In this lab you were able to launch a new software service which implements and API and manage it using the OpenShift platform. Subsequently you were able to call the API to see if it was really deployed and accessible in the right place.  

You can now proceed to [Lab 3](../lab03/#lab-3)

## Notes and Further Reading

* [Getting Started with OpenShift Online](https://docs.openshift.com/online/getting_started/index.html)
* [OpenShift Interactive Portal](https://learn.openshift.com/)
* [Contract First API Design with Apicurio and Fuse/Camel](http://wei-meilin.blogspot.com/2018/07/fuse-contract-first-api-design-with.html)
* [Applying API Best Practices in Fuse](http://wei-meilin.blogspot.com/2017/01/red-hat-jboss-fuse-applying-api-best.html)
