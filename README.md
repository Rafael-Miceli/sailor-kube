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

> Lembrando que usando Hyper-V na etapa de ajustar seu driver de rede tem um gotcha que é: Seu driver de rede não pode estar compatilhado, se não você toma o erro (0x8000FFFF)

4 - Para configurar Minikube com seu Hyer-V, abra o Powershell e execute o seguinte comando: `minikube start --vm-driver hyperv --kubernetes-version v1.7.3  --hyperv-virtual-switch nome-do-seu-switch`

> Tem outro a passo a passo mais completo muito bom: https://medium.com/@JockDaRock/minikube-on-windows-10-with-hyper-v-6ef0f4dc158c

#### Output

- Após a instalação, para verificar se obteve sucesso execute `kubectl get nodes` com Powershell e verifique se você possui um node, caso tenha alguma problema abra uma [Issue](https://github.com/Rafael-Miceli/sailor-kube/issues)

### Subir Deployment e Service para Kubernetes no Minikube

>Para mais informações a respeito do que é um [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) e um [Service](https://kubernetes.io/docs/concepts/services-networking/service/) no K8S

#### Porque e Objetivo:

Subindo sua aplicação no Minikube é perfeito para testar localmente PoCs (Prof of Concepts).

#### Cenário inicial

- Minikube já instalado e configurado.

#### Passo a Passo

1 - Prepare um deployment de forma declarativa como o seguinte:

```yml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec: 
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
          name: nginx
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: nginx

```

2 - Execute o seguinte comando no powershell com o yml acima: `kubectl create -f .\yml-acima.yml`

3 - Execute os seguinte comando para verificar se seu Deployment foi criado: `kubectl get dployments`. Deve aprecer o Deployment nginx com 2 replicas.

4 - Execute os seguinte comando para verificar se seu Service foi criado: `kubectl get services`, deve aparecer seu service com o Ip Binded nele.


#### Output

Para testar sua subida no Minikube pegue a porta que foi gerada pelo minikube do service que você subiu. Ou verifique se ele está no dashboard na porta 30000 do Ip da sua VM.

### Preparar AKS

Quick Start da Azure: https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough

### Trocar de contexto para Azure

Caso você esteja usando seu Kubectl apontando para mais de um cluster lembre que o comando `kubectl config use-context [my-context]` troca o contexto.

Para saber quais contextos você tem configurado analise seu `config` dentro da pasta `.kube` no diretório do seu usuário.

- Transformar Compose para Kubernetes Deployments
https://github.com/kubernetes/kompose