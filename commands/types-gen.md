---
description: Regenera os tipos TypeScript do schema do Supabase
argument-hint: [nome do projeto Supabase, se houver mais de um]
---

Regenere os tipos do banco a partir do schema atual do Supabase.

## Contexto

$ARGUMENTS

- O arquivo de tipos fica em **`src/lib/database.types.ts`** (não `lib/`).
- O projeto Supabase pode ser **compartilhado** com outros apps — gere os tipos do projeto certo e não apague tabelas de outro app do arquivo.
- Regenere **sempre** depois de: criar/alterar tabela, coluna, tipo, enum, ou relação.

## Como gerar

### Opção A — MCP do Supabase (preferida se disponível)
Use a ferramenta `generate_typescript_types` do MCP do Supabase apontando para o `project_id` correto e escreva o resultado em `src/lib/database.types.ts`.

### Opção B — CLI
```bash
npx supabase gen types typescript --project-id <PROJECT_ID> > src/lib/database.types.ts
# ou, com Supabase local:
npx supabase gen types typescript --local > src/lib/database.types.ts
```

## Depois de gerar

1. Confirme que o client é tipado: `createClient<Database>(url, key)` em `src/lib/supabase.ts`.
2. Rode `npx tsc -b --noEmit` — mudanças de schema costumam quebrar tipos em hooks/componentes; corrija.
3. Helper opcional em `src/lib/`:
   ```typescript
   export type Tables<T extends keyof Database['public']['Tables']> =
     Database['public']['Tables'][T]['Row']
   ```
4. Commite o arquivo gerado. **Nunca** edite `database.types.ts` à mão.
5. `npm run build` tem que passar.
