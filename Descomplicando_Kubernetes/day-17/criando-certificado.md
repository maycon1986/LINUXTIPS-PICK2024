## Criando o certificado

# gerando uma chave rsa de 2048 bits
openssl genrsa -out developer.key 2048

# Criando uma requisição da assinatura do certificado
openssl req -new -key developer.key -out developer.csr -subj "/CN=developer"

# gerando um base64 do developer.csr "tr -d '\n'" tira a quebra de linha
# Pedido de assinatura do certificado convertido em base64
cat developer.csr | base64 | tr -d '\n'

# Criando o arquivo develop.yaml,  adiciona o developer.csr em base64

# consultar o certificado
kubectl get csr
# Aprovando o certificado
kubectl certificate approve developer

# Pegando o certificado "crt" em base64
kubectl get csr developer -o jsonpath='{.status.certificate}' | base64 -d > developer.crt