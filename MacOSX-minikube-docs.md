# Zero-Downtime

## Prereqs:
Docker Desktop installed and working

## Prep: 
Install minikube and watch
```
brew install minikube
brew install watch
```

## Create k8s cluster
```
minikube start --vm-driver=hyperkit --memory=4096
```
## Start Watcher
in a new terminal window (aka: termwin1)
```
watch -n0.1 kubectl get svc,pod,ep,deploy
```

## Install test app
in a new terminal window (aka: termwin2)
```
kubectl apply -k k8s
```

## Start Traffic:
in a new terminal window (aka: termwin3)
```
kubectl run siege --image=jstarcher/siege #SERVICEIPADDR# --rm -it
```

## Run Scenarios
in terminal window termwin2
Demonstrate downtime with standard RollingUpdate
- modify line 22 in k8s/nginx/deploy.yaml to change version

Demonstrate downtime with standard RollingUpdate w/ lifecycle probes
- apply probe kustomization
- - ```kubectl apply -k kustom-probes/ ```
- modify line 22 in k8s/nginx/deploy.yaml to change version

Demonstrate downtime with standard RollingUpdate w/ lifecycle probes and prestop sleep
- apply probe kustomization
- - ```kubectl apply -k kustom-probes-prestop/ ```
- modify line 22 in k8s/nginx/deploy.yaml to change version