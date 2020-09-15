Install
========
```
helm repo add itzg https://itzg.github.io/minecraft-server-charts/


cd helm
helm upgrade --install mc -f values.yaml itzg/minecraft
```

remember to create a firewall rule in gcloud
```
gcloud compute firewall-rules create minecraft-firewall-rule --allow=TCP:32028
```

Get IP
-------
```
$ helm get notes mc

NOTES:
Get the IP address of your Minecraft server by running these commands in the
same shell:
  export NODE_PORT=$(kubectl get --namespace default \
    -o jsonpath="{.spec.ports[0].nodePort}" services mc-minecraft)
  export NODE_IP=$(kubectl get nodes --namespace default \
    -o jsonpath="{.items[0].status.addresses[0].address}")
  echo "You'll need to expose this node through your security groups/firewall"
  echo "for it to be world-accessible."
  echo $NODE_IP:$NODE_PORT
```

note: the ip is the local node ip, not the external one, you can get the external one by doing:
```
$ k describe node | grep -i external
  ExternalIP:   <external ip here>
```
