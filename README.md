# Guide

- Change directory to `cluster` and Create minikube cluster `minikube start --nodes 2 -p multinode-demo`
- Once the cluster is running run `kubectl get no` to get the node names.
- add labels to nodes `kubectl label no ${MASTERNODE} app=v1` and `kubectl label no ${WORKERNODE} app=v2`
- deploy app1 `kubectl apply -f app1/` if there you get `ImagePullBackOff` error or `context deadline exceed` just exec to master node by running  `minikube -p multinode-demo ssh` and manually pull the image `dokcer pull alviahmed/app1`
- deploy app1 `kubectl apply -f app2/` if there you get `ImagePullBackOff` error or `context deadline exceed` just exec to master node by running  `minikube -p multinode-demo -n $WORKERNODENAME ssh` and manually pull the image `dokcer pull alviahmed/app2`
- deploy nginx `kubectl apply -f nginx` service should be available in nodeport. We can confirm this by first logging in to master node `minikube -p multinode-demo ssh` and then `curl http://$MASTERNODEIP:30007/app1` this should return the page in app1.
- to view the pages in browser run `minikube -p multinode-demo service nginx` and add `/app1` or `/app2` at the end of the url opened in the browser.