# 🚀 Projeto DevOps - FastAPI + Jenkins + Kubernetes

> **Deploy automatizado de API com FastAPI, Jenkins e Kubernetes**  
> Projeto desenvolvido como parte do programa de estágio DevSecOps na **CompassUOL**

## 📋 Sobre o Projeto

Este projeto implementa uma **pipeline CI/CD completa** utilizando tecnologias modernas de DevOps. Desenvolvemos uma esteira de automação que realiza o deploy automatizado de uma aplicação FastAPI em um cluster Kubernetes local.

### 🎯 Objetivos de Aprendizado
- ✅ Implementar pipeline CI/CD com Jenkins
- ✅ Containerização com Docker
- ✅ Deploy automatizado no Kubernetes
- ✅ Integração com GitHub e Docker Hub
- ✅ Práticas de DevSecOps

---

## 🛠️ Tecnologias Utilizadas

- **Python 3.9+** - Backend API
- **FastAPI** - Framework Web  
- **Docker** - Containerização
- **Kubernetes** - Orquestração de containers (Kind)
- **Jenkins** - CI/CD Pipeline
- **GitHub** - Versionamento de código
- **Docker Hub** - Registro de imagens

---

## 📁 Estrutura do Projeto

```
projeto-fastapi-jenkins/
├── 📂 backend/                 # API FastAPI
│   ├── 🐍 main.py             # Código principal da API
│   ├── 📦 requirements.txt    # Dependências Python
│   └── 🐳 Dockerfile          # Imagem Docker otimizada
├── 📂 k8s/                    # Manifests Kubernetes
│   └── 📄 deployment.yaml    # Deployment + Service
├── 📄 Jenkinsfile            # Pipeline CI/CD
├── 📄 README.md              # Este arquivo
└── 📄 .gitignore            # Arquivos ignorados pelo Git
```

---

## 🚀 API FastAPI - Endpoints Disponíveis

A API possui **6 endpoints** funcionais fornecidos pelos instrutores:

### 📚 Documentação Interativa
```
GET /docs
```
Interface Swagger para testar todos os endpoints - **Acessível em produção!**

### 🎨 Endpoints da API

- **GET /color** - Retorna cor hexadecimal aleatória
- **GET /cat** - URL de imagem de gato aleatória  
- **GET /random-photo** - URL de foto aleatória (Picsum)
- **GET /time** - Horário atual do servidor
- **GET /scare** - URL de GIF de susto
- **GET /lookalike** - URL de avatar aleatório

**🌐 Aplicação em Produção**: `http://localhost:30001/docs`

---

## 🏗️ Status do Projeto

### ✅ Fase 1: Preparação do Projeto (CONCLUÍDA)
- [x] Repositório GitHub criado
- [x] Código FastAPI funcionando localmente
- [x] Python e dependências configurados
- [x] Branches `main` (produção) e `dev` (desenvolvimento) criadas
- [x] Todos os endpoints testados e funcionais

### ✅ Fase 2: Containerização com Docker (CONCLUÍDA)
- [x] Dockerfile otimizado com usuário não-root
- [x] Build da imagem Docker local
- [x] Push da imagem para Docker Hub (`jamalshadowdev/fastapi-jenkins`)
- [x] Testes de container funcionando
- [x] Health checks implementados

### ✅ Fase 3: Deploy no Kubernetes (CONCLUÍDA)
- [x] Manifests de Deployment criados (2 réplicas)
- [x] Service do Kubernetes configurado (NodePort 30001)
- [x] Aplicação exposta via NodePort funcionando
- [x] Testes no cluster local (Kind) aprovados

### ✅ Fase 4: Pipeline Jenkins - Build & Push (CONCLUÍDA)
- [x] Pipeline Jenkins configurada
- [x] Stage de build implementado
- [x] Stage de push para Docker Hub
- [x] Versionamento automático com BUILD_ID

### ✅ Fase 5: Pipeline Jenkins - Deploy (CONCLUÍDA)
- [x] Jenkins com acesso ao kubectl
- [x] Stage de deploy no Kubernetes
- [x] Pipeline completa funcionando
- [x] Deploy automatizado em produção

### 🔄 Fase 6: Documentação & Webhook (EM ANDAMENTO)
- [x] README atualizado com status
- [ ] Screenshots da pipeline funcionando
- [ ] Webhook GitHub + ngrok
- [ ] Documentação de reprodução completa

---

## 🚦 Como Executar 

### 🐍 **Desenvolvimento Local**
```bash
# 1. Clonar repositório
git clone https://github.com/JamalShadowDev/projeto-fastapi-jenkins.git
cd projeto-fastapi-jenkins

# 2. Navegar para backend
cd backend

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Executar aplicação
uvicorn main:app --reload
```

### 🐳 **Container Local**
```bash
# Pull da imagem do Docker Hub
docker pull jamalshadowdev/fastapi-jenkins:latest

# Executar container
docker run -p 8000:8000 jamalshadowdev/fastapi-jenkins:latest
```

---

## 🎯 **Pipeline CI/CD Funcionando**

### 🔄 **Fluxo Automático:**
```
GitHub Push → Jenkins → Docker Build → Docker Hub → Kubernetes Deploy
```

### 📊 **Status Atual:**
- ✅ **Jenkins**: Pipeline funcionando (Build #13+)
- ✅ **Docker Hub**: `jamalshadowdev/fastapi-jenkins` (múltiplas versões)
- ✅ **Kubernetes**: 2 pods rodando com health checks
- ✅ **Aplicação**: Acessível via `localhost:30001`

---

## 🎯 Próximos Passos

### 🌐 **Webhook Automático**
- [ ] Configuração ngrok
- [ ] Webhook GitHub → Jenkins
- [ ] Pipeline 100% automática

### ⭐ **Desafios Extras (CompassUOL)**
- [ ] **Scanner de Vulnerabilidades**: Integração com Trivy
- [ ] **Notificações**: Webhook Slack/Discord para deploys
- [ ] **Análise SAST**: Integração com SonarQube
- [ ] **Helm Charts**: Deploy via Helm no Kubernetes

---

## 👥 **Créditos**

### 📚 **Código Base da API:**
Fornecido pelos instrutores da **CompassUOL** como parte do programa de estágio DevSecOps.

### 🚀 **Implementações DevOps:**
**Marcos (Jamal)** - Estagiário DevSecOps na CompassUOL  
- Pipeline CI/CD completa
- Containerização otimizada
- Deploy automatizado Kubernetes
- Práticas de segurança DevSecOps

---

## 📄 Licença

Este projeto está licenciado sob a **MIT License** - sinta-se livre para usar, modificar e distribuir.

---

<div align="center">

**🚀 PIPELINE CI/CD FUNCIONANDO EM PRODUÇÃO! 🚀**

Status: ✅ Todas as 5 Fases Concluídas | 🌐 App: localhost:30001 | 💪 Chuck Norris Approved

</div>