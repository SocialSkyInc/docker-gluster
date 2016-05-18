# GlusterFS server pod

## Creating GlusterFS server pod

```
# Edit scc.yml, replace YOUR_USERNAME with your login account
oc create -f scc.yml

# Create Glusterfs server pod
oc create -f glusterd.json

# Create service
oc create -f service.json
```

Once your service is created, run `oc get service glusterd`, replace `#SERVICE_IP#` with your service ip in `endpoints.json`.

Assume your service ip is `172.30.172.117`

```
sed -i s/#SERVICE_IP#/172.30.172.117/ endpoints.json
oc create -f endpoints.json
```

### Verifying GlusterFS server pod status

Once you have your server pod created, run `oc exec glusterd -- gluster volume status testvol details`, when you see `Status: Started`, your server is functional.

## Create Persistent Volume and Claim

```
oc create -f pv-rwo.json
oc create -f pvc-rwo.json
oc get pv
oc get pvc
```

You should see PV and PVC are bound together

## Create tester pod

Run `oc create -f pod.json`, when you see pod is `Running`, it has mounted the GlusterFS volume successfully.
