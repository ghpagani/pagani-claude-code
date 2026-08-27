---
description: Roda lint e type-check (oxlint + tsc) e corrige os problemas
argument-hint: [pasta ou arquivo opcional]
---

Rode as verificações de qualidade do projeto e corrija o que der. A stack usa **oxlint** (não ESLint) e o type-check do `tsc`.

## Alvo

$ARGUMENTS

## Passos

### 1. Rodar
```bash
npm run lint          # oxlint
npx tsc -b --noEmit   # type-check (o build do projeto é `tsc -b && vite build`)
npm run build         # confirma que compila de ponta a ponta
```

### 2. Categorias de problema

**TypeScript**
- `any` implícito ou explícito
- Variáveis/imports não usados
- Tipos de retorno frouxos
- Narrowing faltando

**React (regras do oxlint)**
- `key` faltando em listas
- Dependências de `useEffect` / `useCallback` / `useMemo`
- Entidades não escapadas no JSX
- Hook chamado condicionalmente

**Qualidade**
- `console.log` / `debugger` esquecidos
- `var` → `const`/`let`
- Ternário aninhado
- Código inalcançável

### 3. Correção
- Aplique as correções seguras automaticamente.
- Para o resto, liste com arquivo:linha, o problema e a correção proposta.
- **Não** desative regra do oxlint para "passar" — corrija a causa, ou pergunte.

### 4. Prioridade
1. Erros que quebram o `build`
2. `any` / tipos frouxos / deps de effect erradas
3. Estilo e código morto

## Saída
1. **Resumo** — quantos problemas, por categoria
2. **Corrigido automaticamente** — lista
3. **Precisa de decisão** — arquivo:linha + proposta
4. Confirmação de que `npm run build` passa no final
