# Prometheus / Grafana Playground

Playground para experimentação local de prometheus e grafana.

## Ambiente

Para utilizar o playground é necessário ter o Kubernetes, Kubectl e o Helm instalado.

Para instalação do kubernetes localmente, sugiro o uso de [docker-desktop](https://docs.docker.com/desktop/kubernetes/) ou [orbstack](https://docs.orbstack.dev/kubernetes/).

## Instalando o Playground

1. Adicione os repositórios de prometheus e grafana do HELM

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

```bash
helm repo add grafana https://grafana.github.io/helm-charts
```

```bash
helm repo update
```

2. Crie o namespace para nosso playground

```bash
kubectl create ns playground
kubectl config set-context --current --namespace playground
```

3. Instale Prometheus

```bash
helm upgrade --install prometheus -n playground -f prometheus/values.yaml prometheus-community/prometheus
```

4. Instale Grafana
```bash
helm upgrade --install grafana -n playground -f grafana/values.yaml grafana/grafana
```

5. Verifique as instalações
```bash
helm list
```

## Acessando as ferramentas

Para acessar as ferramentas basta descobrir em qual IP ficou disponível cada uma delas. (Isso difere para cada instalação)

Exemplo:
```bash
$ kubectl get services
NAME                            TYPE        CLUSTER-IP        EXTERNAL-IP   PORT(S)    AGE
prometheus-kube-state-metrics   ClusterIP   192.168.194.176   <none>        8080/TCP   6s
prometheus-server               ClusterIP   192.168.194.242   <none>        80/TCP     6s
grafana                         ClusterIP   192.168.194.247   <none>        80/TCP     2s
```

Para acessar o grafana você pode utilizar as credenciais: grafana/grafana

## Desinstalando

```bash
helm uninstall grafana
```

```bash
helm uninstall prometheus
```