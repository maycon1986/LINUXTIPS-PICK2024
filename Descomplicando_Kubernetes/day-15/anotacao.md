# taints

## NoExecute
# No modo NoExecute para ninguem executar nele
kubectl taint node <nome do nó> manutencao=true:NoExecute
# Tirando do modo NoExecute "Adicione o - no final"
kubectl taint node <nome do nó> manutencao=true:NoExecute-


## NoSchedule
# No modo NoSchedule, nada novo vai ser schedulado para o nó
kubectl taint node <nome do nó> manutencao=true:NoSchedule
# Tirando do modo NoSchedule "Adicione o - no final"
kubectl taint node <nome do nó> manutencao=true:NoSchedule-


## Tolerations deixa os deployments que tem essa configuração abaixo tambem adicionar nos nó com a taints NoSchedule
      tolerations:
      - key: "gpu"
        operator: "Equal"
        value: "true"
        effect: "NoSchedule"


# OBS: por padrão o kubernetes não vai redistribuir depois que tirou o nó de NoExecute. Para evitar que toda hora ele fique mudando.
# Uma alternativa para redistribuir o pod é executar o comando:
kubectl rollout restart deployment <nome do deployment>

