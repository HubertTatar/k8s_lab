https://kubernetes.io/docs/reference/kubernetes-api/

- `k create deployment nginx --image=nginx --dry-run=client -o yaml`               - print sintacticaly correct template
- `k create deployment nxses --image=nginx --replicas=2 --dry-run=client -o yaml`  - print sintacticaly correct template
- `k run nginx --image=nginx --dry-run=client -o yaml`                             - print sintacticaly correct pod template
- `k api-resources` - list of resources
- `k explain deployment|pod|etc`       - explain given part of yaml
- `k explain flowschemas --api-version=flowcontrol.apiserver.k8s.io/v1beta3|k explain flowschemas --api-version=flowcontrol.apiserver.k8s.io/v1beta2` specific api version
- `k get pods --watch -v 6` - watch for changes


API Paths:
 - Core API (legacy)
   - `http://apiserver:port/api/$version/$resource-type`
   - `http://apiserver:port/api/$version/namespaces/$namespace/$resource-type/$resource-name` - namespaced
- API Groups
  - `http://apiserver:port/apis/$groupname/$version/$resource-type`
  - `http://apiserver:port/apis/$groupname/$version/namespaces/$namespace/$resource-type/$resource-name` - namespaced
https://kubernetes.io/docs/concepts/overview/kubernetes-api/
- how to check api path
  - `k get pod -v 6`


Call API via curl
```
k proxy
curl -k http://localhost:8001/api/v1/namespaces/default/pods/{pod} -v6

e.g.
curl -k http://localhost:8001/api/v1/namespaces/default/pods/nginx-7854ff8877-x68q4/log\?container\=nginx

sudo lsof -i -P -n | grep LISTEN - if port is used
```

Verify connection
`netstat -plant | grep kubectl`

Selectors & Lables
  - `k get pods --show-labels`
  - `k get pods --selector tier=prod`
  - `k get pods --selector tier!=prod`
  - `k get pods -l 'tier in (prod,qa)'`
  - `k get pods -l 'tier in (prod,qa)' --show-labels`
  - `k get pods -n kube-system -L controller-revision-hash` - show label as column
  - `k logs --selector 'k8s-app=kubedns' --follow`

Deployments:
  - `kubectl create deployment hello-world --image=nginx:1.24.0-alpine-slim`
  - `kubectl set image deployment hello-world --image=nginx:1.25.4-alpine-slim --record`
  - `k rollout status deployment hello-world`
  - `k scale deployment hello-world --replcias=3`
  - `k rollout pause deployment {dep-name}`
  - `k rollout resume deployment {dep-name}`
  - `k rollout history deployment hello-world`
  - `k rollout history deployment hello-world --revision=1`
  - `k rollout undo deployment hello-world`
  - `k rollout undo deployment hello-world --to-revision=1`
  - `k rollout restart deployment hello-world`
  
Events:
 - `k get events --sort-by='.lastTimestamp'`

Secrets:
  - `kubectl get secret db-user-pass -o json | jq '.data | map_values(@base64d)'`
  - `kubectl get secrets/db-user-pass --template={{.data.password}} | base64 -D`

Admin:
  - `kubectl cordon node`
  - `kubectl drain node --ignore-daemosets`

Tips:
  - find dns name for service
    `kubectl get service -n kube-system | grep {dns}`
    `kubectl get service -n powerflex | grep {service}`
    `nslookup {service-ip} {dns-ip}`

  - network ss
    `ss -l` - list sockets
    `ss -t -a` - -t, the -u, or the -x options alone will only list out those connections that are established, -a connections that are listening
    `ss -4 state listening` - filter by state
    `ss dst 192.168.1.139` - connections to specific address

  - ssl
    `openssl s_client -connect host:port`    