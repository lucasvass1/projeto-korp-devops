# Projeto Korp DevOps Challenge

## 📖 Sobre o Projeto

Este projeto foi desenvolvido como solução para um desafio técnico com foco em práticas de DevOps, observabilidade e automação de infraestrutura.

A solução consiste em uma aplicação HTTP desenvolvida em Go, containerizada com Docker e orquestrada via Docker Compose. A infraestrutura utiliza NGINX como Reverse Proxy, Prometheus para coleta de métricas, Grafana para visualização e Ansible para automação do provisionamento.

---

## 🚀 Tecnologias Utilizadas

* Go (Golang)
* Docker
* Docker Compose
* NGINX
* Prometheus
* Grafana
* Ansible
* Ubuntu / WSL2

---

## 🏗️ Arquitetura da Solução

```text
Cliente
   │
   ▼
NGINX (Reverse Proxy)
   │
   ▼
Aplicação Go
   │
   ├── /projeto-korp
   │
   └── /metrics
           │
           ▼
      Prometheus
           │
           ▼
        Grafana
```

---

## 📂 Estrutura do Projeto

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
├── docs/
│   └── images/
│
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Funcionalidades

### Endpoint Principal

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

### Endpoint de Métricas

```http
GET /metrics
```

Métrica customizada:

```text
http_requests_total
```

---

## 🐳 Containers

| Serviço        | Função                       |
| -------------- | ---------------------------- |
| Go Application | API principal                |
| NGINX          | Reverse Proxy                |
| Prometheus     | Coleta de métricas           |
| Grafana        | Visualização e monitoramento |

---

## ▶️ Executando o Projeto

### Subir ambiente

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

## 🤖 Automação com Ansible

Executar o provisionamento:

```bash
cd ansible

ansible-playbook -i inventory.ini playbook.yml
```

O playbook realiza:

* Verificação do Docker
* Instalação do Docker (via role)
* Criação da rede Docker
* Build da aplicação
* Inicialização dos containers
* Validação automática da API

---

## 📊 Observabilidade

### Prometheus

Disponível em:

```text
http://localhost:9090
```

### Grafana

Disponível em:

```text
http://localhost:3000
```

Datasource Prometheus provisionado automaticamente.

---

## 🔗 Endpoints

### API

```text
http://localhost/projeto-korp
```

### Métricas

```text
http://localhost/metrics
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

## 🧪 Como Testar

### Validar API

```bash
curl http://localhost/projeto-korp
```

### Validar Métricas

```bash
curl http://localhost/metrics
```

### Gerar Requisições

```bash
for i in {1..20}; do
  curl http://localhost/projeto-korp
done
```

Após isso, visualize as métricas no Prometheus e Grafana.

---

## 📸 Evidências da Execução

### Containers em execução

Screenshot de:

```bash
docker ps
```

Imagem:

```text
docs/images/docker-ps.png
```

---

### Endpoint da aplicação

Screenshot de:

```bash
curl http://localhost/projeto-korp
```

Imagem:

```text
docs/images/api-response.png
```

---

### Targets do Prometheus

Screenshot da página:

```text
http://localhost:9090/targets
```

Com o target da aplicação em estado **UP**.

Imagem:

```text
docs/images/prometheus-targets.png
```

---

### Dashboard Grafana

Screenshot dos gráficos e métricas.

Imagem:

```text
docs/images/grafana-dashboard.png
```

---

### Execução do Playbook Ansible

Screenshot da execução:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

Mostrando o resultado final:

```text
PLAY RECAP
```

Imagem:

```text
docs/images/ansible-playbook.png
```

---

## ✅ Requisitos Atendidos

### Serviço e Infraestrutura

* [x] Servidor HTTP em Go
* [x] Endpoint `/projeto-korp`
* [x] Resposta JSON
* [x] Dockerização da aplicação
* [x] Docker Compose
* [x] Reverse Proxy com NGINX

### Observabilidade

* [x] Endpoint `/metrics`
* [x] Métrica customizada `http_requests_total`
* [x] Integração com Prometheus
* [x] Integração com Grafana

### Automação

* [x] Provisionamento com Ansible
* [x] Instalação do Docker via Ansible
* [x] Criação automática da rede Docker
* [x] Inicialização dos containers
* [x] Validação automática da aplicação

### Bônus

* [x] Datasource Prometheus provisionado automaticamente
* [x] Estrutura preparada para provisionamento de dashboards Grafana

---

## 👨‍💻 Autor

Lucas Vasconcelos

Desenvolvedor Full Stack | React | Node.js | TypeScript | AWS

Projeto desenvolvido como solução para desafio técnico DevOps, demonstrando conhecimentos em automação, conteinerização, observabilidade e infraestrutura.
