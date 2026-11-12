# Claude Skills

Coleção de skills do Claude para compartilhar.

## Como instalar

- **Claude Code (CLI/desktop):** copie a pasta da skill (a que tem o `SKILL.md`) para `~/.claude/skills/`.
  Ex.: `cp -r anthropic-skills/pdf ~/.claude/skills/`
- **Plugins inteiros** (`plugins/<nome>`): cada pasta é um plugin do Claude Code com `.claude-plugin/plugin.json`. Dá para instalar com `/plugin` apontando para a pasta, ou copiar só as skills de `plugins/<nome>/skills/*` para `~/.claude/skills/`.
- **Claude.ai / app:** compacte a pasta da skill em .zip e envie em Configurações > Capacidades > Skills.

## Conteúdo

| Pasta | O que tem | Licença |
|---|---|---|
| `minhas-skills/` | Skills próprias (lancar-despesa-totvs-jt) | — |
| `anthropic-skills/` | Skills da Anthropic com licença Apache 2.0 | Apache 2.0 |
| `plugins/` | Plugins de terceiros (Bright Data, Kong, Wix, Zoom, Postiz etc.) e plugins Anthropic (finance, marketing, productivity...) | Ver o LICENSE de cada pasta (MIT / Apache 2.0 / AGPL-3.0) |

## Não incluídos (licença não permite redistribuir ou não informada)

Instale direto no Claude (Configurações > Plugins/Skills ou `/plugin` no Claude Code):

- **Skills Anthropic:** built-in-browser, chrome-browser, computer-use, consolidate-memory, deep-research, doc-coauthoring, docs, explain-usage, google-workspace, import-memory, morning, setup-claude, setup-cowork
- **Plugins:** engineering, design, figma, miro, desktop-commander, tareno
