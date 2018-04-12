# sailor-kube

## Discalimer

Este repositório possui códigos usados para demonstrar como subir uma aplicação para Kubernetes.

Este repositório segue um modelo **Just Do It**, com poucos detalhes, mas com passo a passo de como preparar um ambiente Kubernetes localmente.

Muitos links levam a referências para mais detalhes a respeito do que está sendo feito e para mais dúvidas abra um [Issue](https://github.com/Rafael-Miceli/sailor-kube/issues) neste repositório.

## Just Do It

O modelo **Just Do It** (JDI) consiste na seguinte estrutura:

- Porque e Objetivo do exemplo
- Cenário inicial necessário para reproduzir o exemplo
- Passo a Passo do exemplo
- Output após exemplo concluido.

### Preparar K8S em maquina local

#### Porque e Objetivo:

- K8S é o [orquestrador de facto](https://www.thoughtworks.com/radar/platforms/kubernetes) para suas aplicações em containers, crescimento rápido na comunidade e com API extremamente robusta.

- O objetivo deste JDI é você ter sua maquina local com um Node K8S para explorar.

#### Cenário inicial

- Windows 10

- Hyper-V ou VirtualBox

#### Passo a Passo

1 - Instale o KubeCTL [aqui](https://kubernetes.io/docs/tasks/tools/install-kubectl/), e não esqueça de adicionar o KubeCTL ao seu path.

2 - Baixe e instale o [Minikube](https://github.com/kubernetes/minikube), não se esqueca de também adiciona-lo ao seu path

3 - Configure seu driver [hyper-v](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#hyperv-driver) ou virtualbox(sem link para esse infelizmente =/) para user o KubeCtl

4 - Para configurar Minikube com seu Hyer-V, abra o Powershell e execute o seguinte comando: `minikube start --vm-driver hyperv --kubernetes-version v1.7.3  --hyperv-virtual-switch nome-do-seu-switch`

#### Output

- Após a instalação, para verificar se obteve sucesso execute `kubectl get nodes` com Powershell e verifique se você possui um node, caso tenha alguma problema abra uma [Issue](https://github.com/Rafael-Miceli/sailor-kube/issues)

### Subir Deployment para Kubernetes no Minikube

### Preparar AKS

Quick Start da Azure: https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough

### Subir Deployment e Services do DockerHub para AKS

### Push de Imagem para ACR

### Subir Deployment e Services da ACR para AKS


Mais referências (porque nunca é demais):

- Transformar Compose para Kubernetes Deployments
https://github.com/kubernetes/kompose