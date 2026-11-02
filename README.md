# Laboratório Docker - Unidade 3

## Comandos Executados

### 1. Construção das Imagens
docker build -t devops-webapi:1.0.0 .
docker build -t devops-webapi:1.1.0 .
docker build -t devops-webapi:1.2.0 .

### 2. Validação e Testes em Staging
docker run -d --name devops-api-staging -p 8081:8080 -e APP_ENVIRONMENT=staging -e APP_VERSION=1.1.0 devops-webapi:1.1.0
curl.exe -f http://localhost:8081/health

### 3. Falha Controlada e Rollback
# Teste da versão 1.2.0 com falha (HTTP 500)
docker run -d --name devops-api-prod -p 8082:8080 -e APP_ENVIRONMENT=production -e APP_VERSION=1.2.0 devops-webapi:1.2.0

# Rollback para a versão 1.1.0
docker rm -f devops-api-prod
docker run -d --name devops-api-prod -p 8082:8080 -e APP_ENVIRONMENT=production -e APP_VERSION=1.1.0 devops-webapi:1.1.0

### 4. Execução via Docker Compose
docker compose up -d
docker compose ps
