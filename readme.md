### Create the kind cluster
kind create cluster --config kind-config.yaml

### Create node labels
kubectl label nodes frrk8stesting-worker2 tor=tor2

### Start adding manifests.
cd manifests

### Apply calico cni 
kubectl apply -f calico.yaml

### Apply the all in one frr-k8s installer 

kubectl apply -f frr-k8s.yaml

### Apply the selector for only labels of tor=tor2

kubectl apply -f selector.yaml

### Run the ansible-playbook to extract the information

ansible-playbook playbooks/frr-k8s.yaml
```json
"spec": {
                "bgp": {
                    "routers": [
                        {
                            "asn": 6500,
                            "neighbors": [
                                {
                                    "address": "1.2.3.4",
                                    "asn": 6501,
                                    "disableMP": false,
                                    "toAdvertise": {
                                        "allowed": {
                                            "mode": "all"
                                        }
                                    },
                                    "toReceive": {
                                        "allowed": {
                                            "mode": "all"
                                        }
                                    }
                                }
                            ]
                        }
                    ]
                },
```