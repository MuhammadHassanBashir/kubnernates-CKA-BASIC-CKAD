# kubernates & k8s

kubernates ko understand kerny k lye humy **containers or orchestration** dono ko samjana hoga..

**Why do we need containers**

- application compatibility/dependency issue with os..
- long setup time
- different dev/test/prod enviroments...

with docker we can run each service(application) with its own labiraries and dependencies in separate containers..

**what are containers**
(interview)
Containers are a type of virtualization technology that allows you to package an application and all its dependencies into a self-contained unit, which can then be easily deployed and run on any system that supports containerization.

Containers offer several benefits over traditional virtualization technologies, such as:

- portablity
- efficiency
- scalability
- consistency

containers are completely asolated enviroments.. they have own processes or service and have own network interfaces and mount except they all share the same host operating system kernal.



remember containers docker ki traha new ni hn.. container almost 10year phily sa use horhy hn. containers ki different type 

- lxc linux container
- lxd  linux container deamon
- lxcfs

docker lxc container ko use kerta ha..        (docker , kubernates, rkt , lxc/lxd , window) in sab sa containers bn sakhty hn...
(interview)
**to understand how docker works let us revisit some basic concept of OS first(important)**

Agr ap dekhty hn debein , fedora , centos ,susi ko tu y sab do cheezo per base kerty hn..

- OS kernal 
- set of software

operating system os kernal is responsible to interact with the underline hardware...  os kernel sab ka same ha like **linux** but it is the software above it that make the operating system different.. software may consist of different user interface, drivers, complier , file manager ,developer tools. so you have common linux kernal share all operating system and some custom software that differentait OS with each other.. 

**What does mean containers sharing the same host os kernal.**

let suppose k hmry pas aik system ma ubuntu OS install ha... or us per docker k package install ha... now docker can run any flovor of OS on top it as long as they all base on the same **kernal**. In this case is linux... see screen shot . **if the under line OS is ubuntu then docker can run container based on other distribution like debein , fedora , centos...(because sab k base kernal linux ha).** each docker container only has the additional software that make this OS system different from other and docker utilizes the underlying kernel of docker host which works with all the operating systems above..


(interview)
2nd y k vm machines per ap koi b window or linux base operating system run ker sakhty hn. because is made for virtualization(jis ma ap aik hardware ki virtualization ker k different os chal sakhty hn)jis sa OS ki maintainer b bahr jati ha.. 

but docker apny upper un distribution ko containers ker k run ha jin k kernel host operating system k kernal sa milta ha.. like host operating system ubuntu ha iska kerna linux hota ha tu docker underline kernal k according linux base distrubition like fedora , debain , susi, centos ko apny upper run kery ga.. window base container ko run ni kery ga. because window k kernal different hota ha.. or y containers k drawback ni ha because container is not made to virtualize and run differnet OS and kernal on same hardware. the main perpose of docker is to containerized applications and to ship them and run them...

************Container orchestration**************



************Kubernetes Architecture**************


component of master node:

- api server
- etcd data base
- schedular
- controller

component of worker node:

- kubelet
- container runtime(docker , rkt , cro)

kubectl commands:

    kubectl run hello-mimikube

    kubectl cluster-info

    kubectl get nodes

