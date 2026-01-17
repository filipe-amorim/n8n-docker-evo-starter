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

Após instalação deverá aparecer tudo funcionando no docker

<img width="1903" height="473" alt="image" src="https://github.com/user-attachments/assets/bbd2d00c-24fc-400a-aaa2-e7cc97266615" />


---------------------------------------------------------------------------------
### 5. Serviços e acessos

- **n8n**: `http://localhost:5678`

<img width="775" height="599" alt="image" src="https://github.com/user-attachments/assets/e9930f7a-2f54-4449-97dc-7c61be956704" />

- **Evolution API**: `http://localhost:8080/manager/`
Observação: os serviços também se comunicam entre si via a rede interna `evolution_n8n_net` do Docker.

<img width="380" height="220" alt="image" src="https://github.com/user-attachments/assets/df46862d-f3b1-460f-adb1-47fd6898bfc7" />

<img width="955" height="226" alt="image" src="https://github.com/user-attachments/assets/c3fc246c-052f-4879-8e9d-96c1dc8a01bd" />


Ao integrar serviços no Docker, utilize os nomes dos serviços definidos no docker-compose (DNS interno do Docker).
Não utilize localhost, pois ele referencia apenas o container atual, e não os demais serviços da stack.

---------------------------------------------------------------------------------
### 6.Credenciais

### Evolution API no n8n
Use http://evolution-api:8080 como valor para o campo "Server Url" no momento de criar uma credencial da Evolution API no n8n.

<img width="1334" height="781" alt="image" src="https://github.com/user-attachments/assets/839ab70c-7682-4570-82c4-a1c94e23ac36" />

### Redis no n8n
Use o host redis-n8n e a porta 6379 no momento de criar uma credencial do Redis no n8n (não precisa preencher User e Password).

<img width="1340" height="781" alt="image" src="https://github.com/user-attachments/assets/141cd96d-5e4c-4a5c-975c-905b3b8b2b32" />

### Webhook do n8n nas instâncias da Evolution API:
use http://n8n:5678/<resto-da-url> ao invés de http://localhost:5678/<resto-da-url> sempre que for configuar a url do Wbehoook do n8n em alguma instância da Evolution.
<img width="1907" height="978" alt="image" src="https://github.com/user-attachments/assets/2a7b4a4e-e287-4b49-921e-41831415e7a9" />


---------------------------------------------------------------------------------
### 7.Comandos úteis (Docker Compose)

#### Verificar status dos contêineres
```bash
docker compose ps
```
#### Visualizar logs em tempo real (exemplo: evolution-api)
```bash
docker compose logs -f evolution-api
```

#### Reiniciar todos os serviços
```bash
docker compose restart
```

#### Parar os serviços sem remover contêineres
```bash
docker compose stop
```

#### Parar e remover contêineres (mantendo volumes)
```bash
docker compose down
```

#### Atualizar imagens e recriar os contêineres
```bash
docker compose pull && docker compose up -d --remove-orphans
```
---------------------------------------------------------------------------------
### 8. Estrutura dos serviços (resumo)

#### evolution-api
- API Evolution exposta na porta 8080.
- Utiliza variáveis do .env e persiste dados no volume evolution_instances.

#### postgres-evolution
- Banco de dados PostgreSQL da Evolution API.

#### redis-evolution
- Redis utilizado pela Evolution API.

#### n8n
- n8n exposto na porta 5678.
- Utiliza .env e está configurado para usar PostgreSQL e Redis dedicados.

#### postgres-n8n
- Banco de dados PostgreSQL do n8n.

#### redis-n8n
- Redis utilizado pelo n8n.

---------------------------------------------------------------------------------

### 9. Dicas e solução de problemas

#### Arquivo .env
- Verifique se o arquivo .env existe (copiado de .env.example) e se a variável
- AUTHENTICATION_API_KEY está definida.

#### Portas em uso
- Caso alguma porta já esteja ocupada no seu computador, altere o mapeamento de portas no
- docker-compose.yaml ou libere a porta em uso.

#### Windows / WSL2
- Confirme que o Docker Desktop está utilizando o backend WSL2 e que o projeto esteja em um diretório com bom desempenho (ex.: dentro do seu diretório de usuário).

#### Logs para diagnóstico
- Use(para acompanhar erros em tempo real):
```bash
docker compose logs -f <nome_do_servico>
```
#### Terminal na pasta correta
- Execute todos os comandos a partir da pasta do projeto, onde está o arquivo docker-compose.yaml.
---------------------------------------------------------------------------------
### 10. Remover tudo (inclusive volumes)

⚠️ Atenção: este comando remove contêineres e apaga todos os dados persistidos nos volumes.

```bash
docker compose down -v
```
---------------------------------------------------------------------------------
### Criado por: Filipe Amorim

#### Minhas Redes Sociais

**LinkedIn**: https://www.linkedin.com/in/filipe-amorim/

**GitHub**: https://github.com/filipe-amorim

**Licença**: 
Use e adapte livremente conforme suas necessidades.
