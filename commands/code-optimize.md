---
description: Analisa e otimiza código para performance, memória e eficiência
argument-hint: <arquivo ou trecho a otimizar>
---

Otimize o código abaixo. Contexto: SPA React 19 + Vite + Tailwind, dados via Supabase, deploy na Vercel.

## Código

$ARGUMENTS

## Regras

- **Meça antes.** Aponte o gargalo real (re-render, query, bundle, loop). Não faça micro-otimização especulativa.
- **Não sacrifique legibilidade** por ganho marginal.
- Preserve o comportamento observável.

## Onde olhar

**React**
- Re-renders desnecessários (`memo`, `useMemo`, `useCallback` só quando o profiler justifica)
- Valores estáticos declarados dentro do componente → mover para fora
- Funções inline em listas grandes; `key` estável
- `lazy()` + `Suspense` para telas/rotas pesadas
- Listas longas → virtualização

**Dados (Supabase)**
- N+1 → uma query com join / `in()`
- `select('*')` → selecionar só as colunas usadas
- Paginação (`range`)
- Cache/dedup no hook; `prefetch` quando o próximo passo é previsível
- Índice no banco para colunas de filtro/ordenação frequentes

**Bundle (Vite)**
- `import` dinâmico para libs grandes usadas em poucas telas
- Trocar dependência pesada por alternativa leve (⚠️ pedir aprovação p/ instalar)
- `npx vite build --mode production` e inspecionar o output / usar `rollup-plugin-visualizer`

**Memória**
- Cleanup em `useEffect` (listeners, intervals, subscriptions do Supabase Realtime)
- Não recriar objetos/arrays a cada render sem necessidade

## Saída
1. **Gargalo** — qual é e como você sabe
2. **Código otimizado**
3. **O que mudou e por quê**
4. **Ganho esperado** (ordem de grandeza)
5. **Trade-offs**

Rode `npm run lint` e `npm run build` no final.
