# k8/React/Nodemon on Windows Host

This is a simple example of getting a react app to allow development on a K8 cluster reloading local changes on the host computer on Windows.

### Why?

See the issue here: [Inotify on shared drives does not work](https://github.com/docker/for-win/issues/56#issuecomment-242135705)

### What is here:

A vanilla react app created with create-react-app

pod.yaml, k8 file to create your app and pull in your local storage as a volume (edit your path in line 17)

ingress.yaml, basic ingress to pull it all together

HOWTO:

### Build the container:
docker build -t react:app .

### Set up ingress (NGINX)

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml

### Build pod/service/ingress

kubectl apply -f pod.yaml

kubectl apply -f ingress.yaml

### Edit your local machines host file to have the name resolve:

127.0.0.1 k8.local

### Test

Browse to http://k8.local 

Make a change to src/app.js, save it...

Refresh browser...
