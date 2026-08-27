---
description: Cria um componente React novo (Vite SPA) com TypeScript, Tailwind e shadcn/ui
argument-hint: <nome e descrição do componente>
---

Gere um componente React seguindo os padrões de uma SPA React 19 + Vite (sem Next.js, sem Server Components, sem `'use client'`).

## Especificação

$ARGUMENTS

## Padrões

### Estrutura
- Function component, nomeado, export nomeado (`export function NomeDoComponente`).
- Arquivo em `src/components/` com kebab-case (`user-card.tsx`); componentes de UI base em `src/components/ui/` são do shadcn — **não editar à mão**.
- Comentários em português.

### TypeScript
- `interface Props` explícita; sem `any`.
- Preferir literal unions a `enum` (regra do projeto).
- Utility types quando fizer sentido (`Pick`, `Omit`, `ComponentProps<'button'>`).
- Destructuring na assinatura, com defaults.

### Estado e dados
- `useState` para estado local, `useReducer` para estado complexo.
- Busca de dados via hook dedicado (`src/hooks/use-*.ts`) usando o client Supabase de `src/lib/supabase.ts` — não buscar direto dentro do componente de UI.
- Estado compartilhado: dono único no componente pai, passado por props. Context só para auth/tema.

### Estilo
- Tailwind (v4, tokens de tema do shadcn em `src/index.css`).
- Usar o helper `cn()` de `src/lib/utils.ts` para classes condicionais.
- Seguir a linha visual definida no `CLAUDE.md` do projeto (ex.: premium/agency via skill `high-end-visual-design`). Não misturar direções visuais.

### Estados obrigatórios
- Loading → skeleton (não spinner solto), com animação suave.
- Erro → mensagem clara, ação de retry quando aplicável.
- Vazio → empty state com orientação do próximo passo.

### Acessibilidade
HTML semântico · `aria-*` onde necessário · navegação por teclado · foco visível.

### Motion
Entrada/saída/transição suaves; respeitar `prefers-reduced-motion`. Ver skills `animate` / `emil-design-eng` se instaladas no projeto.

## O que gerar

1. Arquivo do componente com Props tipadas
2. Hook de dados separado, se o componente precisar de dados
3. Exemplo de uso (import + JSX)
4. Notas de acessibilidade

Mantenha o componente pequeno (<200 linhas); extraia lógica para hooks. Rode `npm run lint` e `npm run build` no final.
