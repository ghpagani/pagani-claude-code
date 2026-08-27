# MCP servers

Definidos em `.mcp.json` na raiz do plugin. Sobem junto com o plugin; reinicie o Claude Code após instalar.

Por padrão o plugin traz só `context7` e `playwright`. Para Supabase, o recomendado é usar a **conexão Supabase da conta Claude** (já integrada, sem token pra gerenciar). O bloco `supabase` abaixo é opcional — adicione ao `.mcp.json` só se quiser um servidor local dedicado.

## context7 — `@upstash/context7-mcp`
Documentação atualizada e versionada de bibliotecas. Uso: mencione "use context7" no prompt, ou deixe os agentes chamarem. Sem config.

## playwright — `@playwright/mcp`
Automação de browser (navegar, screenshot, testar fluxos, ler console/rede). Sem config. Primeira execução baixa o browser.

## supabase (opcional) — `@supabase/mcp-server-supabase`
Acesso ao schema/logs/advisors do Supabase, em **modo read-only**. Só use se NÃO estiver usando a conexão Supabase da conta Claude.

Bloco para colar em `.mcp.json` → `mcpServers`:

```json
"supabase": {
  "command": "npx",
  "args": ["-y", "@supabase/mcp-server-supabase", "--read-only", "--project-ref=${SUPABASE_PROJECT_REF}"],
  "env": { "SUPABASE_ACCESS_TOKEN": "${SUPABASE_ACCESS_TOKEN}" }
}
```

Precisa de duas variáveis de ambiente na sua máquina (não no repo):

```powershell
# Windows PowerShell (permanente, para o usuário)
[Environment]::SetEnvironmentVariable("SUPABASE_ACCESS_TOKEN", "sbp_...", "User")   # Account → Access Tokens no painel Supabase
[Environment]::SetEnvironmentVariable("SUPABASE_PROJECT_REF", "xxxxxxxxxxxx", "User") # ref do projeto (Project Settings → General)
```

`SUPABASE_PROJECT_REF` aponta para um projeto de cada vez — troque ao mudar de app. Reinicie o Claude Code para as variáveis entrarem.

## Adicionando outros MCP servers

Local, sem versionar: `.claude/settings.local.json` do projeto, ou um `.mcp.json` próprio no repo do projeto. Servidores oficiais úteis nesta stack: **Vercel** (`vercel`), **shadcn**. Não coloque tokens no `.mcp.json` versionado — use `${VAR}`.
