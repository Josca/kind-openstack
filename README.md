# OpenStack in k8s (kind)

## Requirements
- kind, helm

## Installation
~~~bash
# Add helm repos
helm repo add openstack-helm https://tarballs.opendev.org/openstack/openstack-helm
helm repo add openstack-helm-infra https://tarballs.opendev.org/openstack/openstack-helm-infra
helm repo update

# Create kubernetes cluster using kind and konfig from this repo
kind create cluster --config kind-cluster.yaml -n kind-openstack

# Install openstack components
helm install mariadb openstack-helm-infra/mariadb --namespace openstack --create-namespace -f values-mariadb.yaml
helm install rabbitmq openstack-helm-infra/rabbitmq --namespace openstack -f values-rabbitmq.yaml

# monitor pods and events
watch "kubectl get pod && kubectl get events | tail"
kubectl exec -it mariadb-server-0 -- mysql -uroot -p # connect to mysql (password: "password")
~~~

continue TODO
