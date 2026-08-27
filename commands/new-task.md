---
description: Analisa uma tarefa e cria um plano de implementação acionável
argument-hint: <descrição da tarefa>
---

Analise a tarefa abaixo e produza um plano de implementação claro e acionável para um dev solo trabalhando numa stack React + Vite + TypeScript + Tailwind + Supabase, com deploy na Vercel.

## Tarefa

$ARGUMENTS

## Antes de planejar

- Leia o `CLAUDE.md` do projeto (regras, convenções, workflow de Issue/PR).
- Confirme a stack real (Vite SPA? há roteamento? Supabase compartilhado com outro projeto?).
- Não invente arquivos: use a estrutura que existe (`src/components/`, `src/hooks/`, `src/lib/`).

## Framework de análise

### 1. Quebra da tarefa
- Requisitos e critério de "pronto"
- Dependências (schema Supabase, RLS, libs — lembrar: não instalar lib sem perguntar)
- Arquivos afetados (caminho real em `src/`)
- Complexidade: Pequena / Média / Grande / Muito grande

### 2. Riscos e bloqueios
- Mudança de schema / migration / policies RLS
- Dados existentes (backward compatibility)
- Libs novas (precisa aprovação)
- Áreas do código pouco conhecidas

### 3. Passos de implementação (sequenciais)
1. Preparação (tipos, schema, migration)
2. Camada de dados (hooks, queries Supabase)
3. UI (componentes, formulários, estados de loading/erro/vazio)
4. Integração e polimento (motion, acessibilidade)
5. Verificação (`npm run lint`, `npm run build`, teste no browser)

### 4. Critério de "pronto"
Feature funciona como especificado · `npm run build` sem erros · `npm run lint` limpo · sem erros no console · responsivo · estados de loading/erro/vazio · testado no browser.

## Formato de saída

**Análise**
- Tipo: [Bug / Feature / Refactor / Infra]
- Complexidade: [...]
- Estimativa: X horas/dias (dobre a estimativa inicial para dev solo)

**Plano por fase**
```
Fase 1: <nome> (estimativa)
- [ ] passo
Fase 2: <nome> (estimativa)
- [ ] passo
```

**Arquivos a criar/modificar** (caminhos reais em `src/`)

**Migrations / mudanças de schema** (se houver)

**Verificação**
- comandos a rodar
- o que testar manualmente

**Primeiro passo concreto**

Entregue um plano que um dev solo consegue seguir passo a passo. Se a tarefa exige Issue + branch + PR (ver `CLAUDE.md`), inclua isso como passo zero.
