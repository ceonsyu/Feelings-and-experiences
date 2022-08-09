## Define clusters, users, and contexts
Suppose there is two clusters, one for development work and one for scratch work. In the `development` cluster, some developers work in a namespace called `frontend`, some other developers work in a namespace called `storage`. Access to the development cluster requires authentication by certificate. Access to the scratch cluster requires authentication by username and password.
Create a directory named `config-exercise`. In the `config-exercise` directory, create a file named `config-demo` with this content:
```json
apiVersion: v1
kind: Config
preferences: {}

clusters:
- cluster:
  name: development
- cluster:
  name: scratch

users:
- name: developer
- name: experimenter

contexts:
- context:
  name: dev-frontend
- context:
  name: dev-storage
- context:
  name: exp-scratch
```
A configuration file describes clusters, users, and contexts. 

Go to the `config-exercise` directory.   Enter these commands to add cluster details to the `config-demo` file:
```shell
kubectl config --kubeconfig=config-demo set-cluster development --server=https://1.2.3.4 --certificate-authority=fake-ca-file
kubectl config --kubeconfig=config-demo set-cluster scratch --server=https://5.6.7.8 --insecure-skip-tls-verify
```
Add user details to the `config-demo` file:
```shell
kubectl config --kubeconfig=config-demo set-credentials developer --client-certificate=fake-cert-file --client-key=fake-key-seefile
kubectl config --kubeconfig=config-demo set-credentials experimenter --username=exp --password=some-password
```
Add context details to the `config-demo` file:
```shell
kubectl config --kubeconfig=config-demo set-context dev-frontend --cluster=development --namespace=frontend --user=developer
kubectl config --kubeconfig=config-demo set-context dev-storage --cluster=development --namespace=storage --user=developer
kubectl config --kubeconfig=config-demo set-context exp-scratch --cluster=scratch --namespace=default --user=experimenter
```

Then, the `config-demo` will be:
```json 
apiVersion: v1
clusters:
- cluster:
    certificate-authority: fake-ca-file
    server: https://1.2.3.4
  name: development
- cluster:
    insecure-skip-tls-verify: true
    server: https://5.6.7.8
  name: scratch
contexts:
- context:
    cluster: development
    namespace: frontend
    user: developer
  name: dev-frontend
- context:
    cluster: development
    namespace: storage
    user: developer
  name: dev-storage
- context:
    cluster: scratch
    namespace: default
    user: experimenter
  name: exp-scratch
current-context: ""
kind: Config
preferences: {}
users:
- name: developer
  user:
    client-certificate: fake-cert-file
    client-key: fake-key-file
- name: experimenter
  user:
    password: some-password
    username: exp
```
The `fake-ca-file`, `fake-cert-file` and `fake-key-file` above are the **placeholders** for the path names of the certificate files. 

Set the current context:
```shell
kubectl config --kubeconfig=config-demo use-context dev-frontend
```
Now whenever you enter a `kubectl` command, the action will apply to the cluster, and namespace listed in the `dev-frontend` context. And the command will use the credentials of the user listed in the `dev-frontend` context.