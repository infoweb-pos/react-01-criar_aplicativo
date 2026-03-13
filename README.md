# react-01-criar_aplicativo

> **Notas de aula** — Tutorial passo a passo sobre como criar um aplicativo web (frontend) React com [Next.js](https://nextjs.org/) usando [GitHub](https://github.com) e [GitHub Codespaces](https://github.com/features/codespaces).

---

## Sumário

1. [Pré-requisitos](#1-pré-requisitos)
2. [Criar o repositório no GitHub](#2-criar-o-repositório-no-github)
3. [Abrir o GitHub Codespace](#3-abrir-o-github-codespace)
4. [Criar o aplicativo Next.js](#4-criar-o-aplicativo-nextjs)
   - 4.1 [Executar o `create-next-app`](#41-executar-o-create-next-app)
   - 4.2 [Opções de configuração](#42-opções-de-configuração)
5. [Configurar o Biome](#5-configurar-o-biome)
   - 5.1 [Instalar o Biome](#51-instalar-o-biome)
   - 5.2 [Configurar o `biome.json`](#52-configurar-o-biomejson)
   - 5.3 [Adicionar scripts no `package.json`](#53-adicionar-scripts-no-packagejson)
   - 5.4 [Remover ESLint](#54-remover-eslint)
6. [Configurar o React Compiler](#6-configurar-o-react-compiler)
   - 6.1 [Instalar as dependências](#61-instalar-as-dependências)
   - 6.2 [Ativar no `next.config.ts`](#62-ativar-no-nextconfigts)
7. [Estrutura de diretórios do projeto](#7-estrutura-de-diretórios-do-projeto)
8. [Executar o projeto](#8-executar-o-projeto)
9. [Links externos](#9-links-externos)

---

## 1. Pré-requisitos

Antes de começar, certifique-se de que você possui:

| Requisito | Descrição |
|-----------|-----------|
| **Conta GitHub** | Necessária para criar repositório e usar o Codespace. Crie gratuitamente em [github.com](https://github.com/signup). |
| **Navegador moderno** | Chrome, Edge, Firefox ou Safari atualizado. O Codespace roda 100% no navegador. |
| **Conhecimentos básicos** | HTML, CSS, JavaScript e noções de terminal/linha de comando. |

> 💡 **Dica:** Não é necessário instalar nada na sua máquina. O GitHub Codespace fornece um ambiente de desenvolvimento completo na nuvem com Node.js, npm e todas as ferramentas necessárias.

---

## 2. Criar o repositório no GitHub

1. Acesse [github.com](https://github.com) e faça login.

2. Clique no botão **"New"** (ou acesse diretamente [github.com/new](https://github.com/new)).

3. Preencha as informações do repositório:
   - **Repository name:** `meu-app-react` (ou o nome que preferir)
   - **Description:** `Aplicativo web React com Next.js` (opcional)
   - **Visibility:** `Public` ou `Private`
   - ✅ Marque **"Add a README file"**

4. Clique em **"Create repository"**.

> 📘 **Referência:** [Criando um repositório no GitHub](https://docs.github.com/pt/repositories/creating-and-managing-repositories/creating-a-new-repository)

---

## 3. Abrir o GitHub Codespace

O **GitHub Codespace** é um ambiente de desenvolvimento na nuvem baseado no [VS Code](https://code.visualstudio.com/), sem necessidade de instalar nada localmente.

1. No repositório recém-criado, clique no botão verde **"Code"**.

2. Clique na aba **"Codespaces"**.

3. Clique em **"Create codespace on main"**.

   > O Codespace levará alguns minutos para provisionar. Quando terminar, você terá um VS Code completo no navegador, com terminal integrado, já conectado ao seu repositório.

4. No terminal do Codespace (menu **Terminal → New Terminal**), verifique as versões disponíveis:
   ```bash
   node --version
   npm --version
   ```

> 📘 **Referência:** [Início rápido para GitHub Codespaces](https://docs.github.com/pt/codespaces/getting-started/quickstart)

---

## 4. Criar o aplicativo Next.js

### 4.1 Executar o `create-next-app`

No terminal do Codespace, execute:

```bash
npx create-next-app@latest .
```

> O `.` indica que o app será criado na raiz do repositório atual. Se preferir criar em um subdiretório, substitua `.` pelo nome da pasta, por exemplo `npx create-next-app@latest meu-app`.

### 4.2 Opções de configuração

O assistente interativo fará uma série de perguntas. Responda conforme abaixo:

```
What is your project named? › my-app
Would you like to use TypeScript? › Yes
Would you like to use ESLint? › No
Would you like to use Tailwind CSS? › Yes
Would you like your code inside a `src/` directory? › Yes
Would you like to use App Router? (recommended) › Yes
Would you like to use Turbopack for next dev? › Yes
Would you like to customize the import alias (@/* by default)? › Yes
What import alias would you like configured? › @/*
```

| Opção | Escolha | Motivo |
|-------|---------|--------|
| **TypeScript** | `Yes` | Tipagem estática melhora a qualidade do código. |
| **ESLint** | `No` | Será substituído pelo **Biome**, que faz lint e formatação em um único pacote. |
| **Tailwind CSS** | `Yes` | Framework CSS utilitário, muito produtivo para estilização. |
| **`src/` directory** | `Yes` | Organiza o código-fonte separado dos arquivos de configuração. |
| **App Router** | `Yes` | Roteamento moderno do Next.js com suporte a Server Components. |
| **Turbopack** | `Yes` | Bundler incrementalmente mais rápido que o Webpack, integrado ao Next.js. |
| **Import alias** | `@/*` | Permite importar com `@/components/...` em vez de `../../components/...`. |

Aguarde a instalação das dependências. Ao final, você verá:

```
✔ Success! Created my-app
```

---

## 5. Configurar o Biome

O [Biome](https://biomejs.dev/) é uma ferramenta de **lint e formatação** para JavaScript/TypeScript extremamente rápida, escrita em Rust. Ele substitui ESLint + Prettier com uma única dependência.

### 5.1 Instalar o Biome

```bash
npm install --save-dev --save-exact @biomejs/biome
```

### 5.2 Configurar o `biome.json`

Inicialize o arquivo de configuração:

```bash
npx @biomejs/biome init
```

Isso gera o arquivo `biome.json` na raiz do projeto. Edite-o com as configurações abaixo:

```json
{
  "$schema": "https://biomejs.dev/schemas/1.9.4/schema.json",
  "vcs": {
    "enabled": true,
    "clientKind": "git",
    "useIgnoreFile": true
  },
  "files": {
    "ignoreUnknown": false,
    "ignore": [
      "node_modules",
      ".next",
      "dist"
    ]
  },
  "formatter": {
    "enabled": true,
    "indentStyle": "space",
    "indentWidth": 2,
    "lineWidth": 100
  },
  "organizeImports": {
    "enabled": true
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true
    }
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "double",
      "jsxQuoteStyle": "double",
      "semicolons": "asNeeded",
      "trailingCommas": "es5"
    }
  }
}
```

### 5.3 Adicionar scripts no `package.json`

Abra o arquivo `package.json` e adicione os scripts de lint e formatação dentro da chave `"scripts"`:

```json
{
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "biome lint --write .",
    "format": "biome format --write .",
    "check": "biome check --write ."
  }
}
```

> 💡 O comando `check` executa lint + formatação + organização de imports em uma única chamada.

### 5.4 Remover ESLint

Como optamos por não usar ESLint no passo de criação, o `create-next-app` não o instalou. Confirme que não existem arquivos como `.eslintrc.*` ou `eslint.config.*` no projeto. Se existirem, remova-os:

```bash
rm -f .eslintrc.json .eslintrc.js .eslintrc.cjs eslint.config.js eslint.config.mjs
```

---

## 6. Configurar o React Compiler

O [React Compiler](https://react.dev/learn/react-compiler) (anteriormente chamado de "React Forget") é uma ferramenta experimental que **otimiza automaticamente** componentes React, eliminando a necessidade de `useMemo`, `useCallback` e `React.memo` na maioria dos casos.

### 6.1 Instalar as dependências

```bash
npm install --save-dev babel-plugin-react-compiler@experimental
npm install react@experimental react-dom@experimental
```

> ⚠️ **Atenção:** As versões `@experimental` incluem as APIs mais recentes necessárias para o React Compiler. Em produção, avalie se prefere aguardar o lançamento estável.

### 6.2 Ativar no `next.config.ts`

Abra o arquivo `next.config.ts` e configure o React Compiler:

```typescript
import type { NextConfig } from "next"

const nextConfig: NextConfig = {
  experimental: {
    reactCompiler: true,
  },
}

export default nextConfig
```

Verifique se o compilador está funcionando executando o build:

```bash
npm run build
```

> 📘 **Referência:** [React Compiler — documentação oficial](https://react.dev/learn/react-compiler)

---

## 7. Estrutura de diretórios do projeto

Após seguir todos os passos, a estrutura do seu projeto será semelhante a esta:

```
meu-app/
├── .git/                        # Metadados do Git (não edite manualmente)
├── .gitignore                   # Arquivos ignorados pelo Git
├── .next/                       # Build gerado pelo Next.js (gerado automaticamente)
├── biome.json                   # Configuração do Biome (lint + formatação)
├── next.config.ts               # Configuração do Next.js
├── next-env.d.ts                # Tipos TypeScript gerados pelo Next.js
├── node_modules/                # Dependências instaladas (não commitar)
├── package.json                 # Metadados e dependências do projeto
├── package-lock.json            # Lock file das dependências exatas
├── postcss.config.mjs           # Configuração do PostCSS (usado pelo Tailwind)
├── public/                      # Arquivos estáticos públicos (imagens, fontes, ícones)
│   ├── file.svg
│   ├── globe.svg
│   ├── next.svg
│   ├── vercel.svg
│   └── window.svg
├── README.md                    # Documentação do projeto
├── src/                         # Código-fonte da aplicação
│   └── app/                     # Diretório do App Router
│       ├── favicon.ico          # Ícone da aba do navegador
│       ├── globals.css          # Estilos globais (inclui diretivas do Tailwind)
│       ├── layout.tsx           # Layout raiz da aplicação (HTML + Body)
│       └── page.tsx             # Página inicial (rota "/")
└── tsconfig.json                # Configuração do TypeScript
```

### Descrição dos principais arquivos e diretórios

| Caminho | Descrição |
|---------|-----------|
| `src/app/` | Contém todas as rotas e layouts da aplicação (App Router). Cada pasta cria uma rota. |
| `src/app/layout.tsx` | Layout raiz: define as tags `<html>` e `<body>`, fontes globais e metadados padrão. Envolve todas as páginas. |
| `src/app/page.tsx` | Componente da rota raiz (`/`). É o que aparece ao acessar `http://localhost:3000`. |
| `src/app/globals.css` | Estilos globais. Contém as diretivas `@tailwind base`, `@tailwind components` e `@tailwind utilities`. |
| `public/` | Arquivos servidos estaticamente. Um arquivo `public/logo.png` fica acessível em `http://localhost:3000/logo.png`. |
| `next.config.ts` | Configurações avançadas do Next.js: variáveis de ambiente, redirects, headers, React Compiler, etc. |
| `tsconfig.json` | Configuração do TypeScript. Define o alias `@/*` mapeado para `./src/*`. |
| `biome.json` | Configuração unificada de lint e formatação de código (substitui ESLint + Prettier). |
| `postcss.config.mjs` | Necessário para o Tailwind CSS processar as classes utilitárias. |
| `package.json` | Lista de dependências e scripts do projeto (`dev`, `build`, `start`, `lint`, `format`). |

### Como o App Router funciona

No **App Router** do Next.js, a estrutura de pastas dentro de `src/app/` define as rotas da aplicação:

```
src/app/
├── page.tsx          → rota "/"
├── about/
│   └── page.tsx      → rota "/about"
├── blog/
│   ├── page.tsx      → rota "/blog"
│   └── [slug]/
│       └── page.tsx  → rota "/blog/:slug" (rota dinâmica)
└── dashboard/
    ├── layout.tsx    → layout aninhado para "/dashboard/*"
    └── page.tsx      → rota "/dashboard"
```

> 📘 **Referência:** [Fundamentos do App Router](https://nextjs.org/docs/app/building-your-application/routing)

### Como o alias `@/*` funciona

O alias `@/*` está configurado no `tsconfig.json`:

```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

Isso permite importar arquivos usando caminhos absolutos a partir de `src/`, evitando importações relativas longas:

```typescript
// ❌ Sem alias (caminho relativo difícil de manter)
import { Button } from "../../../components/ui/Button"

// ✅ Com alias @/*
import { Button } from "@/components/ui/Button"
```

---

## 8. Executar o projeto

### Modo desenvolvimento

```bash
npm run dev
```

Acesse [http://localhost:3000](http://localhost:3000) no navegador. O servidor recarrega automaticamente ao salvar arquivos.

> 💡 No Codespace, ao iniciar o servidor de desenvolvimento, o GitHub automaticamente cria um **port forwarding** e disponibiliza uma URL pública para visualização.

### Verificar lint e formatação

```bash
# Verificar e corrigir automaticamente lint + formatação
npm run check

# Apenas lint
npm run lint

# Apenas formatação
npm run format
```

### Build de produção

```bash
npm run build
npm run start
```

---

## 9. Links externos

### Next.js
- 📖 [Documentação oficial do Next.js](https://nextjs.org/docs)
- 🚀 [create-next-app — referência](https://nextjs.org/docs/app/api-reference/cli/create-next-app)
- 📂 [App Router — conceitos fundamentais](https://nextjs.org/docs/app/building-your-application/routing)
- 🖥️ [Server Components vs Client Components](https://nextjs.org/docs/app/building-your-application/rendering)

### React
- 📖 [Documentação oficial do React](https://react.dev/)
- ⚙️ [React Compiler](https://react.dev/learn/react-compiler)
- 🪝 [Hooks do React](https://react.dev/reference/react/hooks)

### TypeScript
- 📖 [Documentação oficial do TypeScript](https://www.typescriptlang.org/docs/)
- 🔧 [TypeScript com Next.js](https://nextjs.org/docs/app/building-your-application/configuring/typescript)

### Tailwind CSS
- 📖 [Documentação oficial do Tailwind CSS](https://tailwindcss.com/docs)
- 🎨 [Tailwind CSS com Next.js](https://tailwindcss.com/docs/guides/nextjs)

### Biome
- 📖 [Documentação oficial do Biome](https://biomejs.dev/docs/)
- ⚙️ [Configuração do Biome](https://biomejs.dev/reference/configuration/)
- 🔄 [Migrar do ESLint + Prettier para o Biome](https://biomejs.dev/guides/migrate-eslint-prettier/)

### GitHub
- 🐙 [GitHub Codespaces — documentação](https://docs.github.com/pt/codespaces)
- 📂 [Criando um repositório](https://docs.github.com/pt/repositories/creating-and-managing-repositories/creating-a-new-repository)
- 🌿 [Trabalhando com branches](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)

### Ferramentas relacionadas
- 🔺 [Vercel — plataforma de deploy para Next.js](https://vercel.com/docs)
- 🛠️ [VS Code — editor de código](https://code.visualstudio.com/)
- 📦 [npm — gerenciador de pacotes](https://docs.npmjs.com/)

---

<div align="center">
  <sub>Feito com ❤️ para fins didáticos — <a href="https://github.com/infoweb-pos">infoweb-pos</a></sub>
</div>
