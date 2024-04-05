### Passo 1 - Criando network
docker network create network-lab

# Passo 2 - Executar container do redis
docker container run -d --name redis --network network-lab redis
docker container run -d -p 6379:6379 --name redis --network network-lab redis


# Passo 3 - Executar container do giropops senhas

docker container run -d -p 5000:5000 --name giropops-senhas --env REDIS_HOST=redis --network network-lab mayconcarvalho/linuxtips-giropops-senhas:1.0

# Passo 4 - Remover o ambiente
docker container rm -f giropops-senhas redis
docker image rm -f <IMAGE ID REDIS> <IMAGE ID GIROPOPS-SENHA>