# Projeto Korp DevOps Challenge

## Sobre o Projeto

Este projeto foi desenvolvido como solução para um desafio técnico de estágio DevOps.

A aplicação consiste em um servidor HTTP desenvolvido em Go, containerizado com Docker e orquestrado através do Docker Compose. A infraestrutura conta com NGINX como reverse proxy, Prometheus para coleta de métricas, Grafana para observabilidade e Ansible para automação do provisionamento do ambiente.

O objetivo é demonstrar conhecimentos em desenvolvimento backend, conteinerização, monitoramento e automação de infraestrutura.

---

## Arquitetura da Solução

```text
Cliente
   |
   v
NGINX (Reverse Proxy)
   |
   v
Aplicação Go
   |
   +----> Endpoint de Métricas (/metrics)
                |
                v
          Prometheus
                |
                v
            Grafana
```

---

## Tecnologias Utilizadas

* Go (Golang)
* Docker
* Docker Compose
* NGINX
* Prometheus
* Grafana
* Ansible
* Ubuntu (WSL2)

---

## Estrutura do Projeto

```text
projeto-korp-devops/
│
├── app/
│   ├── main.go
│   ├── go.mod
│   └── Dockerfile
│
├── nginx/
│   └── http-server-projeto-korp.conf
│
├── prometheus/
│   └── prometheus.yml
│
├── grafana/
│   ├── dashboards/
│   └── provisioning/
│       ├── dashboards/
│       └── datasources/
│
├── ansible/
│   ├── inventory.ini
│   ├── playbook.yml
│   └── roles/
│       └── docker/
│
├── docker-compose.yml
└── README.md
```

---

## Funcionalidades

### Aplicação HTTP

Endpoint principal:

```http
GET /projeto-korp
```

Resposta:

```json
{
  "nome": "Projeto Korp",
  "horario": "2026-06-14T14:11:27Z"
}
```

### Métricas

Endpoint:

```http
GET /metrics
```

Métrica customizada:

```text
http_requests_total
```

Responsável por contabilizar todas as requisições realizadas na aplicação.

---

## Containers

### Aplicação Go

Responsável por disponibilizar a API HTTP e expor métricas Prometheus.

### NGINX

Atua como Reverse Proxy da aplicação.

### Prometheus

Realiza coleta periódica das métricas expostas pela aplicação.

### Grafana

Responsável pela visualização das métricas e dashboards de monitoramento.

---

## Executando com Docker Compose

### Build e inicialização

```bash
docker compose up --build -d
```

### Verificar containers

```bash
docker ps
```

### Derrubar ambiente

```bash
docker compose down
```

---

## Provisionamento com Ansible

O projeto possui automação para provisionamento da infraestrutura utilizando Ansible.

### Executar playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

O playbook realiza:

* Verificação do Docker
* Criação da rede Docker
* Build da aplicação
* Subida dos containers
* Validação da API
* Exibição da resposta do endpoint

---

## Endpoints Disponíveis

### API

```text
http://localhost/projeto-korp
```

### Prometheus

```text
http://localhost:9090
```

### Grafana

```text
http://localhost:3000
```

---

## Monitoramento

O Prometheus realiza o scrape das métricas da aplicação.

Exemplo de métrica:

```text
http_requests_total
```

No Grafana é possível visualizar:

* Total de requisições
* Taxa de requisições por segundo
* Evolução temporal das métricas

---

## Requisitos Atendidos

### Parte 1 — Serviço e Infraestrutura

* Servidor HTTP em Go
* Endpoint `/projeto-korp`
* Retorno em JSON
* Dockerização da aplicação
* Docker Compose
* Reverse Proxy com NGINX

### Parte 2 — Observabilidade

* Endpoint `/metrics`
* Integração com Prometheus
* Coleta de métricas customizadas
* Dashboard Grafana

### Parte 3 — Automação

* Provisionamento via Ansible
* Criação de rede Docker
* Inicialização automatizada do ambiente
* Validação automática da aplicação

### Bônus

* Provisionamento automático de datasource Grafana
* Estrutura preparada para provisionamento automático de dashboards

---

## Como Testar

### Validar API

```bash
curl http://localhost/projeto-korp
```

### Validar métricas

```bash
curl http://localhost/metrics
```

### Gerar tráfego

```bash
for i in {1..20}; do
  curl http://localhost/projeto-korp
done
```

Após gerar tráfego, acessar Grafana para visualizar as métricas.

---

## Autor

Lucas Vasconcelos

Desenvolvedor Full Stack | React | Node.js | TypeScript | AWS

Projeto desenvolvido para fins de avaliação técnica e demonstração de conhecimentos em DevOps, automação e observabilidade.
