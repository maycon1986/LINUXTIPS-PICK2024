# Verificando as roles
kubectl get role -n <namespace>

# Verificando as rolesBinding
kubectl get rolebindings.rbac.authorization.k8s.io -n <namespace>

# Adicionando o usuario developer na config do kubeconfig
# --client-certificate -> Passa o certificado no kubeconfig
# --client-key -> Passa a chave no kubeconfig 
# --embed-certs -> Serve para imbutir o certificado no kubeconfig
kubectl config set-credentials developer --client-certificate developer.crt --client-key developer.key --embed-certs

# Listando os usuários que estão no kubeconfig
k config get-users

# Criando um contexto chamado developer-aula no cluster lab maycon no namespace dev com o usuario developer
k config set-context developer-aula --cluster <nome-cluster> --namespace dev --user developer

