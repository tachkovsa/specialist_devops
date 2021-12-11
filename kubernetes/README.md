### Установка Monikube на Ubuntu 20.04
apt install curl wget apt-transport-https virtualbox virtualbox-ext-pack -y
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
mv minikube-linux-amd64 /usr/local/bin/minikube && chmod 755 /usr/local/bin/minikube

### Установка Kubectl на Ubuntu 20.04
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | tee /etc/apt/sources.list.d/kubernetes.list
apt update && apt install kubectl -y

minikube start --driver=docker

### Установка Minikube на Fedora 33
Установить "PermitRootLogin yes" в /etc/ssh/sshd_config
Выключить SELinux в /etc/selinux/config
Ребутнуть сервер
dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
dnf install docker-ce
useradd -m -s /bin/bash -G wheel,docker admin
passwd admin
systemctl enable docker
systemctl start docker
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
mv minikube-linux-amd64 /usr/local/bin/minikube && chmod 755 /usr/local/bin/minikube

### Установка Kubectl на Fedora 33
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
mv kubectl /usr/local/bin/kubectl && chmod 755 /usr/local/bin/kubectl
su admin
minikube start --driver=docker
minikube addons enable ingress

Проброс сервиса наружу в minikube:
https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
