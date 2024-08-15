# https://github.com/kubernetes/ingress-nginx

# Instalando um Ingress Controller

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml

# Você pode utilizar a opção wait do kubectl, assim quando os pods estiverem prontos, ele irá liberar o shell

kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s

# No comando acima, estamos esperando que os pods do Ingress Controller estejam prontos, com o label app.kubernetes.io/component=controller, no namespace ingress-nginx, e caso não estejam prontos em 90 segundos, o comando irá falhar.


# Verificando a classe do controller
k get ingressclasses.networking.k8s.io