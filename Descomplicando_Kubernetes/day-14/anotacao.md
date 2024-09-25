https://kyverno.io/docs/installation/#security-vs-operability

# Instalação Kyverno

# Repositório
helm repo add kyverno https://kyverno.github.io/kyverno/

helm repo update

# Instalação
helm install kyverno kyverno/kyverno --namespace kyverno --create-namespace


# Comandos
# Polices do cluter Polices
kubectl get clusterpolicies
