git clone https://github.com/prometheus-operator/kube-prometheus

### Basicamente o que fizemos foi a instalação de alguns CRDs (Custom Resource Definitions) que são como extensões do Kubernetes, e que são utilizados pelo Kube-Prometheus e com isso o Kubernetes irá reconhecer esses novos recursos, como por exemplo o PrometheusRule e o ServiceMonitor que irei falar mais a frente.
kubectl create -f manifests/setup/

### Com o comando nós estamos aplicando os manifests necessários para a instalação do Prometheus e do Alertmanager
kubectl apply -f manifests/

### O que é service monitor
ServiceMonitor (ou Service Monitor) é um recurso do Prometheus Operator, que permite coletar métricas de aplicativos em execução dentro de pod.

kubectl get servicemonitors.monitoring -n monitoring

### Verificar os resources customizados.
kubectl get customresourcedefinitions.apiextensions.k8s.io

### Conectando um container especifico dentro do pod
kubectl exec -it <nome-pod> -c <nome-container> --bash