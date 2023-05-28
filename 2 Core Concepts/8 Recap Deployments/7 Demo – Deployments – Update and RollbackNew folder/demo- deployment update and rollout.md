is ma wo y bta rha ha k hmry pas deployment ki yaml file ha. jis ko hm create command ka through execute kerty hn tu. wo hmri deployment is ma replicas or is ma pods create kerta ha. 

    kubectl create -f filename

then rollout k status check kery gye tu hmy pods first time create hoty nazar aye gi , phir jb hm yaml file ma version update ker k rollout k status check kery gye tu wo hmy bta rha hoga k new pod with new version k sath new replicaset ma create ker rha ha or old pod ko down ker rha ha old replicaset.

    kubectl rollout status file name

history ki command hmy yaml file ma kitny revision hoi hn wo or changes bta rha hoga...

    kubectl rollout history file name.


- yaml file ko edit ker k new version edit command k through dal ker yaml file ma jab hum rollout k status check kry gye tu wo hmy bta rha hoga k new pod with new version k sath new replicaset ma create ker rha ha or old pod ko down ker rha ha old replicaset. or history ki command hmy revisions bta rhi hogi... **describe** k through ap jb command ko execute kery gye tu wo. **annotation** ma kya command apna use ki thi wo bta rha hoga. or event ma new pod create or old remove bta rha hoga.. or ap version update kerny k bd describe k through new updated image ko b dekha sakhty hn...

- ap image version update **set image** k through b file ma update ker skahty hn..

    kubectl set image deployment deployment-name containername= new-version 

ab wo khta ha k application k version update kerty time koi masla ajata ha tu ap rollout ko **undo** b ker sakhty hn... kubernetes isko pervious version per lye jye, because hmry old replicaset ma pervious version waly pods down state ma thy, jb ap previous version ki command ko execute kery gye tu wo old replicaset ma pods ko up ker dye ga... 

    kubectl rollout undo filename

    ap history ki command k through b dekh sakhty hn k revision ma previous version ajye ga or describe ma jakr b dekh sakhty hn.. k pervious version k image agi hogi...

--------------
ab wo aik scenrio y rakhta ha k let suppose k hmri image ma koi masla ha or wo image docker hub per exist ni kerti or wo hm galti sa yaml file ma edit ker k execute kerty hn tu... jb hum rollout status dekhy gy tu wo pods create kerny k kosish kery ga , **errorimagepull** k error dye rha hoga... mean image na milny ki waja sa wo new pods create ni kery ga or na old pods ko delete kery ga.. is sa client k application per access b lost ni hogi...

then hm rollout undo ki commands ko use ker k previous version per chaly jye ga.. or old replicaset wali sari pods chaly gi with pervious version k sath..

