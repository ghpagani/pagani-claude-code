---
description: Explica um trecho de código TypeScript/React de forma clara e progressiva
argument-hint: <arquivo, função ou trecho a explicar>
---

Explique o código abaixo para um dev que conhece JavaScript mas não este projeto. Foco em clareza e em conectar com o resto da base.

## Alvo

$ARGUMENTS

## Como explicar

### 1. Visão geral (2–4 frases)
- O que esse código faz e por que existe
- Onde ele se encaixa no fluxo do app (quem chama, o que ele chama)

### 2. Passo a passo
Percorra o código na ordem de execução. Para cada bloco relevante:
- O que acontece
- Por que está escrito assim (padrão React, hook, RLS do Supabase, etc.)
- Armadilhas: dependências de `useEffect`, re-renders, `await` em série vs paralelo, tipos frouxos

### 3. Conceitos que aparecem
Liste os conceitos não óbvios usados (ex.: custom hook, memoização, discriminated union, RLS, optimistic update) e explique cada um em 2–3 frases com um mini-exemplo no contexto **deste** código.

### 4. Diagrama (se ajudar)
Use um diagrama Mermaid (`flowchart` ou `sequenceDiagram`) só quando o fluxo for não-linear o suficiente para justificar.

### 5. Riscos e melhorias
- Bugs em potencial ou edge cases não tratados
- Simplificações possíveis sem mudar comportamento

## Formato de saída
Markdown: visão geral → passo a passo → conceitos → (diagrama) → riscos/melhorias. Sem encher linguiça; se o código for simples, a explicação é curta.
