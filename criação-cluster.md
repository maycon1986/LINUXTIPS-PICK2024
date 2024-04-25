## SO Debian Linux 11

## Portas entre os nodes
|  Portas     | Serviços          |
|  :--------- | :---------------- |
| `6443(TCP)` | `KUBE APISERVER`  |
| `10250(TCP)`| `KUBELET`         |
| `10251(TCP)`| `KUBE SCHEDULLER` |
| `10252(TCP)`| `KUBE CONTROLLER` |

## Preparando o cluster "Os passos abaixo será realizado em todas as VMs #####
#### OBS: Sempre desligue a Swap
```bash
sudo swapoff -a
sudo apt update
sudo apt install apt-transport-https curl -y
```
#### Requisitos para o containerD
`sudo apt install gnupg lsb-release ca-certificates gpg-y`

## Repositorio do kubernetes (kubeadm, kubectl, kubelet)
```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

## Instalando dos pacotes
```bash
sudo apt update
sudo apt install -y kubeadm kubeclt kubelet
```
#### OBS: O comando abaixo é para não deixar os pacotes atualizar automaticamente.
```bash
sudo apt-mark hold kubelet kubeadm kubectl
sudo systemctl enable --now kubelet
```

## Crie um arquivo para ativar os modulos na inicialiação das vms do cluster.
`sudo vim /etc/modules-load.d/k8s.conf`
overlay # Para rede
br_netfilter # Para o firewall da rede

## Carregue os modulos 
```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```

## Parametrização do sistema
`sudo vim /etc/sysctl.d/k8s.conf`
`net.bridge.bridge-nf-call-iptables = 1 # Para habilitar o brigde`

`net.bridge.bridge-nf-call-ip6tables = 1 # Para habilitar o brigde`

`net.ipv4.ip_forward = 1 # Habilidade de fazer o repasse dos pacotes`

#### Reload no system
`sudo sysctl --system`

## Instalando o container runtime "ContainerD
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
echo "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" |sudo tee /etc/apt/sources.list.d/docker.list
sudo apt update
sudo apt install containerd -y
```

#### Configurando o containerD
#### Importando as configuração do containerD para o arquivo config.toml
`sudo containerd config default | sudo tee /etc/containerd/config.toml`

#### Ajuste no arquivo config.toml
`sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/g' /etc/containerd/config.toml`

#### Restart o serviço
```bash
sudo systemctl restart containerd.service
sudo systemctl enable containerd.service
```

## Iniciando o Cluster

## Configurando controlplane "Rodar somente o controlplane"
`sudo kubeadm init --pod-network-cidr=10.10.0.0/16 --apiserver-advertise-address=<ip-controlplane>`

#### OBS: Finalizando a inicialição, execute o comando que ele ira  mostrar e coloque na linha de comando.
#### OBS: Os certificados esta localizado no diretório /etc/kubernetes/pki/
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
#### Comando abaixo é para resetar as configurações do comando acima, utillizar caso necessario.
`kubeadm reset`

## Migrar os nodes no controlplane "Comando abaixo aparece quando executa o kubeadm init" Executar somente nos workers.
`sudo kubeadm join <ip-controlplane:6443> --token <token> --discovery-token-ca-cert-hash  sha256:<hash>`

## Instalando o plugin de rede para resolver a comunicação entres os pods "Instalando o Weave Net"
#### CNI: Container Network interface
`kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml`

# Liberar as portas do Wave Net
|  Portas          |
|  :-------------- |
| `6784(TCP)`      |
| `6783-6784(UDP)` |
