---?image=template/img/orchestration.jpeg

@title[Docker Orchestration]

@snap[north text-white span-100]
@fa[terminal fa-2x](Docker Orchestration)
@snapend

+++
@title[Overview]

@snap[north-west]
### Overview - Technologies
@snapend

@snap[west span-100]
@ul[](false)
- Swarm
- Kubernetes (K8S)
- Apache Mesos
@ulend
@snapend

+++
@title[Overview]

@snap[north-west]
### Overview - PaaS
@snapend

@snap[west span-100]
@ul[](false)
- Giant Swarm
- Deis
- Rancher
- Nomad
@ulend
@snapend

+++
@title[Overview]

@snap[north-west]
### Overview - Cloud
@snapend

@snap[west span-100]
@ul[](false)
- EKS
- ECS
- AKS
- GKE
@ulend
@snapend

+++
@title[Docker Swarm]

@snap[north-west]
### Docker Swarm
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/engine/swarm/#feature-highlights) 
@snapend

Cluster management integrated with Docker Engine

Decentralized design

Scaling

Multi-host networking

Service discovery

Load balancing

+++
@title[CLI reference - swarm]

@snap[north-west]
### CLI reference - swarm
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/swarm/reference/swarm/) 
@box[bg-gray rounded](docker swarm [OPTIONS] COMMAND [arg...])
@snapend
<br/>

Parameter | Description
--------- | -------------
  init | Initialize a swarm
  join | Join a swarm
  leave | Leave the swarm
  update | Update the swarm


+++
@title[Exercise]

@snap[north-west]
### Exercise
@snapend

@snap[west span-100]
@ol[](false)
- Go to [www.play-with-docker.com]
- Add 3 nodes
- Initialize master
- Join the other as nodes
- Have a look with `docker node ls`
@olend
@snapend

+++
@snap[north-west]
### Exercise (Answer)
@snapend

@title[Answer]
```sh
# Deploy compose file
docker swarm init --advertise-addr=[IP]

# Join Nodes
docker swarm join --token [TOKEN] [IP]:2377

# List Service
docker node ls
```

@[1-2]
@[4-5]
@[7-8]

+++
@title[CLI reference - service 1/2]

@snap[north-west]
### CLI reference - service 1/2
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/engine/reference/commandline/service/) 
@box[bg-gray rounded](docker service COMMAND)
@snapend
<br/>

Parameter | Description
--------- | -------------
create | Create a new service
inspect | Display detailed information on one or more services
logs | Fetch the logs of a service or task
ls | List services

+++
@title[CLI reference - service 2/2]

@snap[north-west]
### CLI reference - service 2/2
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/engine/reference/commandline/service/) 
@box[bg-gray rounded](docker service COMMAND)
@snapend
<br/>

Parameter | Description
--------- | -------------
ps | List the tasks of one or more services
rollback | Revert changes to a service's configuration
scale | Scale one or multiple replicated services
update | Update a service

+++
@title[Exercise]

@snap[north-west]
### Exercise
@snapend

@snap[west span-100]
@ol[](false)
- Upload your docker-compose file with wordpress
- Deploy it into your Swarm cluster
- Find out where your containers are
- Scale wordpress to 3
@olend
@snapend

+++
@title[Answer]
@snap[north-west]
### Exercise (Answer)
@snapend

```sh
# Deploy compose file
docker deploy --compose-file=wordpress-compose.yml WORDPRESS

# List local container
docker ps

# List Service
docker service ls

# Scale
docker service scale WORDPRESS_wordpress=3
```

@[1-2]
@[4-5]
@[7-8]
@[10-11]

+++

@snap[north-west]
### Exercise
@snapend

@snap[west span-100]
@ol[](false)
- Scale wordpress to 5
- Monitor what happens
- Look where the containers are
- Remove a node
- Monitor what happens
@olend
@snapend

+++
@title[Answer]

@snap[north-west]
### Exercise (Answer)
@snapend

```sh
# Scale
docker service scale WORDPRESS_wordpress=5

# Inspect
docker service ps WORDPRESS_wordpress
```

@[1-2]
@[4-5]

+++
@title[Kubernetes]

@snap[north-west]
### Kubernetes
@snapend

@snap[north-east]
### [@fa[info]](https://kubernetes.io) 
@snapend

Cluster management 

Storage orchestration

Scaling

Multi-host networking

Service discovery

Load balancing

+++
@title[Kubernetes - POD]

@snap[north-west]
### Kubernetes - POD
@snapend

@snap[north-east]
### [@fa[info]](https://kubernetes.io) 
@snapend
Smallest unit in K8s

Can be single or multi container

Share network and storage

+++
@title[CLI reference - kubeadm]

@snap[north-west]
### CLI reference - kubeadm
@snapend

@snap[north-east]
### [@fa[info]](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm) 
@box[bg-gray rounded](kubeadm COMMAND [arg...])
@snapend
<br/>

Parameter | Description
--------- | -------------
  init | Initialize k8s master
  join | Join a k8s node
  reset | Leave the cluster
  upgrade | Update the cluster


+++
@title[Exercise]

@snap[north-west]
### Exercise
@snapend

@snap[west span-100]
@ol[](false)
- Go to [labs.play-with-k8s.com]
- Add 3 nodes
- Initialize master
- Initialize network
- Join the other as nodes
- Have a look with `kubectl get nodes`
@olend
@snapend

+++
@snap[north-west]
### Exercise (Answer)
@snapend

@title[Answer]
```sh
# Deploy compose file
kubeadm init --apiserver-advertise-address $(hostname -i)

# Initialize network
kubectl apply -n kube-system -f \
    "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 |tr -d '\n')"

# Join Nodes
kubeadm join [IP]:6443 --token [TOKEN] --discovery-token-ca-cert-hash [HASH]

# List Service
kubectl get nodes
```

@[1-2]
@[4-6]
@[8-9]
@[11-12]

+++
@title[CLI reference - kubectl 1/2]

@snap[north-west]
### CLI reference - kubectl 1/2
@snapend

@snap[north-east]
### [@fa[info]](https://kubernetes.io/docs/reference/kubectl/overview/) 
@box[bg-gray rounded](kubectl [command] [TYPE] [NAME] [flags])
@snapend
<br/>

Parameter | Description
--------- | -------------
get | List one or more resources
describe | Display the detailed state
logs | Print the logs for a container in a pod
exec | Execute a command 

+++
@title[CLI reference - kubectl 2/2]

@snap[north-west]
### CLI reference - kubectl 2/2
@snapend

@snap[north-east]
### [@fa[info]](https://kubernetes.io/docs/reference/kubectl/overview/) 
@box[bg-gray rounded](kubectl [command] [TYPE] [NAME] [flags])
@snapend
<br/>

Parameter | Description
--------- | -------------
create | Create one or more resources 
delete | Delete resources
run | Run a specified image 
patch | Update one or more fields

+++
@title[Exercise]

@snap[north-west]
### Exercise
@snapend

@snap[west span-100]
@ol[](false)
- Run wordpress container
@olend
@snapend

+++
@title[Answer]
@snap[north-west]
### Exercise (Answer)
@snapend

```sh
# Deploy wordpress
kubectl run wordpress --image=wordpress:latest --port=8000
```

+++
@title[Generate YAML]
@snap[north-west]
### Generate YAML
@snapend

```sh
kubectl get deployment wordpress -o yaml | less
```

+++
@title[Generate YAML]
@snap[north-west]
### Generate YAML
@snapend

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: SOME_DATE
  generation: 1
  labels:
    run: wordpress
  name: wordpress
  namespace: default
  resourceVersion: "5333"
  selfLink: /apis/extensions/v1beta1/namespaces/default/deployments/wordpress
  uid: 311691d6-f2ec-11e8-8c8b-024208017631
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      run: wordpress
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: wordpress
    spec:
      containers:
      - image: wordpress:latest
        imagePullPolicy: Always
        name: wordpress
        ports:
        - containerPort: 8000
          protocol: TCP
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  conditions:
  - lastTransitionTime: SOME_DATE
    lastUpdateTime: SOME_DATE
    message: Deployment does not have minimum availability.
    reason: MinimumReplicasUnavailable
    status: "False"
    type: Available
  - lastTransitionTime: SOME_DATE
    lastUpdateTime: SOME_DATE
    message: ReplicaSet "wordpress-565d787b8f" is progressing.
    reason: ReplicaSetUpdated
    status: "True"
    type: Progressing
  observedGeneration: 1
  replicas: 1
  unavailableReplicas: 1
  updatedReplicas: 1
  ```
@[1-2]
@[3-14]
@[15]
@[17]
@[22-26]
@[32-39]
@[48-65]
