https://kubernetes.io/docs/reference/kubernetes-api/

- ` k create deployment nginx --image=nginx --dry-run=client -o yaml` - print sintacticaly correct template
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