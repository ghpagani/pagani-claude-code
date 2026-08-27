# Publicando e atualizando

Este repositório é ao mesmo tempo **um plugin** (`.claude-plugin/plugin.json`) e **um marketplace de um plugin só** (`.claude-plugin/marketplace.json`, `source: "./"`).

## Primeira publicação

```bash
cd ~/Documents/Claude/pagani-claude-code
git init
git add .
git commit -m "chore: setup inicial do plugin"
gh repo create ghpagani/pagani-claude-code --public --source=. --remote=origin --push
```

## Instalar / testar

```
/plugin marketplace add ghpagani/pagani-claude-code
/plugin install pagani-claude-code@pagani-claude-code
```

Reinicie o Claude Code. Verifique:
- `/new-task`, `/component-new`, `/rls-policy` aparecem na lista de comandos
- `@agent-tech-stack-researcher` responde
- MCP servers carregaram (`/mcp`)

Para testar de novo do zero: `/plugin uninstall pagani-claude-code`.

## Atualizar

```bash
cd ~/Documents/Claude/pagani-claude-code
# edite commands/ ou agents/
# bumpe a versão nos DOIS arquivos: .claude-plugin/plugin.json e .claude-plugin/marketplace.json
git add . && git commit -m "feat: <mudança>"
git push
```

Usuários (você): `/plugin update pagani-claude-code`.

### Versionamento
- `0.1.x` — ajustes de texto, correções
- `0.x.0` — comando ou agente novo
- `x.0.0` — reestruturação / breaking change

## Estrutura esperada

```
pagani-claude-code/
├── .claude-plugin/
│   ├── plugin.json          # manifesto do plugin
│   └── marketplace.json     # marketplace (source: "./")
├── .mcp.json                # MCP servers
├── commands/                # *.md — auto-descobertos, viram /<nome>
├── agents/                  # *.md — auto-descobertos
├── docs/
└── README.md
```

## Erros comuns
- **Plugin não instala** → repo público? `.claude-plugin/plugin.json` existe? JSON válido (sem vírgula sobrando)?
- **Comando não aparece** → arquivo em `commands/` com extensão `.md` e frontmatter `description`?
- **Agente não ativa** → frontmatter com `name` e `description`; ativa por contexto, não por comando
- **`/plugin install` não resolve** → o nome depois do `@` é o nome do **marketplace**; aqui os dois se chamam `pagani-claude-code`
