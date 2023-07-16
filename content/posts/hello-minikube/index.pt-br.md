---
title: Hello Minikube para ppc64le
date: 2021-12-15
draft: false
author: "Junior Santos"
authorLink: "https://jr-santos98.github.io/about/"
description: "Um tutorial para minikube."

tags: ["Tutorial", "Minikube", "Kubernetes"]
categories: ["Tutoriais"]
---

Este tutorial mostra como criar um cluster para processadores da arquitetura Power (ppc64/ppc64le) utilizando o Minikube.

<!--more-->

![Logo of minikube](hello_minikube.png)

O tutorial foi realizado no Ubuntu Server 20.04 LTS (ppc64le), o pacote utilizado foi baixado
utilizando o repositório de arquivos do [OpenPower Lab @ Unicamp](https://openpower.ic.unicamp.br/project/power-repository/).

## Dependências

Para seguir com este tutorial, os sequintes pacotes são requeridos:
- Minikube
- Kubectl
- Docker-ce
- Conntrack

Os pacotes podem ser instalados através dos comandos a baixo:

```bash
apt-get update
apt-get install docker-ce conntrack minikube kubectl
```

> Pode ser que seja necessário adicionar o repositório do [OpenPower Lab @ Unicamp](https://openpower.ic.unicamp.br/project/power-repository/) no seu sistema.

> Opcionalmente, Kubeadm e Kubelet podem ser instalados.

## Criando um cluster com Minikube

1. Inicie o Minikube

```bash
sudo minikube start --driver=none
```

> O driver padrão é o Docker, entretanto o Minikube não reconhece que o Docker está disponível para a arquitetura ppc64le e apresenta uma mensagem de erro.

Para fazer 'none' o driver padrão utilize:

```bash
sudo minikube config set driver none
```

> Talvez seja necessário rodar o comando: `sudo sysctl fs.protected_regular=0`

2. Verifique o status

```bash
sudo minikube status
```

Saída esperada:

```bash
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```
3. Abra o dashboard do Kubernetes no seu navegador

```bash
sudo minikube dashboard
```

## Criando um Deployment

Existem duas estruturas em kubernetes: Pod e Deployment. Um Pod é um grupo de um ou mais containers,
enquanto que um Deployment verifica, gerencia e reinicia os Pods.
Dessa forma, o uso do Deployment é recomendado quando será utilizado um grupo de Pods.

1. Criando um Deployment

```bash
sudo kubectl create deployment hello-node --image=minicloud/node-server
```

> *[minicloud/node-server](https://hub.docker.com/r/minicloud/node-server)*: é uma imagem pública
de um container Docker criada para a arquitetura ppc64le. Os arquivos utilizados para construir a imagem
podem ser acessados pelo [GitHub](https://github.com/Unicamp-OpenPower/nodeServer).

2. Visualizando o Deployment:

```bash
sudo kubectl get deployments
```

Saída esperada:

```bash
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
hello-node   1/1     1            1           6m28s
```

3. Visualizando o Pod:

```bash
sudo kubectl get pods
```

Saída esperada:

```bash
NAME                          READY   STATUS    RESTARTS   AGE
hello-node-5dd47b76c8-l5vs2   1/1     Running   0          6m51s
```

## Criando um serviço

Para que sejá possível acessar o Pod, é necessário criar um serviço.

1. Criando um serviço

```bash
sudo kubectl expose deployment hello-node --type=NodePort --port=8080
```

2. Visualizando o serviço

```bash
sudo kubectl get services
```

Saída esperada:

```bash
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-node   NodePort    10.102.223.224   <none>        8080:31253/TCP   8s
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP          14m
```

Para abrir o serviço no seu navegador acesse: [http://localhost:8080/](http://localhost:8080/).

![Hello Minikube no navegador](screenshot.png)


> Se não for possível acessar, mude o 8080, para os 5 digitos apresentados após o 8080:*****.
Na execução do exemplo a porta criado foi a 31253.

## Limpeza de execução

Os recursos instanciados podem ser removidos executando:

```bash
kubectl delete service hello-node
kubectl delete deployment hello-node
```

Opcional: Parar o Minikube

```bash
minikube stop
```

Opcional: Deletar o Minikube

```bash
minikube delete
```

## Tutorial para outras arquiteturas

[Hello Minikube](https://kubernetes.io/docs/tutorials/hello-minikube/)
