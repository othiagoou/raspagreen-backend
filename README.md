# Raspadinha Backend

Backend da aplicação de raspadinha online desenvolvido em Node.js com Supabase.

## 🚀 Tecnologias

- **Node.js** + **Express.js** - Framework web
- **Supabase** - Banco de dados PostgreSQL com RLS
- **JWT** - Autenticação
- **Winston** - Logging
- **Express Rate Limit** - Rate limiting
- **Helmet** - Segurança
- **CORS** - Cross-origin resource sharing

## 📋 Pré-requisitos

- Node.js 18+ 
- NPM ou Yarn
- Conta no Supabase

## ⚙️ Configuração

### 1. Instalar dependências

```bash
npm install
```

### 2. Configurar variáveis de ambiente

Copie o arquivo `.env.example` para `.env` e configure:

```bash
cp .env.example .env
```

Edite o `.env` com suas credenciais do Supabase:

```env
SUPABASE_URL=your_supabase_project_url
SUPABASE_ANON_KEY=your_supabase_anon_key  
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
JWT_SECRET=your_jwt_secret_key
PORT=3000
NODE_ENV=development
FRONTEND_URL=http://localhost:5173
```

### 3. Configurar banco de dados

Execute o script de setup para criar as tabelas:

```bash
node database/setup-database.js
```

### 4. Iniciar servidor

```bash
# Desenvolvimento (com nodemon)
npm run dev

# Produção
npm start
```

## 📚 Documentação da API

### Autenticação

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/api/auth/register` | Registrar usuário |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/logout` | Logout |
| GET | `/api/auth/profile` | Obter perfil |
| PUT | `/api/auth/profile` | Atualizar perfil |
| GET | `/api/auth/stats` | Estatísticas do usuário |

### Raspadinhas

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/scratch` | Listar categorias |
| GET | `/api/scratch/:slug` | Detalhes da categoria |
| GET | `/api/scratch/:slug/rewards` | Prêmios da categoria |
| POST | `/api/scratch/:slug/buy` | Comprar raspadinha |
| GET | `/api/scratch/games/history` | Histórico de jogos |
| GET | `/api/scratch/games/:id` | Detalhes do jogo |

### Carteira

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/wallet` | Informações da carteira |
| GET | `/api/wallet/transactions` | Histórico de transações |
| POST | `/api/wallet/deposit` | Depositar (teste) |
| POST | `/api/wallet/withdraw` | Solicitar saque |
| GET | `/api/wallet/summary` | Resumo financeiro |

## 🎮 Sistema de Jogos

### RTP (Return to Player)

- **RTP Padrão**: 85%
- **Controle Automático**: Sistema ajusta probabilidades baseado no RTP atual
- **Algoritmo Inteligente**: Evita sequências de grandes ganhos/perdas

### Probabilidades

- Cada prêmio tem um `probability_weight`
- Sistema considera RTP atual vs RTP alvo
- Geração de grid 3x3 balanceada

### Segurança

- **Row Level Security** (RLS) no Supabase
- **Rate Limiting** por usuário e IP
- **Validação** de saldo antes de compras
- **Logs** detalhados de todas as operações

## 🛡️ Segurança

### Rate Limiting

- **Geral**: 100 req/15min por IP
- **Login**: 5 tentativas/15min por IP
- **Jogos**: 10 jogos/min por usuário
- **Transações**: 3 transações/5min por usuário

### Validações

- Entrada de dados com `express-validator`
- Verificação de saldo antes de transações
- Autenticação JWT em rotas protegidas

## 📊 Monitoramento

### Logs

Os logs são salvos em:
- `logs/error.log` - Apenas erros
- `logs/combined.log` - Todos os logs
- Console (desenvolvimento)

### Health Check

```bash
GET /health
```

Retorna status da API e conexão com banco.

## 🚀 Deploy

### Variáveis de Produção

```env
NODE_ENV=production
PORT=3000
SUPABASE_URL=your_production_supabase_url
SUPABASE_SERVICE_ROLE_KEY=your_production_service_key
JWT_SECRET=your_strong_jwt_secret
FRONTEND_URL=https://your-frontend-domain.com
```

### Recomendações

- Use **PM2** para gerenciamento de processos
- Configure **nginx** como proxy reverso
- Ative **HTTPS** em produção
- Configure backup do banco de dados

## 🧪 Testes

```bash
npm test
```

## 📝 Estrutura do Projeto

```
src/
├── config/          # Configurações
├── controllers/     # Controllers da API
├── middleware/      # Middlewares
├── routes/          # Definições de rotas
├── services/        # Lógica de negócio
├── utils/           # Utilitários
└── app.js           # Arquivo principal

database/
├── *.sql            # Scripts SQL
├── setup-database.js # Script de configuração
└── README.md        # Documentação do banco
```

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT.#   l o l  
 #   l o l  
 #   l o l  
 