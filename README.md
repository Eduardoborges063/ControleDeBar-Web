# 🍺 Controle de Bar

Aplicação web em **ASP.NET Core MVC** para gerenciar o dia a dia de um bar ou restaurante: mesas, garçons, produtos e contas (comandas) com seus pedidos.

O projeto também inclui uma versão em **console** que reaproveita as mesmas camadas de domínio e infraestrutura.

---

## 📋 Funcionalidades

### 🪑 Mesas
- Cadastrar, editar, excluir e listar mesas
- Controle de status da mesa (livre ou ocupada)

### 🧑‍🍳 Garçons
- Cadastrar, editar, excluir e listar garçons
- Validação de nome e CPF

### 🛒 Produtos
- Cadastrar, editar, excluir e listar produtos
- Nome e valor de cada produto

### 🧾 Contas
- Abrir conta informando titular, mesa e garçom
- Adicionar e remover pedidos (produto + quantidade) de uma conta aberta
- Cálculo automático do valor total da conta
- Fechar conta, liberando a mesa automaticamente
- Listar todas as contas, apenas as **abertas** ou apenas as **fechadas**
- Visualizar os detalhes de cada conta

---

## ✅ Regras de validação

| Módulo  | Regra |
|---------|-------|
| Mesa    | Número e capacidade devem ser maiores que 0 |
| Garçom  | Nome entre 3 e 100 caracteres; CPF no formato `XXX.XXX.XXX-XX` |
| Produto | Nome entre 2 e 100 caracteres; valor deve ser informado |
| Conta   | Titular entre 3 e 100 caracteres; mesa e garçom são obrigatórios |

Ao **abrir** uma conta, a mesa passa a ficar ocupada; ao **fechar**, ela volta a ficar livre.

---

## 🧱 Arquitetura

A solução é dividida em camadas, cada uma em seu projeto:

```
ControleDeBar/
├── ControleDeBar.Dominio                 # Entidades e regras de negócio
├── ControleDeBar.Infraestrutura.Arquivos # Persistência em arquivo JSON
├── ControleDeBar.Infraestrutura.Memoria  # Persistência em memória
├── ControleDeBar.WebApp                  # Aplicação web (MVC) ← principal
└── ControleDeBar.ConsoleApp              # Versão em console
```

- **Dominio:** `Mesa`, `Garcom`, `Produto`, `Conta` e `Pedido`, com suas validações.
- **Infraestrutura.Arquivos:** repositórios que gravam os dados em um arquivo JSON.
- **Infraestrutura.Memoria:** repositórios que guardam os dados apenas em memória.
- **WebApp:** controllers, view models e views Razor com Bootstrap 5.

---

## 🛠️ Tecnologias

- [.NET 8](https://dotnet.microsoft.com/)
- ASP.NET Core MVC (Razor Views)
- C#
- Bootstrap 5 e Bootstrap Icons
- Persistência em arquivo JSON (`System.Text.Json`)

---

## 🚀 Como executar

### Pré-requisitos

- [SDK do .NET 8](https://dotnet.microsoft.com/download/dotnet/8.0)
- Opcional: Visual Studio 2022 ou VS Code com a extensão C# Dev Kit

Para conferir se o .NET está instalado:

```bash
dotnet --version
```

### Passo a passo

1. Clone o repositório:

   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   cd SEU-REPOSITORIO
   ```

2. Execute a aplicação web a partir da pasta raiz:

   ```bash
   dotnet run --project ControleDeBar.WebApp
   ```

3. Acesse no navegador:

   - http://localhost:5267
   - ou https://localhost:7237 (perfil `https`)

> **Pelo Visual Studio:** abra o arquivo `ControleDeBar.sln`, defina `ControleDeBar.WebApp` como projeto de inicialização e pressione **F5**.

### Versão em console

```bash
dotnet run --project ControleDeBar.ConsoleApp
```

---

## 💾 Armazenamento dos dados

A aplicação web grava os dados em um arquivo JSON, definido em `ContextoDados`:

```
C:\temp\dados-controle-bar.json
```

O caminho está fixo para o Windows. Em Linux ou macOS, altere o valor de `pastaArmazenamento` na classe `ContextoDados` (projeto `ControleDeBar.Infraestrutura.Arquivos`) para uma pasta válida no seu sistema.

---

## 🗺️ Rotas principais

| Rota        | Descrição                         |
|-------------|-----------------------------------|
| `/`         | Página inicial                    |
| `/Mesa`     | Gerenciamento de mesas            |
| `/Garcom`   | Gerenciamento de garçons          |
| `/Produto`  | Gerenciamento de produtos         |
| `/Conta`    | Contas (filtros: `?status=abertas` ou `?status=fechadas`) |

---

## 👤 Autor

Desenvolvido por **Eduardo Macedo** — [GitHub](https://github.com/SEU-USUARIO)
