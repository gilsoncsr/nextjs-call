# 🚀 Ignite Call - Sistema de Agendamento Inteligente

## 📋 Visão Geral

O **Ignite Call** é uma aplicação web moderna e robusta desenvolvida para simplificar o processo de agendamento de compromissos. A plataforma permite que usuários conectem seus calendários do Google e gerenciem sua disponibilidade de forma eficiente, enquanto outros usuários podem agendar horários de forma simples e intuitiva.

## ✨ Funcionalidades Principais

### 🔐 Sistema de Autenticação

- **OAuth 2.0 com Google**: Login seguro e integrado
- **NextAuth.js**: Gerenciamento de sessões robusto
- **Permissões de Calendário**: Acesso ao Google Calendar para sincronização

### 👤 Gerenciamento de Usuários

- **Perfil Personalizado**: Nome, username único, bio e avatar
- **Claim de Username**: Sistema para reservar nomes de usuário
- **Perfil Público**: Página personalizada para cada usuário

### 📅 Sistema de Agendamento

- **Calendário Interativo**: Interface visual para seleção de datas
- **Gestão de Disponibilidade**: Configuração de horários por dia da semana
- **Agendamentos Automáticos**: Criação automática de eventos no Google Calendar
- **Prevenção de Conflitos**: Sistema anti-duplicação de horários

### 🕐 Gestão de Horários

- **Intervalos de Tempo**: Configuração flexível de horários disponíveis
- **Validações Inteligentes**: Verificação de disponibilidade em tempo real
- **Bloqueio de Datas**: Sistema para marcar datas indisponíveis

## 🏗️ Arquitetura do Projeto

### **Frontend**

- **Next.js 13**: Framework React com renderização híbrida
- **TypeScript**: Tipagem estática para maior confiabilidade
- **Ignite UI**: Sistema de componentes personalizado e consistente
- **React Hook Form**: Gerenciamento eficiente de formulários
- **Zod**: Validação de schemas em tempo de execução

### **Backend**

- **API Routes**: Endpoints Next.js para funcionalidades backend
- **Prisma ORM**: Gerenciamento de banco de dados type-safe
- **MySQL**: Banco de dados relacional robusto
- **Google APIs**: Integração com Google Calendar

### **Estado e Cache**

- **React Query**: Gerenciamento de estado do servidor e cache
- **NextAuth**: Gerenciamento de sessões e autenticação
- **Cookies**: Armazenamento seguro de dados de sessão

## 🗄️ Estrutura do Banco de Dados

### **Modelos Principais**

#### `users`

- **id**: UUID único do usuário
- **username**: Nome de usuário único para URLs
- **name**: Nome completo do usuário
- **bio**: Biografia opcional
- **email**: Email do usuário (opcional)
- **avatar_url**: URL da foto de perfil
- **created_at**: Timestamp de criação

#### `user_time_intervals`

- **id**: UUID único do intervalo
- **week_day**: Dia da semana (0-6)
- **time_start_in_minutes**: Hora de início em minutos
- **time_end_in_minutes**: Hora de fim em minutos
- **user_id**: Referência ao usuário

#### `schedulings`

- **id**: UUID único do agendamento
- **date**: Data e hora do compromisso
- **name**: Nome do cliente
- **email**: Email do cliente
- **observations**: Observações opcionais
- **user_id**: Referência ao usuário
- **created_at**: Timestamp de criação

#### `accounts` e `sessions`

- **Suporte NextAuth**: Gerenciamento de contas OAuth e sessões

### **Relacionamentos**

- **1:N**: Usuário → Intervalos de tempo
- **1:N**: Usuário → Agendamentos
- **1:N**: Usuário → Contas OAuth
- **1:N**: Usuário → Sessões ativas

## 🚀 Estrutura de Diretórios

```
src/
├── @types/                 # Definições de tipos TypeScript
├── assets/                 # Imagens e recursos estáticos
├── components/             # Componentes reutilizáveis
│   └── Calendar/          # Componente de calendário personalizado
├── lib/                    # Bibliotecas e configurações
│   ├── auth/              # Configurações de autenticação
│   ├── axios.ts           # Cliente HTTP configurado
│   ├── dayjs.ts           # Configuração de datas
│   ├── google.ts          # Integração Google APIs
│   ├── prisma.ts          # Cliente Prisma
│   └── react-query.ts     # Configuração React Query
├── pages/                  # Páginas e rotas da aplicação
│   ├── api/               # Endpoints da API
│   ├── home/              # Página inicial
│   ├── register/          # Fluxo de registro
│   └── schedule/          # Sistema de agendamento
├── styles/                 # Estilos globais
└── utils/                  # Funções utilitárias
```

## 🔧 Configuração e Instalação

### **Pré-requisitos**

- Node.js 18+
- MySQL 8.0+
- Conta Google Cloud Platform

### **Variáveis de Ambiente**

```env
# Banco de Dados
DATABASE_URL="mysql://user:password@localhost:3306/ignite_call"

# Google OAuth
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-nextauth-secret"
```

### **Instalação**

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/ignite-call.git
cd ignite-call

# Instale as dependências
npm install

# Configure o banco de dados
npx prisma migrate dev

# Execute em desenvolvimento
npm run dev
```

## 📱 Fluxo de Usuário

### **1. Registro e Configuração**

1. **Claim de Username**: Usuário reserva um nome único
2. **Conectar Calendário**: Autenticação OAuth com Google
3. **Configurar Horários**: Define disponibilidade semanal
4. **Perfil Final**: Adiciona bio e informações pessoais

### **2. Agendamento de Compromissos**

1. **Seleção de Data**: Calendário interativo com datas disponíveis
2. **Escolha de Horário**: Lista de horários livres no dia
3. **Confirmação**: Formulário com dados do cliente
4. **Criação Automática**: Evento criado no Google Calendar

## 🔌 APIs e Endpoints

### **Autenticação**

- `POST /api/auth/signin` - Login OAuth
- `POST /api/auth/signout` - Logout
- `GET /api/auth/session` - Verificar sessão

### **Usuários**

- `POST /api/users` - Criar usuário
- `PUT /api/users/profile` - Atualizar perfil
- `GET /api/users/[username]` - Obter perfil público

### **Agendamentos**

- `POST /api/users/[username]/schedule` - Criar agendamento
- `GET /api/users/[username]/availability` - Verificar disponibilidade
- `GET /api/users/[username]/blocked-dates` - Datas bloqueadas

### **Intervalos de Tempo**

- `POST /api/users/time-intervals` - Configurar horários

## 🎨 Sistema de Design

### **Componentes Ignite UI**

- **Design System Consistente**: Componentes padronizados
- **Tema Escuro**: Interface moderna e elegante
- **Responsivo**: Adaptável a diferentes dispositivos
- **Acessibilidade**: Componentes acessíveis por padrão

### **Estilos**

- **CSS-in-JS**: Estilos encapsulados e reutilizáveis
- **Variáveis CSS**: Sistema de design tokens
- **Animações**: Transições suaves e feedback visual

## 🔒 Segurança

### **Autenticação**

- **OAuth 2.0**: Padrão de segurança da indústria
- **JWT Tokens**: Sessões seguras e gerenciadas
- **Refresh Tokens**: Renovação automática de acesso

### **Validação**

- **Zod Schemas**: Validação de dados em tempo de execução
- **Sanitização**: Prevenção de ataques de injeção
- **Rate Limiting**: Proteção contra abuso de API

### **Banco de Dados**

- **Prepared Statements**: Prevenção de SQL injection
- **Índices Otimizados**: Performance e segurança
- **Relacionamentos Seguros**: Constraints de integridade

## 📊 Performance e Otimização

### **Renderização**

- **SSG/SSR Híbrido**: Melhor performance e SEO
- **Code Splitting**: Carregamento sob demanda
- **Image Optimization**: Otimização automática de imagens

### **Cache e Estado**

- **React Query**: Cache inteligente de dados
- **Stale-While-Revalidate**: Dados sempre atualizados
- **Background Updates**: Atualizações em segundo plano

### **Banco de Dados**

- **Índices Estratégicos**: Consultas otimizadas
- **Relacionamentos Eficientes**: Joins otimizados
- **Paginação**: Carregamento progressivo de dados

## 🧪 Testes e Qualidade

### **TypeScript**

- **Tipagem Estática**: Prevenção de erros em tempo de compilação
- **Interfaces Bem Definidas**: Contratos claros entre componentes
- **Generics**: Componentes reutilizáveis e type-safe

### **ESLint**

- **Configuração Rocketseat**: Padrões de código consistentes
- **Regras Automatizadas**: Manutenção de qualidade
- **Prevenção de Bugs**: Detecção de problemas comuns

## 🚀 Deploy e Produção

### **Vercel (Recomendado)**

- **Deploy Automático**: Integração com Git
- **Edge Functions**: Performance global
- **Analytics**: Métricas de performance

### **Outras Opções**

- **Netlify**: Deploy estático e serverless
- **AWS**: Infraestrutura escalável
- **Docker**: Containerização para produção

## 🔄 Migrações e Versionamento

### **Estrutura de Migrações**

- **Versionamento Incremental**: Mudanças controladas
- **Rollback Seguro**: Reversão de alterações
- **Índices Otimizados**: Performance contínua

### **Histórico de Mudanças**

- **v1.0.0**: Estrutura inicial do banco
- **v1.1.0**: Otimização de tipos de texto
- **v1.2.0**: Adição de índices para performance

## 🤝 Contribuição

### **Como Contribuir**

1. **Fork** do repositório
2. **Branch** para nova funcionalidade
3. **Commit** com mensagens claras
4. **Pull Request** com descrição detalhada

### **Padrões de Código**

- **Conventional Commits**: Padrão de mensagens
- **TypeScript Strict**: Configuração rigorosa
- **Componentes Funcionais**: Hooks e padrões modernos

## 📚 Recursos e Documentação

### **Tecnologias Utilizadas**

- [Next.js](https://nextjs.org/) - Framework React
- [Prisma](https://www.prisma.io/) - ORM moderno
- [NextAuth.js](https://next-auth.js.org/) - Autenticação
- [React Query](https://tanstack.com/query) - Gerenciamento de estado
- [Zod](https://zod.dev/) - Validação de schemas
- [Day.js](https://day.js.org/) - Manipulação de datas

### **APIs Externas**

- [Google Calendar API](https://developers.google.com/calendar)
- [Google OAuth 2.0](https://developers.google.com/identity/protocols/oauth2)

