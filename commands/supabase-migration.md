---
description: Cria uma migration SQL do Supabase, isolada por prefixo do app
argument-hint: <o que a migration muda>
---

Crie uma migration para o Supabase. Como o projeto Supabase pode ser **compartilhado** entre apps, toda mudança precisa ser isolada e reversível.

## Mudança

$ARGUMENTS

## Regras de isolamento

- Tabelas e tipos com **prefixo do app** (`estudos_`, `cofre_`, ...) — ou schema dedicado (`create schema <app>`), se preferir.
- Nunca `drop`/`alter` tabela que não seja do app.
- Toda tabela nova: `enable row level security` + policies na mesma migration (use `/rls-policy`).
- FK para `auth.users` com `on delete cascade` quando a linha pertence ao usuário.

## Estrutura

```sql
-- supabase/migrations/<timestamp>_<descricao_curta>.sql

-- 1. schema / tabelas
create table if not exists estudos_<nome> (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users on delete cascade,
  -- colunas...
  created_at timestamptz not null default now()
);

-- 2. índices (colunas de filtro/ordenação/FK)
create index if not exists estudos_<nome>_user_id_idx on estudos_<nome> (user_id);

-- 3. RLS
alter table estudos_<nome> enable row level security;
create policy "estudos_select_own" on estudos_<nome> for select using (auth.uid() = user_id);
-- ...demais policies

-- 4. dados seed (só se for catálogo curado)
```

## Fluxo

```bash
npx supabase migration new <descricao>     # cria o arquivo
# editar o SQL
npx supabase db push                       # aplica no projeto remoto
```
Ou aplique via ferramenta `apply_migration` do MCP do Supabase (com o `project_id` certo).

## Depois

1. `/types-gen` — regenerar `src/lib/database.types.ts`
2. `npx tsc -b --noEmit` e `npm run build`
3. Rodar `get_advisors` (MCP) para checar problemas de segurança/performance no schema novo

## Saída
1. SQL da migration completo
2. Rollback (o que rodar para desfazer)
3. Passos pós-migration
