# Openshift 
To start with you can enable trial from here [Redhat openshift developer sandbox ](https://developers.redhat.com/developer-sandbox)
## Setup OC command in local machine
```
wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/latest/openshift-client-linux.tar.gz
tar -xvf openshift-client-linux.tar.gz
cd openshift-client-linux
chmod +x oc
sudo mv oc /usr/local/bin/
```
Now copy the oc login command and token from openshift console.


## Deployment of Application
```
oc create deploy myapp --image=nginxinc/nginx-unprivileged
oc expose deploy myapp --port=8080 --target-port=80
oc expose svc/myapp
oc get route
```
## Build
It would be easier to use ``oc new-build`` and then ``oc new-app`` if you really need to set this up as two steps for some reason. If you just want to setup the build and deployment in one go, just use ``oc new-app``.

For example, to setup build and deployment in one go use:
```
oc new-app --name myapp <repository-url>
```
To do it in two steps use:
```
oc new-build --name=demo1  https://github.com/mevijays/training-k8s --context-dir=openshift/static
oc new-app demo1
```
### Example dockerfile build from github 
- Perform a dry-run
```
oc new-app --name=ibmdb https://github.com/mevijays/training-k8s --context-dir=openshift/static --dry-run -o yaml
```
- Now deploy 
```
oc new-app --name=ibmdb https://github.com/mevijays/training-k8s --context-dir=openshift/static 
```
- Now expose route 
```
oc expose svc/ibmdb
```
### Import external registry images in openshift
```
oc import-image  hello-k8s:latest --from=docker.io/sharmavijay86/hello-k8s:latest --confirm
```
