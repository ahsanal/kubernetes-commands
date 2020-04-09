<p align="center"><img src="https://i.imgur.com/IYVX7a8.png" /></p>

What is Kubernetes?

> Kubernetes is a platform for managing containerized workloads. Kubernetes orchestrates computing, networking and storage to provide a seamless portability across infrastructure providers

## Cluster Info
```sh
> kubectl config                                                     # get the available commands that config has
> kubectl config current-context                                     # get the current context of the cluster
> kubectl config get-clusters                                        # get the k8s cluster
> kubectl config get-contexts                                        # get the contexts that cluster acquired
> kubectl config rename-context                                      # to rename the context of the cluster
> kubectl config set-context --current --namespace=[your namespace]  # change the current context of the cluster
> kubectl config view                                                # view the config of the cluster
> kubectl cluster-info                                               # get the info about the cluster dns and master node
> kubectl get componentstatuses                                      # get the status of the components in the cluster like scheduler
```

## Viewing Resource Information

#### Nodes
```bash
> kubectl get no                                                                              # get the nodes you have
> kubectl get no -o wide                                                                      # get the wide description of the nodes
> kubectl get no --all-namespaces                                                             # get the all available nodes in the cluster
> kubectl get no --show-labels=[bool(true/false)]                                             # get the cluster info with the labels
> kubectl get no -o json                                                                      # get the node output in json
> kubectl get no --watch=true                                                                 # get the status of the nodes by every 2 seconds
> kubectl get no --sort-by='{.metadata.name}'                                                 # get the sorted info of the nodes
> kubectl get --filename=[path to the directory or yaml file]                                 # get the status of nodes using file path
> kubectl get no -o yaml                                                                      # get the nodes in yaml format
> kubectl get no --selector=[label_name]                                                      # get the nodes with the label name
> kubectl get no -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'  # get the node in the given path of json file
> kubectl describe no                                                                         # Describe the nodes
> kubectl describe no --all-namespaces                                                        # Describe the nodes in all namespaces
> kubectl describe no [node_name]                                                             # Describe a particular node
> kubectl describe --filename=[path to the directory or yaml file]                            # get the described nodes using file path
> kubectl delete no [node_name]                                                               # to delete the node with give node name
```
#### Pods
```bash
> kubectl get po                                                 # get the pods in the current namespace
> kubectl get po -o wide                                         # get the pods in the current namespace in wide 
> kubectl get po --show-labels                                   # get the pods with their labels
> kubectl get po -l app=nginx                                    # get the pods with the label name app=nginx
> kubectl get po -o yaml                                         # get the pods output in yaml format
> kubectl get pod [pod_name] -o yaml --export                    # get the output in yaml format of a particular pod
> kubectl get pod [pod_name] -o yaml --export > nameoffile.yaml  # export the output of pod in some file
> kubectl get pods --field-selector status.phase=Running         # check that pods which are running
> kubectl get po --all-namespaces                                # get pods of all the namespaces
> kubectl get po --allow-missing-template-keys=true              # If true, ignore any errors in templates when a field or map key is missing in the template. Only applies to golang and jsonpath output formats.
> kubectl get po --chunk-size=500                                # Return large lists in chunks rather than all at once. Pass 0 to disable.
> kubectl get po -o json                                         # get the pods in json format
> kubectl get po --watch=true                                    # apply watch to get the status of every pod in 2 seconds
> kubectl get po --sort-by='{.metadata.name}'                    # get the sorted info about the pods
> kubectl describe po                                            # describe the pods
> kubectl describe po --all-namespaces                           # describe the pods in all namespaces
> kubectl describe po [pod_name]                                 # describe the pod given with the name 
> kubectl delete po [pod_name]                                   # delete the given name pod
> kubectl delete pods --all                                      # delete all the pods in current namespace
```

#### Namespaces
```bash
> kubectl get ns                        # get all the namespaces
> kubectl get ns -o yaml                # get the output of namespace in yaml format
> kubectl get ns -o json                # get the output of namespace in json format
> kubectl describe ns [your namespace]  # describe the given namespace
> kubectl describe ns                   # describe all the namespaces
> kubectl delete ns [your namespace]    # delete the given namespace
```

#### Services
```bash
> kubectl get svc                        # get the services in current namespace
> kubectl get svc -o wide                # get the services in wide format
> kubectl get svc -o yaml                # get the services in yaml format
> kubectl get svc --show-labels          # get the services with their labels
> kubectl get svc --all-namespaces       # get services in all namespaces
> kubectl describe svc                   # describe all the services
> kubectl describe svc [service_name]    # describe the given service name
> kubectl describe svc --all-namespaces  # describe the services in all namespaces
> kubectl delete svc -l key=value        # delete the svc with the given label
> kubectl delete svc --all               # delete all the svc in current namespace
```

#### Deployments
```bash
> kubectl get deploy                        # get the deployments in current namespace
> kubectl get deploy -o wide                # get the deployments in wide info
> kubectl get deploy -o yaml                # get the deployments in yaml format
> kubectl get deploy --all-namespaces       # get the deployments in all namespaces
> kubectl describe deploy                   # describe all the deployments
> kubectl describe deploy [deploy_name]     # describe the given name deployment
> kubectl describe deploy --all-namespaces  # describe the deployments in all namespaces
> kubectl delete deploy [deploy_name]       # delete the given name deployment
> kubectl delete deploy --all               # delete all the deployments in current namespace
```

#### ConfigMaps
```bash
> kubectl get cm                            # get the current config map
> kubectl get cm -n=[namespace]             # get the config map given namespace
> kubectl get cm -n=[namespace] -o yaml     # get the config map given namespace in yaml format
> kubectl get cm --all -namespaces          # get the config map in all namespaces
> kubectl get cm --all -namespaces -o yaml  # get the config map in all namespaces in yaml format
> kubectl describe cm [configmap_name]      # describe the given name config map
> kubectl describe cm --all-namespaces      # describe the config map in all namespaces
> kubectl delete cm [configmap_name]        # delete the given name config map
> kubectl delete cm --all                   # delete all the config map in current namespace
```

#### Logs
```bash
> kubectl logs [pod_name]                                     # get the logs of the given pod name
> kubectl logs [pod_name] -n=[namespace]                      # get the logs of the given pod name in given namespace
> kubectl logs --since=1h [pod_name]                          # get the logs of the given pod name since one hour
> kubectl logs --tail=20 [pod_name]                           # get the last 20 lines of the logs of the given pod 
> kubectl logs -f -c [container_name][pod_name]               # begin the streaming of the logs of the given container name in the given pod name
> kubectl logs [pod_name] > pod.log                           # export the logs in pod.log of the given pod name
> kubectl logs [pod_name] --all-containers=true               # get the pod has multi containers
> kubectl logs -l key=value --all-containers=true             # get the logs from all containers have given label
> kubectl logs -p -c [container_name] [pod_name]              # get the previous terminated logs in the given container name with the given pod name
> kubectl logs --insecure-skip-tls-verify-backend [pod_name]  # show logs from a kubelet with an expired serving certificate
> kubectl logs job/[job_name]                                 # get the logs with the given job name
> kubectl logs deployment/[deploy_name] -c [container_name]   # get the logs from given container name of the given deployment name
```

#### Secrets
```bash
> kubectl get secrets                         # get the secrets in current namespace
> kubeclt get secrets -n=[namespace]          # get the secrets in the given namespace
> kubectl get secrets -n=[namespace] -o yaml  # get the secrets in the given namespace in yaml format
> kubectl get secrets --all -namespaces       # get the secrets in all the namespaces
> kubectl get secrets -o yaml                 # get the secrets in current namespace in yaml format
> kubectl describe secret [secret_name]       # describe the given secret name
> kubectl describe secret --all-namespaces    # describe the secrets in all namespaces
> kubectl delete secret [secret_name]         # delete the secret with given name
```

#### ReplicaSets
```bash
> kubectl get rs                         # get the replica sets in current namespace
> kubectl get rs -o wide                 # get the replica sets in wide format
> kubectl get rs -o yaml                 # get the replica sets in yaml format
> kubectl describe rs                    # describe all the replica sets
> kubectl describe rs --all-namespaces   # describe the secrets in all namespaces
> kubectl describe rs [replicaset_name]  # describe the given replica set name
> kubectl delete rs [replicaset_name]    # delete the given replica set name
```
