# How to install, setup & get started using the Findability Platform Predict Plus operator on RedHat Marketplace

In this tutorial, we demonstrate how to install, setup and get started using the Findability Platform Predict Plus (FPPredict Plus) operator on RedHat Marketplace (RHM). The advantages of using RHM operators are per below.  

* `Software for any cloud` :- Enterprise software for container-based environments in public clouds and on-prem

* `Automated deployment` :- Fast, integrated experience with instant availability on Red Hat® OpenShift® clusters

* `Fully supported` :- Free, continuous support for products purchased through Red Hat Marketplace

## A brief about Findability Platform Predict Plus operator

This operator is helpful to solve some of the usecases under AI using different methods like Regression, Classification, Timeseries etc. This operator will be applicable to developers, data scientists, architects who wants to solve different usecases under machine learning and AI. 


## Prerequisites

For all operators being installed from RHM, OpenShift cluster version 4.3 or higher is mandatory. Please set up Classic cluster using the instructions from below URL.

[Setting up OpenShift Cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started)

## Next Step - Access the RedHat OpenShift Container Platform (Web Console)

Follow the steps below to launch the cluster console which is also called RedHat OpenShift Container Platform.

Login to IBM Cloud Account and navigate to Dashboard

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/dashboard.png)

Click on Clusters and select the cluster which you have created under prerequisites. In our case, cluster name is cp-rhm-poc.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster.png)

After you launch the cluster, click on OpenShift web console on the top right hand side.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/web-console.png)

We can see the RedHat OpenShift Container Platform (Web Console). Click on question mark ikon on the top right hand side and select Command Line Tools. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cmd-line-tools.png)

Navigate to the section `oc - OpenShift Command Line Interface (CLI)` and download the respective oc binary onto your local system. This is needed to manage OpenShift projects from a terminal and is further extended to natively support OpenShift Container Platform features.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/oc-binary.png)

We are all set to proceed to next step which is to register the OpenShift cluster on RedHat Marketplace platform. This is mandatory to install any operators from RedHat Marketplace platform using the OpenShift cluster.

## Register the cluster on RedHat Marketplace

Sign up and login to RHM portal at [Link](https://marketplace.redhat.com/en-us) and click on workspace and then click on cluster. We need to add our new OpenShift cluster and register it on RHM platform.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/add-cluster.png)

Update the cluster name, generate the pull secret as per the instructions and save it. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster-details.png)

Copy the curl command which starts with `curl -sL https` and append the pull secret towards the end. The entire script should be handy to be used in next step.

We need to start the cluster first to register it. Open a command prompt and type oc login, update the username and password which are used for accessing the cluster and hit enter. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/start-cluster.png)

The cluster is up and running at this point. We need to run the entire script which is from previous step and hit enter. It will take a couple of mins and we can see that we have successfully registered the cluster on RHM portal.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/register-cluster.png)

## Create a project in web console

We need to create a project to be used and managed from command line. Click on Create Project and give a name as findability-project.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-project.png)

## Install the operator

Navigate to OpenShift web console which was launched during previous step. Select operatorhub under Operators and type FP in the search bar and hit 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/install-operator.png)

Click on Fp Predict Plus Operator (non custom) and hit install.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/select-install.png)

Create Operator Subscription by choosing All namespaces or specific namespace (select findability-project) and hit subscribe.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/subscribe.png)

After a couple of minutes, the operator gets installed on the cluster. We can verify by clicking on Installed Operators under ** Operators ** and see that the operator is successfully installed with status showing as Succeeded.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/installed-operator.png)

## Create storage for the operator

We need to create a persistent volume claim (storage) to handle datasets and bind it to the instance of this operator. Click on storage under Web Console and select Persistent Volume Claims.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/select-pvc.png)

The next step is to create persistent volume claim. We can select Storage Class from Gold, Silver, Bronze which was created in previous step, give the name as `fp-predict-plus-pvc`, select single user access & assign the storage size in GB. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-pvc.png)

After the PVC is created, it needs to be bound with the persistent volume (PV) which was created in earlier step. We should see the status as `Bound` per below.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/pvc-bound.png)

## Install the operand (Instance) of FPPredict Plus

Click on Installed operators under `Operators` and click on FP Predict Plus Operator to get the options like Overview, YAML, Subscription, Events, FP-Predict-Plus. Click on YAML and update the name under persistent volume with `useExisting as false`, persistent volume claims, routerCanonicalHostname and hit `Save`.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/yaml-changes.png)

