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

# Create Persistent Volume and Claim

```
```

