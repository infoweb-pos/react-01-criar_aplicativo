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
| **Navegador moderno** | **Chrome**, Edge, Firefox ou Safari atualizado. O Codespace roda 100% no navegador. |
| **Conhecimentos básicos** | HTML, CSS, JavaScript e noções de terminal/linha de comando. |

> 💡 **Dica:** Não é necessário instalar nada na sua máquina. O GitHub Codespace fornece um ambiente de desenvolvimento completo na nuvem com Node.js, npm e todas as ferramentas necessárias.

---

## 2. Criar o repositório no GitHub

1. Acesse [github.com](https://github.com) e faça login.

2. Clique no botão **"New"** (ou acesse diretamente [github.com/new](https://github.com/new)).

3. Preencha as informações do repositório:
   - **Repository name:** `meu-app-front` (ou o nome que preferir)
   - **Description:** `Aplicativo web React com Next.js` (opcional)
   - **Visibility:** `Public`
   - ✅ Desmarque **"Add a README file"**

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

> O `.` indica que o app será criado na raiz do repositório atual.


### 4.2 Respondendo as perguntas do `create-next-app`

O assistente interativo fará uma série de perguntas. Responda conforme abaixo:

> Provável que apareça a pergunta abaixo.
> Responda que sim digitando a tecla `y` seguido de `ENTER`. 
> O aplicativo `npx` esta solicitando baixar a última versão do script `create-next-app`.

```bash
Need to install the following packages:
create-next-app@16.1.6
Ok to proceed? (y)

```

> Próxima pergunta, o `create-next-app` sugere criar um projeto com as configurações padronizadas.
> Usando a seta para baixo, selecione `No, customize settings - Choose your own preferences` e pressione `ENTER`.
> Fazendo isso vamos configurar nosso projeto com nossas necessidades.

```bash
Need to install the following packages:
create-next-app@16.1.6
Ok to proceed? (y)

? Would you like to use the recommended Next.js defaults? › - Use arrow-keys. Return to submit.
    Yes, use recommended defaults
❯   No, customize settings - Choose your own preferences

```

> A medida que as perguntas são respondidas, o `create-next-app` vai fazendo o cheque com o caractere `✔` e adicionando nova pergunta com o `?`, conforme terminal abaixo.
> Para a pergunta de uso do `Typescript`, responda `Yes` usando ou a seta pro lado ou digitando `y` seguido de um `ENTER`.

```
Need to install the following packages:
create-next-app@16.1.6
Ok to proceed? (y) y

✔ Would you like to use the recommended Next.js defaults? › No, customize settings
? Would you like to use TypeScript? › No / Yes

```

> O terminal abaixo mostra as perguntas e respostas.
> A tabela abaixo segue com as explicações das respostas.

```bash
Need to install the following packages:
create-next-app@16.1.6
Ok to proceed? (y) y

✔ Would you like to use the recommended Next.js defaults? › No, customize settings
✔ Would you like to use TypeScript? … Yes
✔ Which linter would you like to use? › Biome
✔ Would you like to use React Compiler? … Yes
✔ Would you like to use Tailwind CSS? …  Yes
✔ Would you like your code inside a `src/` directory? … Yes
✔ Would you like to use App Router? (recommended) … Yes
✔ Would you like to customize the import alias (`@/*` by default)? … Yes
✔ What import alias would you like configured? … @/*

```
| Opção                    | Escolha | Motivo |
|--------------------------|---------|--------|
| **TypeScript**           | `Yes`   | Tipagem estática melhora a qualidade do código. |
| **linter**.              | `No`    | Será utilizado o **Biome**, que faz lint e formatação em um único pacote. |
| **React Compiler**       | `Yes`   | |
| **Tailwind CSS**         | `Yes`   | Framework CSS utilitário, muito produtivo para estilização. |
| **`src/`**               | `Yes`   | Organiza o código-fonte separado dos arquivos de configuração. |
| **App Router**           | `Yes`   | Roteamento moderno do Next.js com suporte a Server Components. |
| **customize the import** | `Yes`   | Permite definir _alias_ para utilizar nas importações. | 
| **Import alias**         | `@/*`   | Permite importar com `@/components/...` em vez de `../../components/...`. |

Aguarde a instalação das dependências. Ao final, você verá:

```
✔ Success! Created meu-app-front at /workspaces/meu-app-front
```

---

## 5. Executando o projeto

### Modo desenvolvimento

```bash
npm run dev
```

> A saída esperada será como terminal abaixo.

```bash
> meu_app-front@0.1.0 dev
> next dev

▲ Next.js 16.1.6 (Turbopack)
- Local:         http://localhost:3000
- Network:       http://10.0.11.47:3000

✓ Starting...
Attention: Next.js now collects completely anonymous telemetry regarding usage.
This information is used to shape Next.js' roadmap and prioritize features.
You can learn more, including how to opt-out if you'd not like to participate in this anonymous program, by visiting the following URL:
https://nextjs.org/telemetry

✓ Ready in 1010ms
```

Apesar do Next/React abrir a porta 3000 com o endereço `localhost:3000`, lembre que você esta no code space que é uma máquina virtual num servidor na infraestrutura do github.
O code space verifica que você abriu uma porta no computador virtual e pergunta se você deseja abrir o endereço no navegador.
Responda que `abrir no navegador` e ele deverá abrir uma nova aba com um endereço estranho, no meu computador / repositório no momento deste tutorial foi o endereço `https://ideal-xylophone-pj7jp57rvrh75-3000.app.github.dev/`.

> 💡 No Codespace, ao iniciar o servidor de desenvolvimento, o GitHub automaticamente cria um **port forwarding** e disponibiliza uma URL pública para visualização.

---

## 6. Entendendo o projeto

### Estrutura de diretórios do projeto

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
├── package-lock.json            # Lock file das dependências exatas (gerado automaticamente, não commitar)
├── postcss.config.mjs           # Configuração do PostCSS (usado pelo Tailwind)
├── public/                      # Arquivos estáticos públicos (imagens, fontes, ícones)
│   ├── file.svg
│   ├── globe.svg
│   ├── next.svg
│   ├── vercel.svg
│   └── window.svg
├── README.md                    # Documentação do projeto (devemos sempre atualizar as inf daqui)
├── src/                         # Código-fonte da aplicação
│   └── app/                     # Diretório do App Router
│       ├── favicon.ico          # Ícone da aba do navegador
│       ├── globals.css          # Estilos globais (inclui diretivas do Tailwind)
│       ├── layout.tsx           # Layout raiz da aplicação (HTML + Body)
│       └── page.tsx             # Página inicial (rota "/")
└── tsconfig.json                # Configuração do TypeScript
```

### Descrição dos principais arquivos e diretórios

| Caminho               | Descrição |
|-----------------------|-----------|
| `public/`.            | Arquivos servidos estaticamente. Um arquivo `public/logo.png` fica acessível em `http://localhost:3000/logo.png`. |
| `src/app/`            | Contém todas as rotas e layouts da aplicação (App Router). Cada pasta cria uma rota. |
| `src/app/layout.tsx`  | Layout raiz: define as tags `<html>` e `<body>`, fontes globais e metadados padrão. Envolve todas as páginas. |
| `src/app/page.tsx`    | Componente da rota raiz (`/`). É o que aparece ao acessar `http://localhost:3000`. |
| `src/app/globals.css` | Estilos globais. Contém as diretivas `@tailwind base`, `@tailwind components` e `@tailwind utilities`. |
| `biome.json`          | Configuração unificada de lint e formatação de código (substitui ESLint + Prettier). |
| `next.config.ts`      | Configurações avançadas do Next.js: variáveis de ambiente, redirects, headers, React Compiler, etc. |
| `package.json`       | Lista de dependências e scripts do projeto (`dev`, `build`, `start`, `lint`, `format`). |
| `postcss.config.mjs` | Necessário para o Tailwind CSS processar as classes utilitárias. |
| `tsconfig.json`       | Configuração do TypeScript. Define o alias `@/*` mapeado para `./src/*`. |

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

### Modificando a página inicial

Aos curiosos, as modificações podem ser realizadas inicialmente no arquivo `/src/app/page.tsx`.
Arquivos `.ts` são arquivos Typescript enquanto `.tsx` são arquivos React com Typescript.

De uma forma geral, e resumida ao extremo do extremo, arquivos `.tsx` devem conter componentes (que podem ser usado externamente ou não) React, sendo obrigatório pelo menos 1.

Componentes React são tem como valor de saída um JSX, sintaxe extendida do HTML.
Para maiores informações sobre JSX, ou aguarda o momento na sala ou dá uma olhada em [Writing markup with JSX](https://react.dev/learn/writing-markup-with-jsx) ou pergunta ao assistente(s) IA de sua preferência.

Se já for usar [tailwind css](https://tailwindcss.com/), pode começar com o [Styling with utility classes](https://tailwindcss.com/docs/styling-with-utility-classes) ou pedir sugestão ao(s) assistente(s) IA.
Lembre de instalar a extensão no code space `Tailwind CSS IntelliSense`. Ela ajudará no auto completar.

---

## 7. Publicando o projeto no repositório (push)


### Configure o .gitignore

> Adicione o package-lock.json em .gitignore
> Abaixo esta somente o início do arquivo .gitignore


```git
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.
package-lock.json

```

### Marque e guardar os arquivos no repositório, e publicar no github

```terminal
codespace:/workspaces/meu_app-front> git add .
codespace:/workspaces/meu_app-front> git commit -m "adicionado aplicação inicial"
[main 91a6483] adicionado aplicação inicial
 16 files changed, 321 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 biome.json
 create mode 100644 next.config.ts
 create mode 100644 package.json
 create mode 100644 postcss.config.mjs
 create mode 100644 public/file.svg
 create mode 100644 public/globe.svg
 create mode 100644 public/next.svg
 create mode 100644 public/vercel.svg
 create mode 100644 public/window.svg
 create mode 100644 src/app/favicon.ico
 create mode 100644 src/app/globals.css
 create mode 100644 src/app/layout.tsx
 create mode 100644 src/app/page.tsx
 create mode 100644 tsconfig.json
codespace:/workspaces/meu_app-front> git push
Enumerating objects: 22, done.
Counting objects: 100% (22/22), done.
Delta compression using up to 2 threads
Compressing objects: 100% (20/20), done.
Writing objects: 100% (21/21), 15.30 KiB | 3.83 MiB/s, done.
Total 21 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/leonardo-minora/meu_app-front
   2847cfd..91a6483  main -> main
codespace:/workspaces/meu_app-front> 
```

---

## 8. Outras informações

### Biome

O [Biome](https://biomejs.dev/) é uma ferramenta de **lint e formatação** para JavaScript/TypeScript extremamente rápida, escrita em Rust.
Ele substitui ESLint + Prettier com uma única dependência.

O biome já vem instalado e configurado para nosso projeto.
Para detalhes sobre a configuração do biome, ver o arquivo `biome.json` na raiz do projeto e consultar o docs no site do projeto.

O biome também já esta pronto para ser executado via linha de comando:
- `npm run check` : Executa a formatação, linter e ordenação das importações.
- `npm run lint` : Executa verificações nos códigos-fontes.
- `npm run format` : Executa a formatação dos códigos-fonte.

---

### React Compiler

O [React Compiler](https://react.dev/learn/react-compiler) (anteriormente chamado de "React Forget") é uma ferramenta experimental que **otimiza automaticamente** componentes React, eliminando a necessidade de `useMemo`, `useCallback` e `React.memo` na maioria dos casos.

Para Verificar se o compilador está funcionando, execute o _build_:

```bash
npm run build
```

> 📘 **Referência:** [React Compiler — documentação oficial](https://react.dev/learn/react-compiler)


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
  <sub>Feito pelo copilot e revisado pelo professor com ❤️ para fins didáticos para <a href="https://github.com/infoweb-pos">infoweb-pos</a></sub>
</div>
