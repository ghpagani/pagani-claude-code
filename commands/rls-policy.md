---
description: Escreve ou revisa policies RLS do Supabase para uma tabela
argument-hint: <tabela e quem pode fazer o quê>
---

Escreva (ou revise) as policies de Row Level Security para a tabela abaixo. Numa SPA + Supabase, **o RLS é a camada de segurança** — o client tem a anon key, então tudo que protege os dados está nas policies.

## Alvo

$ARGUMENTS

## Antes de escrever

- Confirme o schema real da tabela (colunas, FKs, quem é o "dono" da linha).
- Projeto Supabase possivelmente **compartilhado**: a tabela deve ter dono claro (`user_id uuid references auth.users`) e as policies não podem vazar dados entre apps.
- `alter table <t> enable row level security;` — sem isso, nenhuma policy vale.

## Padrões

**Dono da linha (perfil, dados do usuário)**
```sql
create policy "<app>_select_own" on <tabela>
  for select using (auth.uid() = user_id);

create policy "<app>_insert_own" on <tabela>
  for insert with check (auth.uid() = user_id);

create policy "<app>_update_own" on <tabela>
  for update using (auth.uid() = user_id) with check (auth.uid() = user_id);

create policy "<app>_delete_own" on <tabela>
  for delete using (auth.uid() = user_id);
```

**Leitura pública, escrita bloqueada (catálogo curado)**
```sql
create policy "<app>_public_read" on <tabela> for select using (true);
-- sem policy de insert/update/delete: só service role / migration escreve
```

**Tabela de junção N:N** — checar posse pela linha pai:
```sql
create policy "<app>_select_own_junction" on <juncao>
  for select using (
    exists (select 1 from <pai> p where p.id = <juncao>.<pai>_id and p.user_id = auth.uid())
  );
```

## Regras
- Uma policy por operação (não `for all`) — fica explícito e auditável.
- `using` (linhas visíveis) **e** `with check` (linhas que pode gravar) em update; `with check` em insert.
- Testar cada policy: como o dono, como outro usuário, como anônimo.
- Cuidado com recursão em policy que consulta a própria tabela.

## Saída
1. SQL das policies (pronto para virar migration)
2. Explicação de cada uma (quem pode o quê)
3. Casos de teste (dono / terceiro / anônimo → esperado)
4. Riscos (colunas sensíveis expostas, junção sem checagem de posse)
