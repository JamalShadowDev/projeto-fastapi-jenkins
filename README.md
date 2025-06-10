# 🚀 Projeto DevOps - FastAPI + Jenkins + Kubernetes

> **Deploy automatizado de API com FastAPI, Jenkins e Kubernetes**  
> Projeto desenvolvido como parte do programa de estágio DevSecOps na **CompassUOL**

## 📋 Sobre o Projeto

Este projeto tem como objetivo ensinar na prática os conceitos de **CI/CD** utilizando tecnologias modernas de DevOps. Desenvolvemos uma esteira de automação completa que realiza o deploy automatizado de uma aplicação FastAPI em um cluster Kubernetes local.

### 🎯 Objetivos de Aprendizado
- Implementar pipeline CI/CD com Jenkins
- Containerização com Docker
- Deploy automatizado no Kubernetes
- Integração com GitHub e Docker Hub
- Práticas de DevSecOps

---

## 🛠️ Tecnologias Utilizadas

- **Python 3.9+** - Backend API
- **FastAPI** - Framework Web
- **Docker** - Containerização
- **Kubernetes** - Orquestração de containers
- **Jenkins** - CI/CD Pipeline
- **GitHub** - Versionamento de código
- **Docker Hub** - Registro de imagens

---

## 📁 Estrutura do Projeto

```
projeto-devops-fastapi-jenkins/
├── 📂 backend/                 # API FastAPI
│   ├── 🐍 main.py             # Código principal da API
│   ├── 📦 requirements.txt    # Dependências Python
│   └── 🐳 Dockerfile          # Imagem Docker
├── 📂 frontend/               # Frontend (em desenvolvimento)
├── 📂 docs/                   # Documentação
├── 📂 k8s/                    # Manifests Kubernetes (será criado)
├── 📄 README.md               # Este arquivo
└── 📄 .gitignore             # Arquivos ignorados pelo Git
```

---

## 🚀 API FastAPI - Endpoints Disponíveis

A API possui **6 endpoints** funcionais para demonstração:

### 📚 Documentação Interativa
```
GET /docs
```
Interface Swagger para testar todos os endpoints

### 🎨 Endpoints da API

- **GET /color** - Retorna cor hexadecimal aleatória
  - Resposta: `{"color": "#FF5733"}`

- **GET /cat** - URL de imagem de gato aleatória  
  - Resposta: `{"cat_image_url": "https://..."}`

- **GET /random-photo** - URL de foto aleatória (Picsum)
  - Resposta: `{"random_photo_url": "https://..."}`

- **GET /time** - Horário atual do servidor
  - Resposta: `{"current_time": "2025-06-10 15:30:45"}`

- **GET /scare** - URL de GIF de susto
  - Resposta: `{"scare_image_url": "https://..."}`

- **GET /lookalike** - URL de avatar aleatório
  - Resposta: `{"lookalike_image_url": "https://..."}`

---

## 🏗️ Roadmap do Projeto

### ✅ Fase 1: Preparação do Projeto (CONCLUÍDA)
- [x] Repositório GitHub criado
- [x] Código FastAPI funcionando localmente
- [x] Python e dependências configurados
- [x] Branches `main` (produção) e `dev` (desenvolvimento) criadas
- [x] Todos os endpoints testados e funcionais

### 🔄 Fase 2: Conteinerização com Docker (EM ANDAMENTO)
- [ ] Dockerfile criado e testado
- [ ] Build da imagem Docker local
- [ ] Push da imagem para Docker Hub
- [ ] Testes de container funcionando

### ⏳ Fase 3: Deploy no Kubernetes
- [ ] Manifests de Deployment criados
- [ ] Service do Kubernetes configurado
- [ ] Aplicação exposta via NodePort
- [ ] Testes no cluster local

### ⏳ Fase 4: Pipeline Jenkins - Build & Push
- [ ] Pipeline Jenkins configurada
- [ ] Stage de build implementado
- [ ] Stage de push para Docker Hub
- [ ] Trigger automático via webhook GitHub

### ⏳ Fase 5: Pipeline Jenkins - Deploy
- [ ] Jenkins com acesso ao kubectl
- [ ] Stage de deploy no Kubernetes
- [ ] Pipeline completa funcionando
- [ ] Testes end-to-end

### ⏳ Fase 6: Documentação Final
- [ ] README completo com screenshots
- [ ] Documentação de reprodução
- [ ] Prints da pipeline funcionando
- [ ] Apresentação final

---

## 🚦 Como Executar Localmente

### Pré-requisitos
- Python 3.9+
- Docker
- Kubernetes local (Kind/Minikube/Docker Desktop)
- Git

### 🐍 Executar com Python

```bash
# 1. Clonar repositório
git clone https://github.com/SEU_USERNAME/projeto-devops-fastapi-jenkins.git
cd projeto-devops-fastapi-jenkins

# 2. Navegar para backend
cd backend

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Executar aplicação
uvicorn main:app --reload
```

**Acesse**: `http://localhost:8000/docs`

### 🐳 Executar com Docker

```bash
# 1. Build da imagem
cd backend
docker build -t fastapi-app .

# 2. Executar container
docker run -p 8000:8000 fastapi-app
```

**Acesse**: `http://localhost:8000/docs`

---

## 🧪 Testes Realizados

### ✅ Testes Locais Concluídos

```bash
# Logs de sucesso dos endpoints testados:
INFO: 127.0.0.1:50116 - "GET /time HTTP/1.1" 200 OK
INFO: 127.0.0.1:50117 - "GET /docs HTTP/1.1" 200 OK
INFO: 127.0.0.1:50120 - "GET /color HTTP/1.1" 200 OK
INFO: 127.0.0.1:50135 - "GET /cat HTTP/1.1" 200 OK
INFO: 127.0.0.1:50137 - "GET /random-photo HTTP/1.1" 200 OK
INFO: 127.0.0.1:50153 - "GET /scare HTTP/1.1" 200 OK
INFO: 127.0.0.1:50154 - "GET /lookalike HTTP/1.1" 200 OK
```

**Status**: ✅ Todos os endpoints funcionando perfeitamente!

---

## 🎯 Desafios Extras (Planejados)

- [ ] **Scanner de Vulnerabilidades**: Integração com Trivy
- [ ] **Notificações**: Webhook Slack/Discord para deploys
- [ ] **Análise SAST**: Integração com SonarQube
- [ ] **Helm Charts**: Deploy via Helm no Kubernetes

---

## 👥 Desenvolvido por

**Marcos (Jamal)** - Estagiário DevSecOps na CompassUOL  
Curso: Análise e Desenvolvimento de Sistemas + Técnico em Automação Industrial

---

## 📄 Licença

Este projeto está licenciado sob a **MIT License** - sinta-se livre para usar, modificar e distribuir.

---

<div align="center">

**🚀 Projeto em desenvolvimento - Acompanhe o progresso! 🚀**

Status: Fase 1 Concluída | Pipeline: Em Desenvolvimento | Docker: Ready

</div>