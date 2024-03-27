### Passo 1
docker container run -d -p 6379:6379 --name redis redis
### Passo 2
docker container run -d -p 5000:5000 --name giropops-senhas --env REDIS_HOST="seu-ip-local" mayconcarvalho/linuxtips-giropops-senhas:1.0
