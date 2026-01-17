### 🚀 Guia de Instalação: n8n + Evolution API + Redis

Este repositório automatiza a implantação de uma infraestrutura completa de automação utilizando containers Docker.

---------------------------------------------------------------------------------
### 1. Pré-requisitos
   
Antes de iniciar, garanta que seu ambiente possui as ferramentas base instaladas:

💻 **Visual Studio Code**: https://code.visualstudo.com/

🐳 **Docker Desktop**: https://www.docker.com/get-started/

🧰 **Git** instalado: https://git-scm.com/install/ 
(ou baixe o ZIP do repositório)

---------------------------------------------------------------------------------
### 2. CLONAR O PROJETO

Use Git (via terminal) ou baixe o ZIP.

```bash
# via git (recomendado)
git clone https://github.com/rgvieiraoficial/n8n-evo-docker-starter
cd n8n-evo-docker-starter

# ou baixe o ZIP pelo GitHub: Code > Download ZIP, extraia e abra o terminal na pasta do projeto.
```

<img width="556" height="257" alt="image" src="https://github.com/user-attachments/assets/9e8ec380-a27b-433e-aa7e-cbc86754cfa8" />

---------------------------------------------------------------------------------
### 3. CONFIGURAÇÃO DO env.

### 3.1 RENOMEIE O ARQ ENV.
Este projeto contém o arquivo .env.example, que define as variáveis de ambiente necessárias para o funcionamento dos serviços.
Copie ou renomeie esse arquivo para .env e ajuste os valores conforme sua necessidade.

```bash
cp .env.example .env
# no Windows PowerShell, você pode usar:
copy .env.example .env
```
<img width="587" height="299" alt="image" src="https://github.com/user-attachments/assets/ae57f9dc-3e23-4dbd-8459-e6db9a5b83ea" />

### 3.2 ABRA OS ARQUIVOS NO VISUAL STUDIO CODE

<img width="782" height="422" alt="image" src="https://github.com/user-attachments/assets/07364e30-23a2-4e8e-9136-e0a7701b86e6" />
<img width="920" height="458" alt="image" src="https://github.com/user-attachments/assets/58b57d83-c02e-4035-875f-05a95b09f8e6" />


### 3.3 ALTERE O  `AUTHENTICATION_API_KEY`

**IMPORTANTE**: altere preferencialmente a variável `AUTHENTICATION_API_KEY` (Evolution API) para um valor seguro.
*Revise* também timezone e demais variáveis (ex.: `TZ`, `GENERIC_TIMEZONE`, configs de Postgres e Redis) conforme seu ambiente.


<img width="1175" height="727" alt="image" src="https://github.com/user-attachments/assets/f40c8c26-dbaa-408c-ae48-65e902dd4534" />


**Obs**: Nova API pode ser gerada em qualquer gerador de API KEY global. É só digitar no google `GLOBAL API key generator`

---------------------------------------------------------------------------------
### 4. Inicializar toda a infraestrutura (SUBIR O STACK)

Com o Docker em execução e já dentro da pasta do projeto:

```bash
docker compose up -d
```
<img width="755" height="396" alt="image" src="https://github.com/user-attachments/assets/1a372b3b-7826-4c16-8ca7-42abfdcced50" />

Isso criará e iniciará os serviços definidos em `docker-compose.yaml`.

---------------------------------------------------------------------------------
### 5. Serviços e acessos



---------------------------------------------------------------------------------
Criado por: Filipe Amorim

Minhas Redes Sociais

LinkedIn: https://www.linkedin.com/in/filipe-amorim/

GitHub: https://github.com/filipe-amorim

Licença: 
Use e adapte livremente conforme suas necessidades.
