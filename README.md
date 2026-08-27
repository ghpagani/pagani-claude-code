# pagani-claude-code

Setup pessoal do Pagani para o [Claude Code](https://docs.claude.com/en/docs/claude-code): comandos e agentes afinados para a stack **React + Vite + TypeScript + Tailwind + shadcn/ui + Supabase + Vercel**.

> Base reutilizável para projetos novos. Overrides específicos de um projeto ficam no `.claude/` daquele repositório e têm prioridade sobre este plugin.

## Instalação

```
/plugin marketplace add ghpagani/pagani-claude-code
/plugin install pagani-claude-code@pagani-claude-code
```

Reinicie o Claude Code depois de instalar. Para atualizar: `/plugin update pagani-claude-code`.

## Comandos (12)

| Comando | O que faz |
|---|---|
| `/new-task <tarefa>` | Analisa a tarefa e gera plano de implementação |
| `/feature-plan <feature>` | Plano detalhado com spec técnica (schema, RLS, hooks, estados) |
| `/component-new <nome>` | Componente React (SPA Vite) com TS, Tailwind, shadcn |
| `/code-explain <alvo>` | Explica um trecho de TS/React de forma progressiva |
| `/code-optimize <alvo>` | Otimiza performance (re-render, query, bundle) — mede antes |
| `/code-cleanup <alvo>` | Refatora preservando comportamento |
| `/lint [alvo]` | Roda oxlint + `tsc` e corrige |
| `/docs-generate <alvo>` | TSDoc, README, notas de componente |
| `/types-gen` | Regenera `src/lib/database.types.ts` do Supabase |
| `/edge-function-new <nome>` | Supabase Edge Function (Deno) com auth, validação, CORS |
| `/rls-policy <tabela>` | Escreve/revisa policies RLS |
| `/supabase-migration <mudança>` | Migration SQL isolada por prefixo de app |

## Agentes (11)

**Arquitetura & planejamento:** `tech-stack-researcher`, `system-architect`, `backend-architect`, `frontend-architect`, `requirements-analyst`
**Qualidade:** `refactoring-expert`, `performance-engineer`, `security-engineer`
**Comunicação & pesquisa:** `technical-writer`, `learning-guide`, `deep-research-agent`

Os agentes ativam por contexto ou por invocação explícita (`@agent-<nome>`).

## MCP servers

Definidos em `.mcp.json`: `context7` (docs de libs) e `playwright` (browser). Sem configuração.

Para acesso ao Supabase, use a conexão Supabase da sua conta Claude (já integrada). Se preferir um servidor Supabase local dedicado por projeto, veja [`docs/MCP-SERVERS.md`](docs/MCP-SERVERS.md).

## Premissas da stack

- SPA React 19 + Vite — **sem** Next.js, SSR ou Server Components
- TypeScript estrito, sem `any`, literal unions em vez de `enum`
- Comentários em português
- Nunca commitar segredos / `.env`
- Não instalar biblioteca sem aprovação
- `npm run build` (= `tsc -b && vite build`) tem que passar antes de finalizar
- Projeto Supabase geralmente **compartilhado** entre apps — isolar por prefixo de tabela / schema
- Deploy na Vercel a partir de merge de PR

Ver [`docs/PUBLISHING.md`](docs/PUBLISHING.md) para publicar/atualizar. Licença: MIT.
