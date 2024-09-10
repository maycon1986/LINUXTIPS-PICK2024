# Instalação do chart local.
helm install <nome-release> <diretório do chart>
# Desistalar o chart
helm uninstall <nome-release>

# OBS: quote coloca a opção " "

# Verifica se tem algum erro no chart
helm lint

# Renderizando o template
helm template <nome-diretorio>

# Criando um pacote do chart
helm package charts/<nome-diretorio>

# Criando um index
helm repo index --url <link-gerado-github> .

# Gerando Link da page github
Settings -> Pages
Selecione a branch e clique em save

# Criando um repo do helm
helm repo add <nome-repo> <link-gerado-github>

# Listando os charts que temos no nosso repositorio
helm search repo <meu-repo>