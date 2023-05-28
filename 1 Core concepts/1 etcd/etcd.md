# what is kubernates

Kubernetes, also known as K8s, is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It was originally developed by Google, and is now maintained by the Cloud Native Computing Foundation (CNCF).

# kubernates architecture and use request flow

Kubernetes has a client-server architecture, with a set of nodes that run applications and a control plane that manages the cluster.

The control plane consists of several components, including:

API Server: The API server is the front-end for the Kubernetes control plane. It exposes the Kubernetes API, which applications and users can use to interact with the cluster.

etcd: Etcd is the primary data store for the Kubernetes cluster. It stores configuration and state information about the cluster, including information about nodes, pods, services, and other resources.

Scheduler: The scheduler is responsible for scheduling pods onto nodes in the cluster, based on resource availability and other constraints.

Controller Manager: The controller manager is responsible for managing controllers that control various aspects of the cluster, such as scaling, rolling updates, and self-healing.

Each node in the cluster runs a set of Kubernetes components, including:

Kubelet: The Kubelet is the primary agent that runs on each node. It is responsible for managing the lifecycle of pods on the node, including starting, stopping, and monitoring containers.

Kube-proxy: The Kube-proxy is responsible for managing network communications between different pods in the cluster.

When an application or user sends a request to the Kubernetes API server, the request is validated and processed. The API server then updates the state of the cluster in etcd, and sends a message to the relevant components in the cluster to take action. For example, if a user requests to scale up a deployment, the API server updates the deployment object in etcd, and sends a message to the scheduler to schedule additional pods.

The scheduler then selects a node to schedule the new pods, based on resource availability and other constraints. The Kubelet on the selected node starts the new pods, and the Kube-proxy manages network communications between the new pods and other pods in the cluster.


# Etcd 

ETCD is a distributed reliable key-value store that is simple, secure and fast... that is used for storing configuration and state information in distributed systems.

When a user or application sends an API request to the Kubernetes API server, the request is first validated, then processed, and the result is stored in etcd. Etcd then notifies the relevant components in the cluster of the change, ensuring that the cluster's state is kept up to date.

Etcd data store stores information regarding the cluster such as

- NODEs
- Pods
- Configs
- Secrets
- Accounts 
- Role 
- Bindings 
- others

Etcd ko **kubeadm** k through b ker sakhty hn... but manual cluster creation k time per apko master node ma etcd ki libery ko add etcd ko as a service use keerny k lye master node ma... see screenshot...

High availability ma we have multiple master nodes...

# kubernates architecture



# kub controller manager

node controller: it checks the status of the node every 5min. it check the heartbit of the node. agr heartbit receive ni hoti tu isko wo unreachable state ma dal dye ga. but 40sec thk wait kery ga phir unreachable state ma dal dye ga. unreachable stat ma jaty hi isko 5m up hony ma lgye gye.. see screen shot

Relication controller: it is responsible to check the status of relicas said.. or insure kerta ha k desire no of pod availabe ho all sets ma... if a pod dies it creats another one..  see screen shot

their are any controller available in kube controller to handle the process... see screen shot

y sab controller package kub controller manager k under hoty hn. jb ap kub controller manager ko install kerty hn tb y package is ma ajty hn..

see screenshot that how to install kube controller manager.....

# kub schedular

it is responsible for scdeduling pod on nodes... remember y sirf decide kerta ha actual ma y khud y kam ni ker rha hota.. kubelet is the right one who create the POd(mean creating the pod on node). the schedular only decides which pod goes where... is k lye schedular hr node k resources ko dekhy ga, jo resource POD ki requirement(like cpu , memory) k according fit hoga wo us node ma jyega.

# kubelet

kubelet , kube schedular ki instruction k according pod ko nodes per create kerta ha.. remove kerta ha or iski report wo master node ma api server k through kube schedular ko dye rha hota ha. tky wo etcd data base ma store hojeyg..

# kube proxy 

Kube-proxy is a network proxy that runs on each worker node in a Kubernetes cluster. Its primary responsibility is to manage network communications between different pods in the cluster.

Kube-proxy provides a few important services:

Load balancing: Kube-proxy can route traffic to multiple instances of a pod, distributing the workload evenly.

Service discovery: Kube-proxy maintains a list of available services and their corresponding IP addresses, making it easy for pods to find and communicate with each other.

Network address translation (NAT): Kube-proxy can translate a pod's IP address to a different IP address that is routable within the cluster. This can be useful when pods need to communicate with resources outside the cluster.

Kube-proxy is a crucial component of a Kubernetes clu

kube proxy is a proccess that runs on each nod in kubernates cluster. it job is to look new services and every time new services get created. it creates the new the appropriate role to each node to forward the traffic to those services to the backend pod... 

it is responsible to provide the network to the pod.

aik cluster ma her pod dosry pod k sath communication ker sakhta ha... because of deploying POD network, pods inside the nodes are able to communicate with each other...


apko kublet ko worker nodes per manually install kerna pary ga..


# Creating a pod using a yaml base configuration file...

**POD with yaml**

we will learn how to write yaml file specfically for kubernates..

kubernates defination file

pod-defination.yml
    
    api-version: this a version of kubernates you are using to create the object.. For pod and service the version would be **V1**. and for relicaset and deployment version would be **app/v1**. see screenshot
    kind:   it refers the type of the project that we want to create... like here we want to create pod so the type would be **POD**. seescreenshoot
    metadata: metadata is a data about the object... like name ,label.. see screenshot(is ma bta rha ha k name aik string value ha is lye wo samny aye gi.. but label aik dictionary ha is lye wo indented hokr aye gi... remember metadata ma ap name , label or kubenates ki properties bta sakhty hn is k alwa kuch ni... but label ma ap key value pair ki tarha content likh sakhty hn) 
    spec:   yha pa object sa related additional information likh sakhty hn...

    spec is dictionary and container property inside the spec would be  list/array that way we could say that one pod would have multiple containers.. yha **-** means k y first item ha. agr again y sign use kery gye tu mean k y 2nd item hogi.... see screenshot


file create kerny k bd ap execution k lye y command use kerni pary gi...

    kubectl create -f pod-defination.yml

    here pod-defination.yml is file name

command to see running pod and its details..

    kubectl get pods

    kubectl describe pod "pod name"

practical: of creating pod

vim pod.yml

    api-version: v1
    kind: Pod    yha *P* capital rakhna ha.. y case sensitive ha..
    metadata:    it would be dictionary. yha ap object sa related information likh sakhty hn...like name and label 
        name: nginx
        label: 
            app:ngnix
            tair: frontend

    spec:
        containers:
        - name: ngnix
          image: ngnix     y image dockerhub sa get ker rha hoga... agr kisi or registry sa get kerna ha is na tu iska complete address dena hoga yha...
        - name: apacheserver
          image: apache    

          hum na container k under 2 images k kha ha. its mean hum pod ma 2 containers create kerna chahty hn... after that save the file and run the file by using below command
          
          kubectl create -f pod.yml(command to execute the yml file) you can also use **apply** instead or create both works same..

          see screenshot...

Now use these commands to get information abour pod

    kubectl get pods

    kubectl describe pod "pod name"

next we will learn some tips and tricks for deploying yaml files easily...using IDE...

command to create nginx containers inside the pod..

    kubectl run nginx --image nginx   

command to delete pod

    kubectl delete pod webapp
# solution section used command

get pods detail with wide output

    kubectl get pods -o wide

command to create pod and run redis container and dry run output on yaml 

    kubectl run redis --image=redis123 --dry-run=client -o yaml

see screenshots 

command to create pod and run redis container and dry run output on yaml and put that output in redies yaml file..

    kubectl run redis --image=redis123 --dry-run=client -o yaml > redies.yaml

read yml file

    cat redies.yaml

execute yaml file

    kubectl create -f redies.yaml 

    or

    kubectl apply -f redies.yaml


# ReplicaSets

    this is kubernates replication controller. they are the processes that monitor object and response accordingly...

    basically hota y ha k hmri application node ma majood pod or pod ma majood container ma hoti ha.. jis ko sab users access ker rhy hoty hn... agr hmri application crush ker jye tu user apni access lose ker dety hn... 

    1- so replication controller help us to run multiples instances of single pod on a kubernate cluster... jis sa hota y ha k agr aik pod down hojye tu us jesy or create hojaty hn... or user ki access lose ni hoti... this provide **HIGH AVAILABILITY**

    AGr aik b pod node ma apna run ker k replication controller lgya howa ha tu jesy hi pod down hogi tu us jesi or pods create hojye gi...

    2- load balancing & scaling

    2nd reason is k traffic k load jesy hi increase hota ha... tu wo traffic k load ko balance kerny k lye... instance ko run kerta ha of a single pod k(mean us jesy or pod create kerta ha)... 
    
    replication controller help us to run multiples instances of single pod on a kubernate cluster..so jb hum cluster ki bt ker rhy hoty hn tu... it mean agr kisi node ki resources limited hn tu wo ksis or node ma pod k instances ko run kery ga resource k according balance load dalny k lye... see screenshots..

remember **relication controller or relicasets** dono k purpose same hn but dono aik jesy ni hn kuch differences b hn....  

relication controller is older and replace by relicassets... difference dono ma y ha k hum replications controller ma **selector property** ko use ni ker rhy hoty(use uska feasture ni ha yha) ... but replicassets ma hum **selector** ko use ker rhy hoty hn or is property ma hum un pods k label define kerty hn jin ko hum monitor kerwana chahty hn...(because kafi pods run horhy hoty hn tu is way sa hmry define kerda selected pods ki monitoring easy hojati ha.. k replicsset monitor kery k y pod down hogi ha tu is jesy or pod ko create ker dye...)

we already know that k hum pods ko yaml file k through b create ker sakhty hn or relication controller or relicassets ko b yaml file k through create ker skahty hn... 

hum pod ko yaml file k through create kery gye or use per relication controller ko set kerny k lye b yaml file create kergye. jis ma basically hum templete ma apny already created pod ko hi define kery gye tky at the time of pod replicas creation is jye pod hi create ho.. or yha per replicas b btye gye...

# pod.yaml

apiVersion: V1
kind: Pod
metadata:
    name: nginx
    label:
        app: nginx
        type: frontend

spec:
    containers:
    - name: nginx_app
      image: nginx
    
# rc-defination.yaml

apiVersion: V1 (replication controller k lye b version V1 hota ha)
kind: ReplicationController
metadata:
    name: myapp-rc
    label:
        app: myapp
        type: front-end

spec:
    template:
        metadata:
            name: nginx
            label:
                app: nginx
                type: frontend

        spec:
            containers:
            - name: nginx_app
              image: nginx
    replicas:3

execution command:

    kubectl create -f rc-defination.yml

    kubectl get replicationcontroller

    kubectl get pods

# replicasset
replicaset-defination.yml
apiVersion: app/v1 (replicaset k lye b version apps/v1 hota ha)
kind: ReplicaSet
metadata:
    name: myapp-
    label:
        app: myapp
        type: front-end

spec:
    template:
        metadata:
            name: nginx
            label:
                app: nginx
                type: frontend

        spec:
            containers:
            - name: nginx_app
              image: nginx
    replicas:3
    selector:   (it helps to find what pod under it. for this we would define pods labels here..)
        matchlabels:
            type: front-end

execution command:

    kubectl create -f replicasets-defination.yml

    kubectl get replicasets

    kubectl get pods

# scaling

replicase ki scaling kerny k lye hum template na replicas increase ker k command ko execute kery gye..

    kubectl replace -f replicaset-defination.yml

Delete the created ReplicaSets 

    kubectl delete rs replicaset-2

# command(important)

Create an NGINX Pod

    kubectl run nginx --image=nginx

Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)

    kubectl run nginx --image=nginx --dry-run=client -o yaml

Create a deployment

    kubectl create deployment --image=nginx nginx

Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run)

    kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) and save it to a file.

    kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

Make necessary changes to the file (for example, adding more replicas) and then create the deployment.

    kubectl create -f nginx-deployment.yaml

OR

In k8s version 1.19+, we can specify the –replicas option to create a deployment with 4 replicas.

kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml


# Deployments

**In Kubernetes, deployment is used to manage the deployment and scaling of containerized applications.** A deployment is a Kubernetes object that defines the desired state of a set of replicas of a particular application or service.

**The role of deployment in Kubernetes is to ensure that the desired number of replicas of a containerized application or service is running at all times. Deployment enables the **rolling updates and rollbacks of the application**, which helps in maintaining the application's availability while the update or rollback is in progress.**

Here are some of the key roles that deployments play in Kubernetes:

Creation of ReplicaSets: Deployments create and manage ReplicaSets, which are responsible for maintaining a specified number of pod replicas.

Rolling updates: Deployments support rolling updates, which allow you to update your application without any downtime by gradually replacing old pods with new ones.

Rollback: If there is an issue with the new version of the application, Kubernetes provides the ability to roll back to the previous version by simply reverting to the previous ReplicaSet.

Scaling: Deployments provide the ability to scale the number of replicas of a pod up or down to meet the changing demands of your application.

Overall, deployments are a critical component of managing containerized applications in Kubernetes, providing automated management of replicas and enabling zero-downtime updates and rollbacks.

(important) As we know that replication controller , replicasets , deployments are pod controller...**3ndo ki reponsibility same hi thi is to ensure that the desired number of replicas of a containerized application or service is running at all times** but 3ndo ma difference ha..

**Major difference b/w replication controller , replicaset , deployment**

- Replication controller **selector** k through sirf **same lables** waly pod ko hi moniter kerta tha... **jo iska drawback tha**. mean no of different selector ko monitor ni ker sakhta tha. but relication cotroller ma rolling update ki functionality hn.. mean application k new version ko update kerny k lye wo new replication controller create kerta tha or gradually replace kerta tha older pod to the new pod(remember replacing k time hi wo new version ko pod ma majood container ma update ker rha hota tha..) us k bd service older replication controller sa hat ker new replication controller per ajati thi. jis ki waja sa user ko kuch time k lye downtime ata tha jo k **drawback tha** or wo previous replication controller ko delete b ker deta ha... 

- is lye iska advance version replicaset aya. **y selector k through different label waly pod ko jo ap selector ma define kery gye,** usko b monitor ker rha hota ha. mean no of selector ko monitor ker sakhta tha. but relication cotroller ma rolling update ki functionality hn.. 

- so is promblem ko resolve kerny k lye replicaset hi k upper deployment ko add ker dya gya ha jis sa humy rollout(rolling updates and rollback) ki b feasility mil gi ha... mean application k new version ko update kerny k lye wo new replicaset create kerta tha or gradually replace kerta tha older pod to the new pod(remember replacing k time hi wo new version ko pod ma majood container ma update ker rha hota tha..) us k bd service older replicasets sa hat ker new replicasets per ajati thi. is br user ko downtime face ni hoga because service ab deployment k sath direct connected ha.. or deployment replicasets k sath... or rolling update k time new version ma koi issue ata ha tu wo wo isko older version per roll back b ker sakta ha... because older replicaset is case ma delete ni hota..

All of these capabilities are available with the kubernates deployment..



**what does rollout mean in kubernates-deployment**

In Kubernetes, **a rollout is the process of updating a deployment to a new version of an application or rolling back to a previous version**. Rollout enables the deployment to be updated or rolled back with minimal disruption to the application's availability.

During a rollout, Kubernetes updates the deployment's ReplicaSet to manage the deployment's new desired state, which includes the number of replicas and the updated container image. Kubernetes ensures that the new ReplicaSet is ready to handle traffic before it gradually replaces the old ReplicaSet's pods with the new ones.

There are two types of rollouts in Kubernetes: rolling updates and rollbacks.

Rolling updates: This type of rollout gradually replaces old pods with new ones. Kubernetes updates the deployment one pod at a time, ensuring that there is always a specified minimum number of available replicas during the update process.

Rollbacks: In case of a problem with the new version of the application, Kubernetes provides the ability to roll back to the previous version by simply reverting to the previous ReplicaSet. Kubernetes ensures that the deployment is rolled back to the previous version without any downtime.

Overall, rollout in Kubernetes deployment is an essential process to update or revert an application to a previous version with minimal disruption to the application's availability.

LAB:

vim deployment.yaml

    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: nginx-deployment
    labels:
        app: nginx
    spec:
    replicas: 3
    selector:
        matchLabels:
        app: nginx
    template:
        metadata:
        labels:
            app: nginx
        spec:
        containers:
        - name: nginx
            image: nginx:1.14.2
            ports:
            - containerPort: 80

command use to execute and apply changes
    
    kubectl apply -f filename
     
     or 

    kubectl apply -f filename

get details of deployment , replicasets and pods

    kubectl get deployment,rs,pod

describe for more details...

    kubectl describe deployment

**pods ko scale up and down kerny k lye file ma replicas ko jesy jesy hum increase ker k apply command k through file ko execute kery gye tu pod scale up and down hogye...**
    

get all details with one command.

    kubectl get all




