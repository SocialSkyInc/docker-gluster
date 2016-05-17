# GlusterFS server pod

## Creating GlusterFS server pod for OpenShift

The GlusterFS server pod **must** run as privileged container, otherwise it can not create the gluster volume when the container starts. To allow privileged containers on OpenShift, run `oc edit scc restricted`, set `allowPrivilegedContainer: true` and save.

```
# Create Glusterfs server pod
oc create -f glusterd.json

# Create service
oc create -f service.json
```

Your GlusterFS server pod should be ready!

# Test server pod

```
# Edit endpoints.json, replace the ip with service ip, then create it
oc create -f endpoints.json

# Create the test pod
```

