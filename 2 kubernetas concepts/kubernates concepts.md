# POD

A single pod can have multiple containers except for the fact that they are usually not multiple containers of the same kind.. 

if our intention was to scale our application, then we would need to create additional pods..

but sometimes you might hava a scenario where you have a **helper container** that might be doing some kind of supporting task for our web applicaition, like processing a user-entered data, processing a file uploaded by the user. or ap isko apny container k sath hi rakhna chahty hn , in that case, you can have both of these containers part of the same pod,

so that when a new application container is created, the helper is also created when it dies, the heloper also dies since they are a part of the same pod... 

the two container can also communicate with each other directly by referring to each other as localhost since they share the same network space. and plus they can easily share the same storage space as well.

multi-pod containers rare use case hoty hn..


**kubectl**

Command to create container and pod.

    kubectl run nginx --image nginx

    here nginx is the name of pod. and --image nginx is the image that pulled from docker hub and deploy in a container inside the pod..

    the command deploys a docker container by creating pod. it first create a pod automatically and deploy an instance of the nginx docker image,

command to get pod list..

    kubectl get pods

this is for more details

    kubectl get pods -o wide

command to check resource in more details

    kubectl describe pod nginx

    yha ma pod jis k name nginx ha ko detail ma check kerna cha rha ho..

for 
