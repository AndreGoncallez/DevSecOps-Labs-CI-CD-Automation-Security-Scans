# 🚀 Imersão DevOps - Alura + Google Cloud

> _API desenvolvida com **FastAPI** para gerenciar alunos, cursos e matrículas em uma instituição de ensino._

---

## ⚙️ Pré-requisitos

Antes de iniciar, verifique se os seguintes componentes estão instalados:

- 🐍 [Python 3.10+](https://www.python.org/downloads/)
- 🔧 [Git](https://git-scm.com/downloads)
- 🐳 [Docker](https://www.docker.com/get-started)

---

## 🧱 Como Subir o Projeto Localmente

### 📥 1. Baixe o Repositório

[⬇️ Clique aqui para baixar o projeto ZIP](https://github.com/guilhermeonrails/imersao-devops/archive/refs/heads/main.zip)

---

### 🛠 2. Crie um Ambiente Virtual

```bash
python3 -m venv ./venv
```

---

### ⚡ 3. Ative o Ambiente Virtual

- **Linux/Mac:**
  ```bash
  source venv/bin/activate
  ```

- **Windows:**
  > Execute o terminal como administrador:
  ```bash
  Set-ExecutionPolicy RemoteSigned
  venv\Scripts\activate
  ```

---

### 📦 4. Instale as Dependências

```bash
pip install -r requirements.txt
```

---

### ▶️ 5. Execute a Aplicação

```bash
uvicorn app:app --reload
```

---

### 🌐 6. Acesse a Documentação Interativa

Abra no navegador:  
👉 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

Você poderá testar todos os endpoints da API diretamente pelo Swagger UI.

---

## ☁️ Autenticação com Google Cloud

Para realizar o deploy com Google Cloud Run:

```bash
gcloud auth login
gcloud config set project PROJECT_ID
gcloud run deploy --port=8000
```

---

## 🧬 Estrutura do Projeto

📁 Organização dos arquivos:

- `app.py` → Aplicação principal FastAPI  
- `models.py` → Modelos ORM (SQLAlchemy)  
- `schemas.py` → Schemas de validação (Pydantic)  
- `database.py` → Configuração SQLite  
- `routers/` → Rotas separadas (alunos, cursos, matrículas)  
- `requirements.txt` → Dependências

📝 O banco de dados será criado automaticamente como `escola.db`.

> ⚠️ **Atenção:** Ao excluir o arquivo `escola.db`, todos os dados serão perdidos.

---

## 🎥 Sugestão de GIFs para ilustrar seções

Você pode substituir os emojis por GIFs temáticos (para um estilo mais sci-fi ou tech). Exemplos:

- **Deploy / Cloud**  


- **Instalação / Setup**  
  

- **API Testing**  
 

---
