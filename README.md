# Criando uma Aplicação do Zero a Nuvem Usando o TurboRepo

## NEXT.JS (Renderização React no Lado Servidor)


### Repositório em comum para várias aplicações e utilizando os serviços da Vercel.

<p>TuboRepo é uma ferramenta de build que te ajuda manter dentro de um único repositório vários projetos.</p>
<p>Existe uma questão de dependência, pode utilizar, por exemplo, uma pasta <b><i>common</i></b>, e nesse projeto, você tem uma série de códigos e componentes visuais que você quer compartilhar em vários projetos e é nesse aspécto que o TurboRepo entra.</p>

<p>Ele consegue entender todas as dependências do seu projeto e fazer build na ordem certa, paralelizar o build e você consegue colocar dentro de um mesmo diretório, por exemplo, vários projetos.</p>

- Area administrativa
- Área do Cliente
- Área do entregadores 
- Restaurante
- Área de entregas
- Área dos clientes
- Etc

<p>Projetos diferentes e ainda sim, compartilhar um trecho de código específico entre esses vários projetos</p>


<b>Exemplo no link:<b> https://turborepo.brasilnarede.com.br/



Vídeo tutorial: https://www.youtube.com/watch?v=SQy5we_2L7Y

### Criar aplicação:
```sh
npx create-turbo@latest
```

<i>? Where would you like to create your turborepo?</i> `.`<br />
<i>? Which package manager do you want to use?</i> `yarn workspaces`<br />

Sugestão: `npx turbo login`

Para conectar-se ao seu cache remoto, execute o seguinte em qualquer turborepo: npx turbo link
 

### Instale a versão mais recente doturbo
```sh
yarn add turbo --save-dev --ignore-workspace-root-check
```

### Rodar Aplicação:
```sh
npm run dev
```

Acesso pelo browser:<br />
http://localhost:3000 (examples/basic web) <br />
http://localhost:3001 (examples/basic docs) <br />


https://tsdx.io/
```sh
cd .\packages\ 
```
```sh
npx tsdx create shared
```

```sh
cd .\shared\
```
```sh 
npm start 
```
or 
```sh
yarn start
```

### Build na pasta raiz:
```sh
npm run build
```

<b>Corrigir erro:</b> <i>Error: Parsing error: DeprecationError: 'originalKeywordKind' has been deprecated since v5.0.0 and can no longer be used. Use 'identifierToKeywordKind(identifier)' instead.</i>

```sh
npm install @typescript-eslint/eslint-plugin --save-dev
npm install @typescript-eslint/parser --save-dev
```

### DEPLOY
#### Comandos config site VERCEL
https://vercel.com/<br />

Obs.: Atualizar o arquivo yarn.lock com esse comando quando ocorrer erro no DEPLOY:
```sh
npm update
```

#### Root Directory:
`apps/web`<br />

#### Build Command:
`cd ../.. && npm run build:web`<br />

turbo run build --scope=*build-tools* --no-deps --includeDependencies<br />
turbo run build --scope=*build-tools* --no-deps --include-dependencies<br />
package.json<br />
  "scripts": {<br />
    <b>"build:web": "turbo run build --scope=web --no-deps --include-dependencies",</b><br />
    ...<br />

#### Output Directory:
`Next.js default`<br />

#### Install Command:
`yarn install`

#### Development Command:
`next`<br />


## Install Tailwind CSS with Next.js
https://www.youtube.com/watch?v=NYhOkNLV6KM <br />
https://tailwindcss.com/docs/guides/nextjs <br />


### Precisa fazer a instalação nos projetos, tanto no PACKAGES/* (PACKAGES/UI), quanto no APPS/* (APPS/DOCS e APPS/WEB)

<b>-w</b> é workspace que eu quero utilizar, <b>'packages/ui'</b> onde eu quero criar.<br />
será criado: <b>packages/ui/node_modules/postcss</b>, o resto, compartilha com outros projetos:<br /> 
<br /><br />
<b>pakages/ui/package.json, apps/docs/package.json e apps/web/package.json:</b><br />
{<br />
"tailwindcss": "^3.3.6",<br />
...<br />
<br />

```sh
npm install -D tailwindcss postcss autoprefixer -w='packages/ui'
```
```sh
npm install -D tailwindcss postcss autoprefixer -w='apps/docs'
```
```sh
npm install -D tailwindcss postcss autoprefixer -w='apps/web'
```

<br /><br />
Esse comando deve ser feito em cada projeto:<br />
cd apps/web/<br />
cd apps/docs/<br />
cd package/ui/<br />

```sh
npx tailwindcss init -p
```

Agora, todos os projetos com  "postcss.config.js" e "tailwind.config.js"<br />
Alterar em todas as pastas dos projetos o arquivo tailwind.config.js:<br />
de :<br />
content: [],<br />
<br />

para (apps/docs e apps/web):<br />
  content: [<br />
    "./app/**/*.{html,js,ts,jsx,tsx}",<br />
    "./components/**/*.{html,js,ts,jsx,tsx}",<br />
    "../../packages/ui/**/*.{html,js,ts,jsx,tsx}"<br />
  ],<br />
<br />
<br />
para (packages/ui):<br />
  content: [<br />
    "./**/*.{html,js,ts,jsx,tsx}"<br />
  ],<br />
<br />



* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 

# Turborepo starter

This is an official starter Turborepo.

## Using this example

Run the following command:

```sh
npx create-turbo@latest
```

## What's inside?

This Turborepo includes the following packages/apps:

### Apps and Packages

- `docs`: a [Next.js](https://nextjs.org/) app
- `web`: another [Next.js](https://nextjs.org/) app
- `@repo/ui`: a stub React component library shared by both `web` and `docs` applications
- `@repo/eslint-config`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `@repo/typescript-config`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).

### Utilities

This Turborepo has some additional tools already setup for you:

- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting

### Build

To build all apps and packages, run the following command:

```
cd my-turborepo
pnpm build
```

### Develop

To develop all apps and packages, run the following command:

```
cd my-turborepo
pnpm dev
```

### Remote Caching

Turborepo can use a technique known as [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching) to share cache artifacts across machines, enabling you to share build caches with your team and CI/CD pipelines.

By default, Turborepo will cache locally. To enable Remote Caching you will need an account with Vercel. If you don't have an account you can [create one](https://vercel.com/signup), then enter the following commands:

```
cd my-turborepo
npx turbo login
```

This will authenticate the Turborepo CLI with your [Vercel account](https://vercel.com/docs/concepts/personal-accounts/overview).

Next, you can link your Turborepo to your Remote Cache by running the following command from the root of your Turborepo:

```
npx turbo link
```

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turbo.build/repo/docs/core-concepts/monorepos/running-tasks)
- [Caching](https://turbo.build/repo/docs/core-concepts/caching)
- [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching)
- [Filtering](https://turbo.build/repo/docs/core-concepts/monorepos/filtering)
- [Configuration Options](https://turbo.build/repo/docs/reference/configuration)
- [CLI Usage](https://turbo.build/repo/docs/reference/command-line-reference)
