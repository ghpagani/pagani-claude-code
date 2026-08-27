---
description: Gera documentação (TSDoc, README, notas de componente) para o código
argument-hint: <arquivo, módulo ou "README">
---

Gere documentação para o código abaixo. Escreva para "você daqui a 6 meses". Documente o *porquê*, não o óbvio. Comentários e prosa em português.

## Alvo

$ARGUMENTS

## Tipos

**TSDoc** (funções/hooks exportados)
```typescript
/**
 * Busca o perfil do estudante logado.
 *
 * @param userId - id de `auth.users`
 * @returns o perfil, ou `null` se ainda não foi criado
 * @throws quando a query do Supabase falha (não trata RLS negada — trate no caller)
 *
 * @example
 * const { data } = useStudentProfile(user.id)
 */
```

**Nota de componente** (props com descrição)
```typescript
interface UserCardProps {
  /** Dados do usuário a exibir */
  user: User
  /** Callback ao clicar em editar */
  onEdit?: () => void
  /** Mostra os botões de ação (default: false) */
  showActions?: boolean
}
```

**README** (seções relevantes para uma SPA Vite + Supabase)
- O que o projeto faz
- Stack (React + Vite + TS + Tailwind + shadcn + Supabase + Vercel)
- Setup: `npm install`, `.env` (`VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`), nunca commitar `.env`
- Scripts: `npm run dev` / `build` / `lint` / `preview`
- Estrutura de `src/`
- Deploy: merge de PR na `main` → Vercel

## O que gerar
1. TSDoc para o que está exportado
2. Descrição das props (se for componente)
3. Trecho de README (se pedido)
4. Exemplos de uso reais do projeto
5. "Gotchas" — o que costuma dar errado

Não documente o óbvio. Se algo só é claro com um comentário de *por que*, esse é o comentário que importa.
