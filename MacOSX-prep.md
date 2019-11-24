# Zero-Downtime

## Prereqs:
Docker Desktop installed and working

## Prep: 
Install kind and watch
```
brew install kind
brew install watch
```

## Create k8s cluster
```
kind create cluster
```
## Start Watcher
in a new terminal window
```
watch -n0.1 kubectl get pod,ep
```

## Install test app
```
kubectl apply -k k8s
```

## Test deployment: 
```
docker run -it busybox wget -qO- 172.17.0.2:80
```
## Start Traffic:
in a new terminal window
```
docker run --rm -t jstarcher/siege -c5  172.17.0.2
```
