GlusterFS server pod for OpenShift 3.

# Creating GlusterFS server pod

Edit scc.yml, replace YOUR_USERNAME with your login account, then

```
oc create -f scc.yml
oc create -f glusterd.json
oc create -f service.json
```

Once your service is created, run `oc get service glusterd`, you will get an IP of your service, replace `#SERVICE_IP#` with this IP in `endpoints.json`, then create an endpoint.

Assume your service ip is `172.30.172.117`, then:

```
sed -i s/#SERVICE_IP#/172.30.172.117/ endpoints.json
oc create -f endpoints.json
```

## Verifying GlusterFS server pod is functional

Once you have your server pod created, run `oc exec glusterd -- gluster volume status testvol details`, you should see `Status: Started`. If you haven't seen it, wait a short time until it's successfully deployed.

# Creating Persistent Volume and Claim

```
oc create -f pv-rwo.json
oc create -f pvc-rwo.json
oc get pv
oc get pvc
```

You should see PV and PVC are bound together

# Creating tester pod

Run `oc create -f pod.json`, when you see pod is `Running`, it has mounted the GlusterFS volume successfully.
