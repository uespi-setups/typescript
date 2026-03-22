# TypeScript Setup

Template profissional para projetos TypeScript com foco em qualidade, produtividade e integração com VS Code.

Inclui uma base pronta para desenvolvimento com:

- TypeScript strict
- ESLint
- Prettier
- Vitest
- Husky
- lint-staged
- Commit message validation
- Debug com VS Code
- Build para produção
- Alias de import
- GitHub Actions

## Objetivo

Este repositório fornece uma configuração base para projetos TypeScript com Node.js, organizada para oferecer:

- padronização de código
- validação automática de qualidade
- experiência consistente no VS Code
- pipeline simples para desenvolvimento, testes e build
- base reutilizável para novos projetos

## Requisitos

- Corepack habilitado
- Node.js 22
- Yarn 4

## Instalação

Clone o repositório e instale as dependências:

```bash
git clone git@github.com:uespi-setups/typescript.git
cd typescript
corepack enable
yarn install
```

Para confirmar as versões:

```bash
node -v
yarn -v
```

## Scripts disponíveis

### Desenvolvimento

Executa o projeto em modo de desenvolvimento:

```bash
yarn dev
```

### Build

Gera a versão compilada em `build/`:

```bash
yarn build
```

### Execução da build

Executa o código já compilado:

```bash
yarn start
```

### Verificação de tipos

Valida os tipos TypeScript dos arquivos de aplicação e teste:

```bash
yarn type:check
```

### Lint

Analisa o código com ESLint:

```bash
yarn lint
```

Versão para CI, falhando caso existam warnings:

```bash
yarn lint:ci
```

### Formatação

Formata todos os arquivos com Prettier:

```bash
yarn format
```

Valida se os arquivos já estão formatados:

```bash
yarn format:check
```

### Testes

Executa os testes:

```bash
yarn test
```

Executa os testes em modo watch:

```bash
yarn test:watch
```

Executa os testes com coverage:

```bash
yarn test:coverage
```

Versão usada na CI:

```bash
yarn test:ci
```

### Validação completa

Executa a validação local completa:

```bash
yarn check
```

Executa a validação completa usada na integração contínua:

```bash
yarn check:ci
```

## Estrutura do projeto

```text
.
├── .github/
│   └── workflows/
├── .husky/
├── .vscode/
├── src/
├── test/
├── .commitlintrc.cjs
├── .editorconfig
├── .env.example
├── .gitignore
├── .nvmrc
├── .prettierignore
├── .prettierrc
├── eslint.config.mjs
├── package.json
├── tsconfig.json
├── tsconfig.build.json
├── tsconfig.test.json
├── vitest.config.ts
└── README.md
```

## Configuração TypeScript

O projeto utiliza uma configuração TypeScript estrita para aumentar a segurança e reduzir erros em tempo de desenvolvimento.

### Arquivos principais

#### `tsconfig.json`

Usado para validação de tipos no ambiente de desenvolvimento.

Características:

- `strict: true`
- `noEmit: true`
- regras adicionais de segurança de tipos

#### `tsconfig.build.json`

Usado exclusivamente no processo de build.

Características:

- emite arquivos compilados
- define `rootDir` e `outDir`
- gera saída em `build/`

#### `tsconfig.test.json`

Usado para o contexto de testes.

## Alias de import

O projeto suporta alias para imports internos.

Exemplo:

```ts
import { hello } from '@src/utils/hello'
```

Esse alias é validado pelo TypeScript e reescrito no build com `tsc-alias`.

## Build e `tsc-alias`

O script de build deve usar o `tsconfig.build.json` explicitamente tanto no `tsc` quanto no `tsc-alias`.

Exemplo esperado no `package.json`:

```json
"build": "rimraf ./build && tsc -p ./tsconfig.build.json && tsc-alias -p ./tsconfig.build.json"
```

Isso é importante para garantir que o `tsc-alias` consiga localizar corretamente o `outDir`.

## VS Code

Este template inclui configuração para melhorar a experiência de desenvolvimento no VS Code.

### Recursos esperados

- formatação automática com Prettier
- integração com ESLint
- organização do workspace
- debug de arquivos TypeScript
- recomendações de extensões

### Extensões recomendadas

Ao abrir o projeto no VS Code, instale as extensões sugeridas pelo workspace.

### Seleção do TypeScript do workspace

Após abrir o projeto no VS Code, selecione a versão do TypeScript do workspace para garantir consistência com a configuração local do projeto.

## Variáveis de ambiente

O projeto inclui um arquivo de exemplo:

```bash
.env.example
```

Crie um arquivo `.env` com base nele:

```bash
cp .env.example .env
```

## Qualidade de código

Este setup aplica validações automáticas para manter consistência no projeto.

### ESLint

Responsável por análise estática e boas práticas.

### Prettier

Responsável por formatação de código.

### Husky

Executa hooks de Git automaticamente.

### lint-staged

Executa validações apenas nos arquivos staged no commit.

## Commits

O projeto possui validação de mensagens de commit.

Exemplo válido:

```bash
git commit -m "feat: add user service"
```

Exemplo inválido:

```bash
git commit -m "update files"
```

Se quiser ampliar o padrão para Conventional Commits completo, isso pode ser ajustado posteriormente.

## Testes

A base usa Vitest para execução dos testes.

Exemplo simples:

```ts
import { describe, expect, it } from 'vitest'

describe('sum', () => {
  it('should return 2 when adding 1 + 1', () => {
    expect(1 + 1).toBe(2)
  })
})
```

## Debug

A pasta `.vscode/` inclui configurações para facilitar o debug da aplicação no editor.

Casos comuns:

- debug do `main.ts`
- debug do arquivo atual
- uso de breakpoints diretamente em arquivos TypeScript

## CI

O projeto inclui workflow de GitHub Actions para validar:

- instalação das dependências
- formatação
- lint
- type check
- testes

A instalação deve usar Yarn 4 com:

```bash
yarn install --immutable
```

## Fluxo recomendado de uso

### 1. Instalar dependências

```bash
corepack enable
yarn install
```

### 2. Rodar o projeto em desenvolvimento

```bash
yarn dev
```

### 3. Validar qualidade

```bash
yarn check
```

### 4. Gerar build

```bash
yarn build
```

### 5. Executar build

```bash
yarn start
```

## Roteiro rápido de validação do setup

### Instalação limpa

```bash
rm -rf node_modules
yarn install --immutable
```

### Type check

```bash
yarn type:check
```

### Lint

```bash
yarn lint
```

### Formatação

```bash
yarn format:check
```

### Testes

```bash
yarn test
```

### Coverage

```bash
yarn test:coverage
```

### Build

```bash
yarn build
```

### Execução da build

```bash
yarn start
```

### Validação completa

```bash
yarn check:ci
```

## Para quem este template é indicado

Este setup é indicado para:

- APIs Node.js com TypeScript
- serviços backend
- projetos acadêmicos com padrão profissional
- templates internos de equipe
- bases reutilizáveis para novos sistemas

## Melhorias futuras possíveis

Sugestões que podem ser adicionadas depois, dependendo do objetivo do projeto:

- Docker e Docker Compose
- integração com PostgreSQL
- commitlint mais completo
- release automation
- changelog automático
- testes de integração
- cobertura mínima obrigatória por arquivo
- arquitetura em camadas
- exemplos prontos de módulos de domínio

## Licença

Este projeto está licenciado sob a licença MIT.
