---
description: Plano de implementação detalhado para uma feature nova, com especificação técnica
argument-hint: <descrição da feature>
---

Crie um plano de implementação detalhado para a feature abaixo. Stack: React + Vite + TypeScript + Tailwind + shadcn/ui + Supabase (banco, auth, RLS, Edge Functions), deploy na Vercel.

## Feature

$ARGUMENTS

## Antes de planejar

- Leia o `CLAUDE.md` do projeto e o `PRODUCT.md` se existir.
- Assuma **projeto Supabase compartilhado** com outros apps: isole por tabela com prefixo claro e RLS própria, não presuma que dá para criar um projeto Supabase novo.
- Respeite o workflow de Issue → branch → PR se o projeto exigir.

## Framework

### 1. Quebra da feature
User stories · requisitos técnicos · edge cases · critério de sucesso.

### 2. Especificação técnica

**Arquitetura**
- Onde encaixa em `src/` (componentes, hooks, contexto)
- Estado: quem é dono? (levantar estado para o pai, passar por props; Context só para auth/tema; Zustand só se realmente global)
- Fluxo de dados: `Ação do usuário → hook → Supabase (RLS) → estado → UI`

**Banco (Supabase)**
- Tabelas novas / colunas / índices (com prefixo do app)
- Policies RLS para cada operação (select/insert/update/delete)
- Relações N:N via tabela de junção
- Regenerar `src/lib/database.types.ts` após mudança de schema

**Libs**
- O que precisa instalar e por quê (⚠️ pedir aprovação antes de instalar)
- Alternativas consideradas

### 3. Passos de implementação
1. Schema + migration + RLS + regenerar types
2. Hooks de dados (`src/hooks/use-*.ts`)
3. Componentes e formulários (`src/components/`)
4. Estados: loading (skeleton), erro, vazio
5. Motion de entrada/saída/carregamento (ver skills de design do projeto)
6. Verificação: `npm run lint`, `npm run build`, teste no browser

### 4. Riscos
Técnicos · de tempo · de dependência externa · de dados/migration.

### 5. Critério de "pronto"
Funciona como especificado · `npm run build` sem erro · sem erro no console · acessível · responsivo · loading/erro/vazio tratados · `CLAUDE.md` atualizado se mudou arquitetura.

## Formato de saída

1. **Visão geral** — problema, público, funcionalidade principal
2. **Design técnico** — estrutura de componentes, hooks, schema, RLS, estado
3. **Plano por fase** com checkboxes e estimativa
4. **Arquivos novos / modificados** (caminhos reais em `src/`)
5. **Migrations** (SQL resumido)
6. **Libs a instalar** (para aprovar)
7. **Verificação e rollback**
8. **Primeiro passo**
