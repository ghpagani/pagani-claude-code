# MCP servers

Definidos em `.mcp.json` na raiz do plugin. Sobem junto com o plugin; reinicie o Claude Code após instalar.

## context7 — `@upstash/context7-mcp`
Documentação atualizada e versionada de bibliotecas. Uso: mencione "use context7" no prompt, ou deixe os agentes chamarem. Sem config.

## playwright — `@playwright/mcp`
Automação de browser (navegar, screenshot, testar fluxos, ler console/rede). Sem config. Primeira execução baixa o browser.

## supabase — `@supabase/mcp-server-supabase`
Acesso ao schema/logs/advisors do Supabase, em **modo read-only** (`--read-only`).

Precisa de duas variáveis de ambiente na sua máquina (não no repo):

```bash
# ~/.bashrc, ~/.zshrc, ou variáveis de ambiente do Windows
export SUPABASE_ACCESS_TOKEN="sbp_..."      # Account → Access Tokens no painel Supabase
export SUPABASE_PROJECT_REF="xxxxxxxxxxxx"  # ref do projeto (Project Settings → General)
```

Como o projeto Supabase costuma ser **compartilhado** entre apps, aponte `SUPABASE_PROJECT_REF` para o projeto que hospeda o app atual e trate as tabelas por prefixo.

Se preferir o MCP do Supabase hospedado (conectado pela sua conta Claude) em vez deste local, remova o bloco `supabase` do `.mcp.json` para não ter dois.

## Adicionando outros MCP servers

Local, sem versionar: `.claude/settings.local.json` do projeto, ou um `.mcp.json` próprio no repo do projeto. Servidores oficiais úteis nesta stack: **Vercel** (`vercel`), **shadcn**. Não coloque tokens no `.mcp.json` versionado — use `${VAR}`.
