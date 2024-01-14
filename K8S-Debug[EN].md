## Namespace that's stuck in the "terminating status":

1. Get all k8s resources that are stuck in the "terminating" stage in the Namespace and delete them.

Next, run the following commands:

```
kubectl get namespace NAMESPACE_NAME -o json > file.json
```
```
kubectl replace --raw "/api/v1/namespaces/NAMESPACE_NAME/finalize" -f ./file.json
```
After that, you should see that the Namespace can now be successfully deleted without sitting in the "Terminating" stage


## Get pod Events:
```
kubectl describe pod <pod-name> -n <namespace> | grep -A5 "Events:
```

## 5 common k8s failures and how to fix them

𝟭) 𝗜𝗺𝗮𝗴𝗲-𝗽𝘂𝗹𝗹 𝗯𝗮𝗰𝗸 𝗼𝗳𝗳 ~ Check for 𝙄𝙢𝙖𝙜𝙚 𝙥𝙪𝙡𝙡 𝙥𝙤𝙡𝙞𝙘𝙮 , 𝙥𝙚𝙧𝙢𝙞𝙨𝙨𝙞𝙤𝙣 𝙩𝙤 𝙥𝙪𝙡𝙡 𝙛𝙧𝙤𝙢 𝙧𝙚𝙥𝙤𝙨𝙞𝙩𝙤𝙧𝙮,𝙘𝙤𝙧𝙧𝙚𝙘𝙩 𝙞𝙢𝙖𝙜𝙚 𝙣𝙖𝙢𝙚 𝙖𝙡𝙤𝙣𝙜 𝙬𝙞𝙩𝙝 𝙩𝙖𝙜.

𝙐𝙨𝙚𝙛𝙪𝙡 𝙘𝙤𝙢𝙢𝙖𝙣𝙙𝙨 
```
 Kubectl describe po <podname>
 ```
 ```
 Kubectl get po <podname>
 ```
 ```
 Kubectl apply -f <deployment file name>
 ```


2) 𝘾𝙧𝙖𝙨𝙝-𝙇𝙤𝙤𝙥 𝙗𝙖𝙘𝙠 𝙤𝙛𝙛~ Check for 𝘾𝙤𝙧𝙧𝙚𝙘𝙩 𝙞𝙢𝙖𝙜𝙚 𝙣𝙖𝙢𝙚 𝙖𝙡𝙤𝙣𝙜 𝙬𝙞𝙩𝙝 𝙩𝙖𝙜 , 𝙚𝙣𝙤𝙪𝙜𝙝 𝙧𝙚𝙨𝙤𝙪𝙧𝙘𝙚 𝙘𝙤𝙣𝙨𝙩𝙧𝙖𝙞𝙣𝙩𝙨,𝙢𝙞𝙨𝙘𝙤𝙣𝙛𝙞𝙜𝙪𝙧𝙖𝙩𝙞𝙤𝙣 𝙤𝙛 𝙚𝙣𝙫𝙞𝙧𝙤𝙣𝙢𝙚𝙣𝙩 𝙫𝙖𝙧𝙞𝙖𝙗𝙡𝙚𝙨 , 𝙖𝙥𝙥𝙡𝙞𝙘𝙖𝙩𝙞𝙤𝙣 𝙛𝙖𝙞𝙡𝙪𝙧𝙚 𝙗𝙚𝙘𝙖𝙪𝙨𝙚 𝙤𝙛 ( 𝙛𝙖𝙞𝙡 𝙩𝙤 𝙗𝙪𝙞𝙡𝙙 𝙟𝙖𝙧 𝙛𝙞𝙡𝙚𝙨 , 𝙞𝙨𝙨𝙪𝙚𝙨 𝙬𝙝𝙞𝙡𝙚 𝙗𝙪𝙞𝙡𝙙𝙞𝙣𝙜 𝙙𝙤𝙘𝙠𝙚𝙧 𝙞𝙢𝙖𝙜𝙚.

𝙐𝙨𝙚𝙛𝙪𝙡 𝙘𝙤𝙢𝙢𝙖𝙣𝙙𝙨 
```
 Kubectl describe po <podname>
 ```
 ```
 Kubectl logs <podname>
 ```
 Also to check if enough resources are allocated (memory) 


3) 𝙁𝙖𝙞𝙡𝙪𝙧𝙚 𝙬𝙞𝙩𝙝 𝙀𝙭𝙞𝙩 𝙘𝙤𝙙𝙚 1~ Check for 𝘼𝙥𝙥𝙡𝙞𝙘𝙖𝙩𝙞𝙤𝙣 𝙘𝙤𝙙𝙚 𝙘𝙧𝙖𝙨𝙝𝙚𝙨 , 𝙞𝙣𝙘𝙤𝙧𝙧𝙚𝙘𝙩 𝙚𝙣𝙫𝙞𝙧𝙤𝙣𝙢𝙚𝙣𝙩 𝙫𝙖𝙧𝙞𝙖𝙗𝙡𝙚𝙨, 𝙞𝙣𝙨𝙪𝙛𝙛𝙞𝙘𝙞𝙚𝙣𝙩 𝙛𝙞𝙡𝙚 𝙥𝙚𝙧𝙢𝙞𝙨𝙨𝙞𝙤𝙣𝙨.


𝙐𝙨𝙚𝙛𝙪𝙡 𝙘𝙤𝙢𝙢𝙖𝙣𝙙𝙨 
```
 Kubectl logs <podname>
 ```
 Kubectl get po <podname>
 ```
 ```
 Kubectl apply -f <deployment file name>
 ```
Lookout for any exceptions in logs /missing variables at code level as well .


4) 𝙁𝙖𝙞𝙡𝙪𝙧𝙚 𝙬𝙞𝙩𝙝 𝙀𝙭𝙞𝙩 𝙘𝙤𝙙𝙚125~ Check for 𝙞𝙣𝙘𝙤𝙧𝙧𝙚𝙘𝙩 𝙛𝙞𝙡𝙚 𝙥𝙚𝙧𝙢𝙞𝙨𝙨𝙞𝙤𝙣𝙨 , 𝙚𝙭𝙘𝙚𝙥𝙩𝙞𝙤𝙣𝙨 𝙙𝙪𝙧𝙞𝙣𝙜 𝙗𝙤𝙤𝙩𝙞𝙣𝙜 𝙪𝙥 𝙤𝙛 𝙥𝙤𝙙

𝙐𝙨𝙚𝙛𝙪𝙡 𝙘𝙤𝙢𝙢𝙖𝙣𝙙𝙨  
```
 Kubectl logs <podname>
 ```
 ```
 Kubectl describe po <podname>
 ```

5) 𝙋𝙤𝙙/𝙉𝙤𝙙𝙚 𝙉𝙤𝙩 𝙍𝙚𝙖𝙙𝙮 ~ Check for 𝙉𝙚𝙩𝙬𝙤𝙧𝙠 𝘾𝙤𝙣𝙣𝙚𝙘𝙩𝙞𝙫𝙞𝙩𝙮 , 𝙚𝙣𝙤𝙪𝙜𝙝 𝙧𝙚𝙨𝙤𝙪𝙧𝙘𝙚 𝙖𝙡𝙡𝙤𝙘𝙖𝙩𝙞𝙤𝙣 ,𝙪𝙣𝙝𝙚𝙖𝙡𝙩𝙝𝙮 𝙥𝙧𝙤𝙘𝙚𝙨𝙨𝙚𝙨

𝙐𝙨𝙚𝙛𝙪𝙡 𝙘𝙤𝙢𝙢𝙖𝙣𝙙𝙨 
```
 Kubectl logs <podname>
 ```
 ```
 Kubectl get po <podname> and check for its state 
 ```
Increase system resource usage


