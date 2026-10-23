## Check resource Quata

```
# Check current CPU and memory utilization on every node
oc adm top nodes

# Check CPU and memory utilization of all pods
oc adm top pods -A

# Check individual container resource consumption
oc adm top pods -A --containers

# Check CPU/memory allocations and node conditions
oc describe nodes

# Review project resource quotas
oc get resourcequota -A

# Review default and maximum resource constraints
oc get limitrange -A
```
--------------------------------------------------------------------------
# Check Horizontal Pod Autoscalers in all namespaces
```
oc get hpa -A

# Check PodDisruptionBudgets in all namespaces
oc get pdb -A
```



--------------------------------------------------------------------------

## Networkpolocy

```
oc get networkpolicy -A
oc get route -A
```

__________________________________________________________________________

## Roles 
```
oc get clusterrolebindings

# List namespace-level role bindings
oc get rolebindings -A


##Find who has the cluster-admin role
# Find ClusterRoleBindings that grant the cluster-admin role

oc get clusterrolebinding -o json | jq -r '
.items[] |
select(.roleRef.name == "cluster-admin") |
[
  .metadata.name,
  ([.subjects[]? | (.kind + ":" + .name)] | join(","))
] | @tsv'
```
----------------------------------------------------------------------------
### SCC: Security Context Constraints.
#### check ssc
```
oc get scc
# Display SCC names and important security settings
oc get scc -o custom-columns='NAME:.metadata.name,PRIVILEGED:.allowPrivilegedContainer,ROOT_POLICY:.runAsUser.type,HOST_NETWORK:.allowHostNetwork,HOST_PATH:.allowHostDirVolumePlugin,ESCALATION:.allowPrivilegeEscalation,PRIORITY:.priority'


# Find identities with RBAC permission to use privileged SCC
oc adm policy who-can use scc privileged

# Find identities with RBAC permission to use anyuid SCC
oc adm policy who-can use scc anyuid
```



## Display Pod name, namespace, and assigned SCC
```
oc get pods -A \
  -o custom-columns='NAMESPACE:.metadata.namespace,POD:.metadata.name,SCC:.metadata.annotations.openshift\.io/scc'

```
