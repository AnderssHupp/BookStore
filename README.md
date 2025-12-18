# 📚 Sistema de Gestão de Biblioteca - BookStore

Sistema completo de gestão de biblioteca desenvolvido com Laravel, oferecendo funcionalidades modernas para administração de livros, requisições, devoluções, avaliações, e-commerce e muito mais.

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Funcionalidades](#funcionalidades)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Requisitos](#requisitos)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [Estrutura de Banco de Dados](#estrutura-de-banco-de-dados)
- [Testes](#testes)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

## 🎯 Sobre o Projeto

O **InovCorp Library** é um sistema completo de gestão de biblioteca que permite:

- **Gestão de Acervo**: Administração completa de livros, autores e editoras
- **Sistema de Requisições**: Usuários podem solicitar livros para empréstimo
- **Gestão de Devoluções**: Controle completo de devoluções com verificação de estado
- **Sistema de Multas**: Cálculo automático de multas por atraso, danos ou perda
- **Avaliações**: Sistema de reviews moderado para livros
- **E-commerce**: Compra de livros com carrinho e checkout
- **Notificações**: Sistema completo de notificações por email
- **Exportação de Dados**: Exportação para Excel de livros, autores, editoras e usuários
- **Logs de Atividade**: Rastreamento completo de ações do sistema

## 🛠 Tecnologias Utilizadas

### Backend
- **Laravel 12** - Framework PHP moderno
- **PHP 8.2+** - Linguagem de programação
- **Laravel Jetstream** - Autenticação e gestão de perfis
- **Laravel Fortify** - Autenticação robusta
- **Laravel Sanctum** - API Authentication
- **Laravel Livewire** - Componentes interativos
- **Stripe** - Gateway de pagamento
- **Maatwebsite Excel** - Exportação de dados
- **DomPDF** - Geração de PDFs (faturas)

### Frontend
- **Tailwind CSS** - Framework CSS utilitário
- **DaisyUI** - Componentes para Tailwind
- **Vite** - Build tool moderna
- **Swiper** - Carrossel de imagens
- **Alpine.js** - Framework JavaScript leve (via Jetstream)

### Banco de Dados
- **SQLite** (desenvolvimento) / **MySQL/PostgreSQL** (produção)

### Ferramentas de Desenvolvimento
- **Pest PHP** - Framework de testes
- **PHPUnit** - Testes unitários
- **Laravel Pint** - Code style fixer
- **Laravel Pail** - Log viewer

## ✨ Funcionalidades

### 👥 Gestão de Usuários

- **Dois tipos de usuários**:
  - **Admin**: Acesso completo ao sistema
  - **Citizen**: Usuário comum da biblioteca
- Autenticação com verificação de email
- Perfis de usuário com foto
- Autenticação de dois fatores (2FA)

### 📖 Gestão de Livros

- CRUD completo de livros
- **Campos principais**:
  - ISBN, Nome, Editora, Bibliografia (criptografada)
  - Imagem de capa, Preço, Disponibilidade, Estoque
- Relacionamento muitos-para-muitos com autores
- **Busca avançada** por nome, ISBN, autor, editora
- **Ordenação** por nome, autor, editora, preço
- **Importação de livros** via Google Books API
- **Livros relacionados** baseados em similaridade de conteúdo
- **Avaliação média** calculada automaticamente

### 👨‍💼 Gestão de Autores

- CRUD completo de autores
- Foto do autor
- Relacionamento com múltiplos livros

### 🏢 Gestão de Editoras

- CRUD completo de editoras
- Logo da editora
- Relacionamento com múltiplos livros

### 📝 Sistema de Requisições

- Usuários podem solicitar livros para empréstimo
- **Estados da requisição**:
  - `pending` - Aguardando aprovação
  - `approved` - Aprovada
  - `rejected` - Rejeitada
  - `pending_returned` - Aguardando confirmação de devolução
  - `returned` - Devolvida
  - `cancelled` - Cancelada
- **Numeração automática**: REQ-000001, REQ-000002, etc.
- **Limite de requisições**: Máximo de 3 requisições ativas por usuário
- **Restrições**: Usuários com multas pendentes não podem fazer novas requisições
- Upload de foto ao receber o livro
- Data esperada de devolução

### 🔄 Sistema de Devoluções

- Usuários podem solicitar devolução de livros
- Upload de foto do estado do livro
- **Verificação de estado**:
  - `Good` - Bom estado
  - `Bad` - Mau estado
  - `Damaged` - Danificado
  - `Lost` - Perdido
- Aprovação/rejeição por administrador
- Cálculo automático de multas baseado no estado

### 💰 Sistema de Multas

- **Cálculo automático** de multas baseado em:
  - **Atraso**: €1,00 por dia de atraso
  - **Dano**: €5,00 fixo
  - **Perda**: Valor do livro
- Histórico completo de multas
- Pagamento de multas
- Bloqueio de novas requisições até quitação

### ⭐ Sistema de Avaliações

- Usuários podem avaliar livros após devolução
- **Sistema de moderação**:
  - `pending` - Aguardando moderação
  - `active` - Aprovada e visível
  - `refused` - Rejeitada
- Avaliação de 1 a 5 estrelas
- Comentários opcionais
- Notificações para administradores sobre novas avaliações

### 🛒 E-commerce

- **Carrinho de compras**:
  - Adicionar/remover livros
  - Quantidade ajustável
  - Cálculo automático de total
- **Checkout**:
  - Gestão de endereço de entrega
  - Integração com Stripe para pagamentos
  - Geração de faturas em PDF
- **Pedidos**:
  - Acompanhamento de status
  - Histórico completo
  - Cancelamento de pedidos
- **Notificações de carrinho abandonado**

### 🔔 Sistema de Notificações

- **Tipos de notificações**:
  - Confirmação de requisição
  - Livro disponível (quando estava esgotado)
  - Lembrete de devolução
  - Nova avaliação (para admin)
  - Aprovação/rejeição de avaliação
  - Carrinho abandonado
- Envio por email
- Notificações em tempo real

### 📊 Dashboard Administrativo

- **Estatísticas**:
  - Total de livros, autores, editoras
  - Pedidos pendentes e pagos
  - Gráficos mensais de pedidos
- **Gestão rápida**:
  - Requisições pendentes
  - Devoluções pendentes
  - Últimos pedidos
  - Últimos livros adicionados

### 📤 Exportação de Dados

- Exportação para Excel de:
  - Livros
  - Autores
  - Editoras
  - Usuários

### 📋 Sistema de Logs

- Rastreamento completo de atividades
- Visualização de logs no dashboard
- Histórico de ações do sistema

### 🔍 Catálogo Público

- Visualização pública de livros
- Busca e filtros
- Detalhes completos do livro
- Avaliações aprovadas visíveis

## 📁 Estrutura do Projeto

```
library/
├── app/
│   ├── Actions/              # Ações do Fortify/Jetstream
│   ├── Console/              # Comandos Artisan
│   ├── Events/               # Eventos do sistema
│   ├── Exports/              # Classes de exportação Excel
│   ├── Helpers/              # Funções auxiliares
│   ├── Http/
│   │   ├── Controllers/      # Controladores
│   │   ├── Middleware/       # Middleware customizado
│   │   └── Requests/         # Form Requests
│   ├── Jobs/                 # Jobs em fila
│   ├── Listeners/            # Listeners de eventos
│   ├── Livewire/             # Componentes Livewire
│   ├── Mail/                 # Classes de email
│   ├── Models/               # Modelos Eloquent
│   ├── Notifications/        # Notificações
│   ├── Observers/            # Observers de modelos
│   ├── Providers/            # Service Providers
│   └── View/                 # Componentes de view
├── bootstrap/                # Arquivos de inicialização
├── config/                   # Arquivos de configuração
├── database/
│   ├── factories/            # Factories para testes
│   ├── migrations/           # Migrações do banco
│   └── seeders/              # Seeders
├── public/                   # Arquivos públicos
├── resources/
│   ├── css/                  # Estilos CSS
│   ├── js/                   # JavaScript
│   ├── images/               # Imagens
│   ├── markdown/             # Arquivos Markdown
│   └── views/                # Views Blade
├── routes/                   # Rotas
├── storage/                  # Arquivos de armazenamento
├── tests/                    # Testes
└── vendor/                   # Dependências Composer
```

## 📋 Requisitos

- **PHP**: 8.2 ou superior
- **Composer**: 2.x
- **Node.js**: 18.x ou superior
- **NPM**: 9.x ou superior
- **Banco de Dados**: SQLite (dev) / MySQL 8.0+ ou PostgreSQL 13+ (prod)
- **Extensões PHP**:
  - BCMath
  - Ctype
  - Fileinfo
  - JSON
  - Mbstring
  - OpenSSL
  - PDO
  - Tokenizer
  - XML

## 🚀 Instalação

### 1. Clone o repositório

```bash
git clone <url-do-repositorio>
cd library
```

### 2. Instale as dependências PHP

```bash
composer install
```

### 3. Instale as dependências Node.js

```bash
npm install
```

### 4. Configure o ambiente

```bash
cp .env.example .env
php artisan key:generate
```

### 5. Configure o banco de dados

Edite o arquivo `.env` e configure as credenciais do banco de dados:

```env
DB_CONNECTION=sqlite
# ou para MySQL/PostgreSQL:
# DB_CONNECTION=mysql
# DB_HOST=127.0.0.1
# DB_PORT=3306
# DB_DATABASE=library
# DB_USERNAME=root
# DB_PASSWORD=
```

Para SQLite, certifique-se de que o arquivo existe:

```bash
touch database/database.sqlite
```

### 6. Execute as migrações

```bash
php artisan migrate
```

### 7. (Opcional) Execute os seeders

```bash
php artisan db:seed
```

### 8. Crie o link simbólico para storage

```bash
php artisan storage:link
```

### 9. Compile os assets

Para desenvolvimento:

```bash
npm run dev
```

Para produção:

```bash
npm run build
```

## ⚙️ Configuração

### Configuração do Email

Configure o serviço de email no arquivo `.env`:

```env
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="noreply@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```

### Configuração do Stripe

Para usar pagamentos, configure as chaves do Stripe:

```env
STRIPE_KEY=your-stripe-key
STRIPE_SECRET=your-stripe-secret
STRIPE_WEBHOOK_SECRET=your-webhook-secret
```

### Configuração de Filas

Para processar jobs em background, configure uma fila:

```env
QUEUE_CONNECTION=database
# ou
QUEUE_CONNECTION=redis
```

Execute o worker:

```bash
php artisan queue:work
```

### Configuração do Google Books API (Opcional)

Para importar livros do Google Books, configure:

```env
GOOGLE_BOOKS_API_KEY=your-api-key
```

## 🎮 Uso

### Iniciar o servidor de desenvolvimento

```bash
php artisan serve
```

Ou use o script do Composer que inicia tudo:

```bash
composer dev
```

Este comando inicia:
- Servidor Laravel (porta 8000)
- Worker de filas
- Vite dev server

### Acessar o sistema

- **URL**: http://localhost:8000
- **Dashboard Admin**: http://localhost:8000/dashboard
- **Catálogo Público**: http://localhost:8000/catalog

### Criar um usuário administrador

```bash
php artisan tinker
```

```php
$user = \App\Models\User::create([
    'name' => 'Admin',
    'email' => 'admin@example.com',
    'password' => bcrypt('password'),
    'role' => 'admin',
    'email_verified_at' => now(),
]);
```

## 🗄️ Estrutura de Banco de Dados

### Principais Tabelas

- **users** - Usuários do sistema
- **books** - Livros
- **authors** - Autores
- **publishers** - Editoras
- **author_book** - Relacionamento muitos-para-muitos entre autores e livros
- **book_requests** - Requisições de empréstimo
- **fines** - Multas
- **reviews** - Avaliações de livros
- **book_notifications** - Notificações de disponibilidade
- **carts** - Carrinhos de compra
- **cart_items** - Itens do carrinho
- **orders** - Pedidos
- **order_items** - Itens do pedido
- **logs** - Logs de atividade

### Relacionamentos Principais

- **Book** ↔ **Author** (Many-to-Many)
- **Book** → **Publisher** (Many-to-One)
- **User** → **BookRequest** (One-to-Many)
- **BookRequest** → **Book** (Many-to-One)
- **BookRequest** → **Fine** (One-to-Many)
- **BookRequest** → **Review** (One-to-Many)
- **User** → **Cart** (One-to-One)
- **Cart** → **CartItem** (One-to-Many)
- **User** → **Order** (One-to-Many)
- **Order** → **OrderItem** (One-to-Many)

## 🧪 Testes

O projeto utiliza **Pest PHP** para testes. Execute os testes com:

```bash
composer test
```

Ou:

```bash
php artisan test
```

Para executar testes específicos:

```bash
php artisan test --filter BookRequestTest
```

## 🔐 Segurança

- **Criptografia**: Bibliografia dos livros é criptografada automaticamente
- **Autenticação**: Laravel Fortify com 2FA
- **Autorização**: Middleware de admin para rotas protegidas
- **Sanitização**: Validação de inputs com Form Requests
- **CSRF Protection**: Proteção CSRF em todas as rotas
- **SQL Injection**: Protegido pelo Eloquent ORM
- **XSS Protection**: Blade templates escapam automaticamente

## 📝 Observações Importantes

### Limites e Regras de Negócio

- **Máximo de 3 requisições ativas** por usuário
- **Usuários com multas pendentes** não podem fazer novas requisições
- **Multas calculadas automaticamente**:
  - €1,00 por dia de atraso
  - €5,00 por dano
  - Valor do livro se perdido
- **Avaliações moderadas** antes de serem exibidas publicamente

### Observers Implementados

- **BookObserver**: Logs de criação/atualização de livros
- **AuthorObserver**: Logs de criação/atualização de autores
- **PublisherObserver**: Logs de criação/atualização de editoras
- **BookRequestObserver**: Notificações e logs de requisições
- **OrderObserver**: Processamento de pedidos

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 👨‍💻 Desenvolvido por

**InovCorp**

---

## 📞 Suporte

Para suporte, envie um email para suporte@inovcorp.com ou abra uma issue no repositório.

---

**⭐ Se este projeto foi útil para você, considere dar uma estrela!**
