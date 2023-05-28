# Deployment- update and Rollback

**Deployment strategy**

- Recreate     
- Rolling update

**Recreate**:

Is deployment strategy ma hota y ha. jb apna apni application ka new version update kerna hota ha tb sab pods aik sath delete hoti hn or phir new version k sath sab pod aik sath create hoti hn. but is sa client ki application k access at the time of new pods create k kuch time k lye loss ho jata ha...

**Rolling update**

Is deployment strategy ma hota y ha. jb apna apni application ka new version update kerna hota ha tu gradually(one by one ker k) old pod new pods ma with new application version k sath create or update horhi hoti hn... jis sa client ki application tk access loss ni hoti...

**agr ap application update kerty time deployment strategy ni btaty tu wo by default rolling update strategy ko lye ga...** in other words rolling back is the default deployment strategy..

jb hum update ker rhy hn tu its could be different thing such as updating application verision, by updating the docker containers version used. updating labels, updating no of replicas..

file ma changes kerny k bd us changes ko hum below command sa execute ker sakhty hn..d

    kubectl apply -f filename...

    or yaml file ma image update is command sa b hoti ha..

    kubectl set image deployment/filename \nginx=new version

ap recreate or update rolling dono ko kubctl describe command k through dekhy gye tu apko pta chaly ga, k recreate ma event session ma wo sab pods ko phily delete kerny k khy ga phir recreate kery ga. 

but rolling update ma wo event session ma dekhy ga. tu wo kha rha hoga k  it gradually(one by one) create new pods and down old pods in old replicaset..(). see screenshot..

**Upgrade**

is ma wo bta rha hota ha k jb new application version pods ma update kerni hoti hn tb phily wo new replicaset ko deployment ma create kera ha phir us ma it gradually(one by one) create new pods with new application version in new replicaset and down old pods in old replicaset..()

Command

    kubectl get replicaset 
     
    use kery gye tu wo apko btye ga k old pod zero hogye hn or new pods create hogye hn.. see screenshot..


**Rollback**

because deployment ma replicas controller ki tarha older replicaset delete ni hota. is lye agr application version upgradation k time agr koi masla ajye tu ap rollout(rollback) use ker k older version per wapis b ja sakhty hn.. kubernets allow you tu rollback to a pervious revision.

changes ko undo kerny k lye below command ko use kery...

    kubectl rollout undo deployment/filename

    deployment old replicas set ki pods ko on ker dye ga or new replicas set k pods ko down ker dye ga.. and your application is back to older format

    
    kubectl get replicaset 

    is command k through b dekhty gye tu 1st replicas set apko sab pods k sath on mily ga or new replicaset sab pods k sath down mily ga..



