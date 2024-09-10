# Criação da service account service-account.yaml

# criação do secret para pegar o token service-account-secret.yaml

# Coletando o token e realizando o dcode da base64
kubectl get secrets service-account-secret -o jsonpath='{.data.token}' | base64 -d

# Criando a role role-sa.yaml

# Associando um pod na serviceaccount pod-exemple-sa.yaml

# OBS: dentro do pod o local onde fica as serviceaccount
/var/run/secrets/kubernetes.io/serviceaccount/


# Testando
curl -k -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/servi
ceaccount/token)" https://kubernetes.default.svc/api/v1/namespaces/default/pods