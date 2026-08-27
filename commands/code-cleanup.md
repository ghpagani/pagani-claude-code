---
description: Refatora e limpa código preservando o comportamento
argument-hint: <arquivo ou trecho a limpar>
---

Limpe e refatore o código abaixo para melhorar legibilidade e manutenção, **sem mudar o comportamento externo**. Stack: React 19 + Vite + TypeScript + Tailwind + Supabase.

## Código

$ARGUMENTS

## Checklist

**Nomes**
- Descritivos e consistentes (camelCase / PascalCase para componentes)
- Booleanos com `is`/`has`/`can`
- Comentários em português, explicando o *porquê*, não o *o quê*

**Funções e componentes**
- Responsabilidade única; funções curtas
- Componentes <200 linhas; extrair lógica para `src/hooks/`
- Early return em vez de aninhar `if`
- Máx. 3–4 parâmetros → objeto de parâmetros

**DRY**
- Extrair repetição para `src/lib/` ou hook
- Componentes reutilizáveis
- Constantes centralizadas

**TypeScript**
- Remover `any`; tipar de verdade
- `interface` para props; literal unions em vez de `enum`
- Utility types (`Pick`, `Omit`, `Partial`)

**Patterns**
- Optional chaining `?.` e nullish `??`
- Destructuring
- `map`/`filter`/`reduce` em vez de loop manual quando fica mais claro
- Mapa de handlers em vez de cadeia de `if (type === ...)`

**Código morto**
- Imports não usados, código comentado, variáveis não usadas, `console.log`

**Erros**
- `catch` que só faz `console.log` → tratar de verdade ou deixar propagar com contexto

## Saída
1. **Problemas encontrados**
2. **Código limpo**
3. **O que mudou e por quê**
4. **Melhorias opcionais** (sem over-engineering)

Rode `npm run lint` e `npm run build` no final.
