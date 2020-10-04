# K8sToHelm
A simple dobby deployment from with k8s yaml and same specifications with Helm

Use ```./run deploy``` to start the application in your local. Make sure you have cluster running either in your local or in any cloud.


## Dobby deployment specifications:
 1. Running on port 4444
 2. Passing the configuration INITIAL_DELAY=20 through configmap which sets the initial delay to start the server
 3. ReadinessProbe will check at at every 5 seconds with 2 seconds timeout but will start this checking after 10 seconds of starting the container.
 4. LivenessProbe will check at at every 10 seconds with 2 seconds timeout but will start this checking after 30 seconds of starting the container.
 5. Container is not running as root
 6. Request for 10m CPU and 50 Mi Memory. And limit is set to 20m CPU and 60Mi Memory
 7. Rolling update with maximum 1 pod down and 1 pod extra when it's in full capacity during rollout
 
 ### Problems:
 1. Configmap stores a lot of specifications which can control the deployment in it's way. But deployment will not consume any spec from configmap. it will only consume those which are service/image specifications. So it would create a problem if we want to create a configurable deployment for each environemnt.
 
 ### Solution Acceptence Criteria:
 1. We can consume deployment specifications from either configmap or from anywhere else. But it has to be passed when deployment is about to create.  
 _Example_:- CPU request and limits can change based on their environment. So it will consume from either from one of our configmap or else from any env value files
