# ocp-virt-stress-test
Repo for Scripts used on OCP-Virt Stress Test

## Requisitos
Maquina com podman para buildar o container

## Criando a imagem
```
git clone https://github.com/LucianoRed/ocp-virt-stress-test.git
cd ocp-virt-stress-test/ansible
podman build -t ocp-virt-stress-test .
podman tag ocp-virt-stress-test seuregistry/ocp-virt-stress-test
podman push seuregistry/ocp-virt-stress-test
```
## Deployment OpenShift

1 - Anote o endereço da API do seu OpenShift e gere o token para conexao

<img width="1508" alt="image" src="https://github.com/user-attachments/assets/1d840b40-148e-405a-bd3a-34a96cf8cc03">

<img width="1508" alt="image" src="https://github.com/user-attachments/assets/e5c810fd-42ec-4c2c-96f2-70abb26d3431">

2 - Faca o deployment da aplicacao no OpenShift

```
oc new-project ocp-virt-stress-test
oc new-app quay.io/ricardi/ocp-virt-stress-test -e "K8S_AUTH_API_KEY=<api key>" -e "K8S_AUTH_HOST=<host api>" -e "HOME=/ansible"
oc get pods
oc rsh <pod>
cd /ansible
```

## Uso
Dentro do pod, pode editar os arquivos ou mudar as variaveis ao chamar o comando ansible-playbook.

### Criar VMs
```
ansible-playbook -e "numero_de_vms=4" -e "namespace=abc123" -e "vm_password=Hs9Vkd9a" cria_vms.yaml
```

### Gera Inventario e Instala stress tool (pre-req para todos os comandos a seguir)
```
ansible-playbook -e "namespace=abc123" gera_inventario.yaml
ansible-playbook -i inventario.ini -e "namespace=abc123" instala_stress.yaml
```

### Executa testes de Stress CPU e Memoria
```
ansible-playbook -e "namespace=abc123" -i inventario.ini 
ansible-playbook -i inventario.ini -e "namespace=abc123" stress_cpu.yaml
ansible-playbook -i inventario.ini -e "namespace=abc123" stress_memoria.yaml
```


### Destruir VMs
```
ansible-playbook -e "namespace=abc123 destroi_vms.yaml" 
```


