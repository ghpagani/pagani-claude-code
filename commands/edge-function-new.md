---
description: Cria uma Supabase Edge Function (Deno) com auth, validação e CORS
argument-hint: <nome e propósito da function>
---

Crie uma Supabase Edge Function. Rodam em Deno (não Node), globalmente na edge. Use para lógica que **não pode** viver no client: segredos de terceiros, webhooks, operações com service role, tarefas agendadas.

## Especificação

$ARGUMENTS

## Contexto

- Projeto Supabase possivelmente **compartilhado**: nomeie a function com prefixo do app (`<app>-<nome>`), e toda query deve respeitar o escopo do app.
- Frontend chama via `supabase.functions.invoke('<app>-<nome>', { body })`.

## Estrutura

```typescript
// supabase/functions/<app>-<nome>/index.ts
import { serve } from 'https://deno.land/std@0.224.0/http/server.ts'
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'

const cors = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Headers': 'authorization, content-type',
  'Access-Control-Allow-Methods': 'POST, OPTIONS',
}

serve(async (req) => {
  if (req.method === 'OPTIONS') return new Response('ok', { headers: cors })

  try {
    const supabase = createClient(
      Deno.env.get('SUPABASE_URL')!,
      Deno.env.get('SUPABASE_ANON_KEY')!,
      { global: { headers: { Authorization: req.headers.get('Authorization')! } } },
    )

    const { data: { user } } = await supabase.auth.getUser()
    if (!user) {
      return new Response(JSON.stringify({ error: 'Não autorizado' }), {
        status: 401, headers: { ...cors, 'Content-Type': 'application/json' },
      })
    }

    const body = await req.json()
    // TODO: validar body antes de qualquer operação

    const result = await handle(body, user, supabase)

    return new Response(JSON.stringify({ data: result }), {
      status: 200, headers: { ...cors, 'Content-Type': 'application/json' },
    })
  } catch (err) {
    console.error(err)
    return new Response(JSON.stringify({ error: 'Erro interno' }), {
      status: 500, headers: { ...cors, 'Content-Type': 'application/json' },
    })
  }
})
```

## Regras
- Validar todo input antes de tocar no banco.
- `service_role` só quando o RLS não dá conta; nunca expor a key.
- Nunca vazar detalhe de erro no response (log server-side, mensagem genérica pro client).
- Uma responsabilidade por function; helpers em `supabase/functions/_shared/`.

## Fluxo
```bash
npx supabase functions new <app>-<nome>
npx supabase functions serve <app>-<nome>          # local
npx supabase functions deploy <app>-<nome>         # deploy
npx supabase secrets set CHAVE=valor               # segredos
```

## Saída
1. Arquivo `index.ts` completo
2. Schema de validação do body
3. Exemplo de chamada do frontend com `supabase.functions.invoke`
4. Lista de secrets a configurar
