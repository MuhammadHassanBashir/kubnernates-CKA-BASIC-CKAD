# Kubernetes Networking

Kubernates ma docker ki tarha ip container ko ni milta **PODs** ko milta ha. Y ip PODs ko kha sa milta ha... basically jb kubernates initailly configure hota ha tu y internal private network create kerta ha. jis ma network range 10.244.0.0 hoti ha. Sab pod is k sath attach hoty hn or inhy is private network sa ip milta ha..

when we deploy multiple pods they all get saperate ip address from this network. aik node ma pods internal communication k lye in ips ko use kerti hn.. but other nodes ma other pods k sath internal ips k through communication kerna sahi ni ha.. because agr node ma pod kisi waja sa crush hojye tu communication stop hojye gi.. is lye hum 2 nodes k b/w external communication k lye service ko use kerty hn.   

aik node ma pods sa data service tk or service sa data other node ki service tk or waha pods tk jata ha. is tarha sa communication stop ni hoti...


**problem**

let suppose apky ps do nodes hn. jis ma pods na aaik dosary sa communication kerti ha... ap dono nodes ma kubernetes install kerty hn kubernetes dono nodes ma private internal network create kery ga. or is network k sath jo pods attach hogi y network isko ip dye ga. but dono nodes ma pods ko same ip milny ki waja sa cluster ma ip conflict ajye ga... this will not work in cluster see screen shots

jb kubernates cluster setup hota ha tu kubernates does not automatically setup any kind of networking to handle this kind of issue... is masly ko dekhy howy kubernetes hum sa except kerta ha k hum set up kery to handle network fundamental requirements k lye... kubernetas hum sa except kerta ha k hum mention below wala criteria setup kery.

- mean all container/pods can communicate to one another without NAT.
- All nodes can communicate with all containers and vice-versa without nat. **

phily sa hi kuch pre build solution available hn on different plateform per... see screenshots.. for example agr apna kubernetes cluster ko apny system per setup kya ha tu ap is masly k hal k lye in ma sa koi aik platfrom use kery gye..

- agr vmware ma deploy kerty hn tu NXT is a good option

is sa hoga kya k wo nodes ma private network ko hamesha same 10.244.0.0 wala ip pool ni dye ga. bilky change ker k dye ga. or wo network agye pods ko is k according ips dye ga.... see screenshot.. 

is sa simple routing technique sa 2 nodes m pods aik dosary sa communication ker sakhty hn...