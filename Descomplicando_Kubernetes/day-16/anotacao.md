
# Verificar se o cluster suporta o Networking Policies
kubectl api-versions | grep networking

# Listando os networkpolicies
kubectl get networkpolicies -n <namespace>
kubectl get netpol

# Conectando um pod para tester (Somente para ter um shell)
kubectl run -ti alpine --image alpine -- sh
apk add curl
apk add  redis

# Testando na aplicacao
curl giropops-senhas.giropops.svc.cluster.local:5000