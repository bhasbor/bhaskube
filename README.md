# Welcome to K8 command notebook!

All the usefull commands which can be refered

```sh
kubectl get namespaces
```

```sh
kubectl get roles --all-namespaces
```

```sh
kubectl get serviceaccounts --all-namespaces
```

To view the ClusterRoles on your system
```sh
kubectl get clusterroles

```sh
To interrogate a particular ClusterRole, input:
kubectl get clusterroles <name of role> -o yaml
```
You may also use the describe verb with ClusterRoles:
```sh
kubectl describe clusterrole view
```
To create a namespace called qa-test, input the following:
```sh
kubectl create namespace qa-test
```
To create a ServiceAccount called qa-test-account within the namespace qa-test, input:
```sh
kubectl --namespace=qa-test create serviceaccount qa-test-account
```
To create a role with the qa-test namespace called qa-tester-view that grants the get and list verb actions on the pods resource, input:
```sh
kubectl --namespace=qa-test create role qa-tester-view --verb=get --verb=list --resource=pods
```
To set up a Linux alias so you don’t have to specify the namespace on every command, input:
```sh
alias kubeqa='kubectl --namespace=qa-test'
```
If you set up the above alias, the commands to create the role would be:
```sh
kubeqa create role qa-tester-view --verb=get --verb=list --resource=pods
```
To describe the role, input either of the following:
```sh
kubectl --namespace=qa-test describe role/qa-tester-view
Or:
kubeqa describe role/qa-tester-view
```
Now the role must be bound to the ServiceAccount. To create the RoleBinding, input:
```sh
kubeqa create rolebinding qa-viewer --role=qa-tester-view --serviceaccount=qa-test:qa-test-account
```