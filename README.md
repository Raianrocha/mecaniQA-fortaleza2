# mecaniQA-fortaleza2
Isolamento e containerização da API Java, MySQL e Redis para a MecâniQA Tech.

#Equipe#

Joaqson Rodrigues Miranda;

Lucas Santos Oliveira;

Manoel Souza Santos;

Monique Prado Pereira Gomes;

Raian Rocha Santos;

## Ambiente Docker

Suba a API Java, o MySQL e o Redis com um único comando:

```bash
docker compose up -d --build
```

Confira o estado dos serviços e os healthchecks:

```bash
docker compose ps
docker compose exec api getent hosts mysql redis
docker compose exec mysql mysqladmin ping -h mysql -uroot -proot
docker compose exec redis redis-cli ping
```

O MySQL persiste os dados no volume `mysql_data` e o Redis no volume `redis_data`.
Os serviços se comunicam pela rede interna `mecaniqa`; a API deve usar `mysql:3306` e `redis:6379` como hosts dos serviços.

## Kubernetes

Os manifestos da pasta `k8s/` realizam a implantação da API Java, MySQL e Redis no Kubernetes.

Para verificar os recursos em execução:

```bash
kubectl get pods
kubectl get services
```

## Terraform

A pasta `terraform/` contém a configuração inicial de provisionamento da infraestrutura utilizando Terraform.

O Terraform utiliza o provider Kubernetes para criar e gerenciar o namespace `mecaniqa` no cluster.

Para inicializar e validar a configuração:

```bash
cd terraform
terraform init
terraform validate
terraform plan
```

Para aplicar a configuração:

```bash
terraform apply
```

Após a aplicação, o namespace pode ser verificado com:

```bash
kubectl get namespaces
```
