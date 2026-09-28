# APP - O.S PREVENIR EXTINTORES

Aplicativo mobile (Android e iOS) para gerenciamento de Ordens de Serviço da **PREVENIR EXTINTORES**, empresa especializada em instalações elétricas e serviços de combate a incêndio (SPDA).

O sistema permite abrir, atribuir, acompanhar e finalizar O.S., registrando data, horário e responsável em cada etapa do atendimento.

---

## Estrutura do Repositório

```
prevenir-os/
├── api-os/               → Backend (Spring Boot)
├── mobile/               → Aplicativo mobile (React Native + Expo)
├── docker-compose.yml    → Banco de dados PostgreSQL
├── .gitmodules
└── README.md
```

---

## ⚙️ Funcionalidades principais

- **Autenticação de usuários** com login seguro via JWT e controle por perfil (Admin e Funcionários)
- **Cadastro de clientes** com CNPJ, telefone e endereço
- **Cadastro de funcionários** com cargo e especialidade (eletricista, ajudante, etc)
- **Abertura de O.S.** com numeração automática, tipo de serviço, prioridade e descrição
- **Atribuição de O.S.** ao funcionário, com histórico de reatribuições
- **Acompanhamento de status** ("Aberta", "Em andamento", "Aguardando material", "Concluída", "Cancelada")
- **Finalização com rastreabilidade**, registrando data, horário, usuário responsável e local
- **Histórico completo** de todas as mudanças da O.S.
- **Filtros de consulta** por status, prioridade, técnico, cliente, tipo de serviço e período de serviço

---

## Tipos de serviço

| Área | Exemplos |
|---|---|
| Instalação elétrica | Instalação, manutenção, quadro de distribuição, SPDA, laudo elétrico |
| Combate a incêndio | Recarga e inspeção de extintores, hidrantes, alarme, iluminação de emergência, sinalização |

---

## Perfis de acesso

| Perfil | Permissões |
|---|---|
| Admin | Gerencia usuários, técnicos e clientes, atribui, cancela e reabre O.S., visualiza todas |
| Funcionário | Visualiza as O.S. atribuídas a ele, altera status e finaliza |

---

## Fluxo de status da O.S.

```
ABERTA → EM_ANDAMENTO → AGUARDANDO_MATERIAL ⇄ EM_ANDAMENTO → CONCLUIDA
   ↓            ↓                ↓
CANCELADA   CANCELADA        CANCELADA
```

> Datas, horários e usuários de abertura, mudança de status e finalização são sempre gerados pelo servidor e não podem ser alterados.

---

## Stack do projeto

| Camada | Tecnologia |
|---|---|
| Backend | Java (Spring Boot) + Spring Security (JWT) |
| Banco de dados | PostgreSQL |
| Mobile | React Native + Expo (Android e iOS) |
| Infra | Docker |

---

## Pré-requisitos

- Java 21+
- Node.js 20+
- Docker e Docker Compose
- App **Expo Go** no celular (para testes) ou emulador Android / simulador iOS

---

### 1. Clonar o repositório com os submódulos

```bash
git clone --recurse-submodules https://github.com/lliliss/NOME_DO_APP.git
cd NOME_DO_APP
```

> Caso já tenha clonado sem os submódulos, rode:
> ```bash
> git submodule update --init --recursive
> ```

---

### 2. Subir o banco de dados

```bash
docker compose up -d
```

O PostgreSQL estará disponível em: `localhost:5432`

---

### 3. Configurar variáveis de ambiente do Backend

Crie o arquivo `api-os/.env` com base no `.env.example`:

```env
DB_URL=jdbc:postgresql://localhost:5432/os_db
DB_USER=postgres
DB_PASSWORD=postgres
JWT_SECRET=sua_chave_secreta
JWT_EXPIRATION=28800000
TZ=America/Maceio
```

---

### 4. Rodar o Backend

```bash
cd api-os
./mvnw spring-boot:run
```

O servidor estará disponível em: `http://localhost:8080`

---

### 5. Rodar o Mobile

Crie o arquivo `mobile/.env` apontando para a API:

```env
API_URL
```

> Use o IP da sua máquina na rede (não `localhost`), para que o celular consiga acessar a API.

```bash
cd mobile
npm install
npx expo start
```

Escaneie o QR Code com o **Expo Go** (Android) ou com a câmera (iOS).

---

## Gerando os builds

```bash
cd mobile
npx eas build --platform android
npx eas build --platform ios
```

> O build de iOS exige uma conta Apple Developer.

---

## Atualização dos submódulos

Para puxar as últimas alterações dos submódulos:

```bash
git submodule update --remote
```

---

## 👥 Equipe

| Nome | Função |
|---|---|
| Alice Ferreira | Analista de Sistemas Júnior
| Alice Ferreira | Desenvolvedora Mobile e Full-Stack

---

## Estrutura dos Submódulos

| Submódulo | Repositório |
|---|---|
| `api-os` | https://github.com/lliliss/api-os |
| `mobile` | https://github.com/lliliss/mobile-os |

---

## Tecnologias

- Spring Boot (Java)
- Spring Security + JWT
- React Native + Expo
- PostgreSQL
- Docker

---

## 📄 Licença

© 2026 lliliss. Todos os direitos reservados.
