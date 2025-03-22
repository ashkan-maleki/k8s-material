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


curl http://ent.dev.svc.cluster.local:8080
curl http://ent.prod.svc.cluster.local:8080


You should see the responses:

Development for the dev namespace.

Production for the prod namespace.