# Services

kubernetes services enable communication b/w verious component within and outside the application. kubernetes services helps us connect application together with other application and user..

for example service hi ha jo user ki request frontend pod k sath milti ha. or frontend pods ki request ko backend pods k sath milti ha. or backend pod ki request ko data base k sath..

Ther kubernetes service is an object, just like pods, relica set, or deployment that we worked with before. One of its use case is to listen to a port on the node and forward request on that port to a port on the pod running web application. This type of service is known as a **node port service.**

there are other service type available.

**Service Type**

- NodePort
- ClusterIP(the service creates a virtual IP inside the cluster to enable communication b/w different services, such as a set of front-end servers to a set of back-end servers.)
- Load balancer(where it provisions a load balancer for our application in supported cloud provider. A good example of that would be to distribute load across the different web servers in your front end tier.)

**Service- NODEPORT**

agr hum aws per node ma pods, or pod ma container, or container ma web application run ker rhy hn.. tu user application ko kesy access kery ga..

flow y ha k
-----------

user brower per IGW k public or external expose port ko hit kery ga... request IGW per public ip per aye gi... IGW k public ip node k private ip k sath map hota ha. is tarha sa user ki request node tk ajye gi. yha sa user ki request external expose port per aye gi. service external port per user ki request lister ker k internal port(target port) jis per pod run ker rha hota ha is per request ko move ker deta ha... is tarha sa pod ma container ma pari web application accessable hojati ha.. see screenshot.

let take a closer look. their are 3 port involve. 
1- the port on the pod where the actual web server is running is 80. it is referred to as the target port because that is where the service forwards the request to.
2- The second port is the port on the service itself, it is simply referred to as the port. Remember, these terms are from the viewpoint of the service

the service is in fact like a virtual server inside the node. Inside the cluster, it has its own ip address and that ip address is called the cluster Ip of the service.

3- finally, we have the port on the node itself, which we use to access the web server externally and that is known as the node port.

see screenshots.. 

is ma bta rhy hn k external nodeport 30008 ha. **this is because node ports can only be in a valid range, which by default is from 30000 to 32767.**


**How to create service**

Jis tarha sa hum yaml file k through pods,replicaset or deployment ko create kerty thy. same isi tarha hum yaml file k through service ko create kery gye..


apiVersion: v1
kind: Service
metadata:
    name: myapp-service
spec:
    type: NodePort(mean is tarha ki service type bn rhi ha)
    ports:
       - targetPort: 80(port on which pod service is running)   
         port: 80(service internal port)
         nodeport: 30008 (external port )


remember if you don't provide a target port, it is assumed to be the same as port, and if you don't provide a node port, a free port in the valid range b/w 
30000 and 32767 is automatically allocated.

yaml file ma hum na aik important cheez miss ker di ha.. hum na target port k tu bta dya ha jis per request jani ha.. 

we have simply specfied tha target port, but we didn't mention target port on which POD, there could be hundreds of other PODs with web services running on port 80.

so how we do that.. 

    jesa k hum na replicaset ma kya ha selector feature ma pods k labels bta dye thy. replicaset in labels waly pods ko hi mointor kerta tha.. same is technique ko use kerty howy hi hum is kam ko b kery gye.. 

 **we will use labels and selectors to link these together.** 

 we know that the pod was created with a label. we need to bring that label into the service-definaiton file.

 so for this we have new property called selector

 apiVersion: v1
kind: Service
metadata:
    name: myapp-service
spec:
    type: NodePort
    ports:
       - targetPort: 80  
         port: 80
         nodeport: 30008 
    selector:
        app: myapp
        type: front-end

selector ma wo labels aye gye jo apna pods ko create ekrty time dya tha... is tarha sa target port ko specfically pta chal jye ga k wo un pods k lye ha...

create service

    kubectl create -f service-defination.yaml

for listing the service

    kubectl get service

**This is for the single pod, so what do you do when you have multiple pod**

Single node ma multiple pods per request kesy jye gi... hum na jo service ki configuration ki ha is sa zayada or koi steps ni kerny hn.. jb node ma pods increase hojye gi. tu service ma define target port jis per pod run ker rhi hn or selector ma mentioned pods k labels in sa specfically un pods k pta chal jye ga service ko jis per is na user request ko forward kerna ha.. tu wo is trha sa in pod per load balancing kerty howy user ki request ko move kery gye..

**multiple pods on multiple nodes k case ma**

is case ma kubernetes automatically service object ko across the cluster expand ker dye ga... service configuration ma mention target port or selector ma pod labels sa service specfic pods ko cluster ma find ker lye ga or un per user ki request load balancing ker k send ker rha hoga... or node remove hony k case ma automatically service abject ko b existing nodes per shrink ker rha hoga... 





To summarize, in any case, whether it be a single pod on a single node, multiple pods on a single node, or multiple pods on multiple nodes, the service is created exactly the same without you having to do any additional steps during the service creation. when pods are removed or added, the service is automatically updated, making it highly flexible and adaptive. Once created you won,t typically have to make any additional configuration changes.