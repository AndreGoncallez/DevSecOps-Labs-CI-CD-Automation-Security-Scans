🔐 DevSecOps Labs – CI/CD · Automation · Security Scans




Repositório de laboratórios práticos para integrar segurança ao ciclo de vida de software e infraestrutura: pipelines CI/CD, automação (IaC), varreduras de segurança (SAST/DAST/Dependency) e integrações com Google Cloud.

📚 Sumário

Objetivo

Stack Tecnológica

Níveis de Laboratórios

Estrutura do Repositório

Guia Rápido (Quickstart)

Pipelines CI/CD

Varreduras de Segurança

Integração com Google Cloud

Roadmap

Boas Práticas

Contribuição

Licença

🎯 Objetivo

Consolidar conhecimentos em Cloud Security + DevOps + Cibersegurança, com foco em implementação prática. Este repositório foi desenhado para ser didático (ensino) e profissional (pronto para produção em ambientes de laboratório).

Trilha relacionada: Cisco CCNA · Fortinet FCP/FCSS · Google ACE · Google Professional Cloud Security Engineer · Pós-graduação em Cibersegurança e Governança de Dados (PUC Minas).

🛠️ Stack Tecnológica

IaC: Terraform · Ansible

Contêineres & Orquestração: Docker · Kubernetes

CI/CD: GitHub Actions (padrão) · GitLab CI (exemplos)

Segurança: Trivy · SonarQube · OWASP ZAP · Snyk

Cloud: Google Cloud Platform (GCP)

Ajuste a stack conforme seu cenário. Os exemplos funcionam isoladamente em Docker e podem ser integrados ao GCP.

🎓 Níveis de Laboratórios

Nível 1 – Fundamentos: pipelines simples, SAST e dependency scan no push.

Nível 2 – Intermediário: imagens Docker, varredura de contêiner, relatórios e gates de qualidade.

Nível 3 – Avançado: DAST, deploy controlado, IaC com Terraform e segurança em ambientes Kubernetes/GCP.

📂 Estrutura do Repositório
├── .github/
│   └── workflows/
│       └── ci.yml              # Pipeline CI/CD padrão (GitHub Actions)
├── infra/                      # IaC (Terraform/Ansible)
├── pipeline/                   # Configs e exemplos de CI/CD (GitHub/GitLab)
├── scans/                      # Relatórios de segurança (SAST/DAST/Dependency)
├── src/                        # Código de exemplo (apps/containers)
├── docs/                       # Guias e referências
└── README.md
⚡ Guia Rápido (Quickstart)
1) Pré-requisitos

Docker e Docker Compose instalados

Git instalado

(Opcional) Conta GCP e gcloud se for testar nuvem

2) Clonar o repositório
git clone https://github.com/AndreGoncallez/DevSecOps-Labs-CI-CD-Automation-Security-Scans.git
cd DevSecOps-Labs-CI-CD-Automation-Security-Scans
3) Subir stack local de ferramentas (ex.: Sonar + ZAP Proxy) (opcional)
# Exemplo (se houver um docker-compose.yml na raiz ou em ./pipeline/examples/)
docker compose -f pipeline/examples/devsecops-stack.compose.yml up -d
4) Executar um scan local com Trivy
# Varredura no sistema de arquivos do projeto
trivy fs .


# Varredura de imagem (após build)
docker build -t devsecops-lab:latest .
trivy image devsecops-lab:latest
🏗️ Pipelines CI/CD
GitHub Actions (arquivo: .github/workflows/ci.yml)

Copie este workflow para iniciar com build + testes + SAST + dependency scan.

name: CI


on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]


jobs:
  build-and-scan:
    runs-on: ubuntu-latest


    steps:
      - name: Checkout
        uses: actions/checkout@v4


      - name: Setup Python (exemplo)
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'


      - name: Install deps (exemplo)
        run: |
          pip install -r requirements.txt || true


      - name: Trivy FS Scan
        uses: aquasecurity/trivy-action@0.24.0
        with:
          scan-type: 'fs'
          ignore-unfixed: true
          format: 'sarif'
          output: 'scans/trivy-fs.sarif'


      - name: Upload Security Report (SARIF)
        uses: github/codeql-action/upload-sarif@v3
        with:
          sarif_file: scans/trivy-fs.sarif


      - name: Build Docker image
        run: |
          docker build -t ghcr.io/${{ github.repository }}:sha-${{ github.sha }} .

Para DAST (ZAP) e análise de dependências avançada, veja exemplos em pipeline/.

🛡️ Varreduras de Segurança

SAST: análise estática do código-fonte (SonarQube/Semgrep) → gates de qualidade.

Dependency Scan: vulnerabilidades em bibliotecas (Trivy/Snyk) → falha o build em CVEs críticos.

Container Scan: imagens Docker antes do deploy (Trivy) → políticas de baseline.

DAST: teste dinâmico de aplicação (OWASP ZAP) em ambiente de teste → relatórios em scans/.

Exemplos de comandos
# SAST com Semgrep (se configurado)
semgrep --config auto --error --json > scans/semgrep.json


# ZAP Baseline (DAST) – container oficial
docker run --rm -t owasp/zap2docker-stable zap-baseline.py -t http://app:8080 -r scans/zap-report.html
☁️ Integração com Google Cloud (opcional)

Autenticação

gcloud auth login
gcloud config set project <SEU_PROJECT_ID>

Infra com Terraform (exemplo em infra/terraform)

cd infra/terraform
terraform init
terraform plan
terraform apply

Deploy controlado: use gates de segurança para só publicar imagens aprovadas (Arifact Registry/GKE).

Reforce políticas: IAM mínimo necessário, escaneamento de imagens no Artifact Registry, Workload Identity no GKE, Cloud Armor e WAF quando aplicável.

🗺️ Roadmap




✅ Boas Práticas

Commits descritivos (Convencional Commits)

Padrões de branch: main (estável) · feat/* · fix/* · chore/*

Secrets sempre em Actions Secrets / Vault (nunca no repo)

Relatórios de segurança versionados em scans/ (sem dados sensíveis)

CODEOWNERS e proteção de branch (review obrigatório)

🤝 Contribuição

Contribuições são bem-vindas! Abra uma Issue ou envie um Pull Request. Para mudanças maiores, discuta primeiro via Issue.

Sugerimos adicionar um CONTRIBUTING.md e um CODE_OF_CONDUCT.md ao projeto.

📄 Licença

Este projeto está licenciado sob a MIT License. Consulte o arquivo LICENSE para mais detalhes.

Contatos & Reconhecimentos

Este repositório faz parte da jornada de estudos e práticas profissionais em DevSecOps & Cloud Security. Agradecimentos à comunidade open source e às ferramentas citadas.
