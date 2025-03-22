# Service Discovery


## How to Test the Example
Apply the YAML file:  

`kubectl apply -f example.yaml`

Verify that the Pods and Services are running:


`kubectl get pods -n dev`  
`kubectl get pods -n prod`  
`kubectl get svc -n dev`  
`kubectl get svc -n prod`

Access the jump Pod:

`kubectl exec -it jump -n dev -- bash`

From inside the jump Pod, use curl to call the HTTP API of the dev and prod Services:


`curl ent:8080`  
`curl http://10.101.71.140:8080` *Replace it with the ClusterIP of the service in **prod** namespaces*  
`curl http://ent.prod:8080` *If your cluster is configured to allow cross-namespace communication using short names*



You should see the responses in order:

Development  
Production  
Production


Inside the **jump** pod:  
`nslookup ent.prod.svc.cluster.local`

Output:  
Server:         10.96.0.10  
Address:        10.96.0.10:53  

Name:   ent.prod.svc.cluster.local  
Address: 10.101.71.140

Inside the **jump** pod:  
`cat /etc/resolv.conf`

Output:  
nameserver 10.96.0.10  
search dev.svc.cluster.local svc.cluster.local cluster.local localdomain  
options ndots:5