# 🚀 SDD Harness Plugin (`sdd-harness-plugin`)

> **Harness genérico, agnóstico e portátil de Spec-Driven Development (SDD) para Agentes AI.**

O **SDD Harness Plugin** traz uma metodologia robusta de engenharia de produto para transformar ideias em software funcionando de forma iterativa, previsível e sem sobre-engenharia em **qualquer linguagem, framework ou repositório**.

**Agnóstico de agente por construção:** todo o harness é Markdown puro com frontmatter YAML — sem runtime, sem dependência, sem binário. Roda em Claude Code, OpenCode, Codex CLI, Cursor, Copilot, Windsurf, Gemini CLI, Antigravity e qualquer agente que leia arquivos de skill/command. Veja [Compatibilidade](#-compatibilidade-de-agentes).

---

## 🎯 Por que usar Spec-Driven Development?

1. **Visão de Produto Alinhada (`PRD`):** Nenhuma linha de código é escrita sem entender a dor do usuário e o valor de negócio.
2. **Escopo Mínimo Viável (`MVP`):** Recorte rigoroso entre **Must-Have** (MVP) e **Nice-To-Have** (futuro), fatiando a entrega em etapas gerenciáveis.
3. **Especificação Técnica Estrita (`Spec`):** Arquitetura, dados, APIs, UI e testes mapeados de todas as fatias antes da implementação.
4. **Código Enxuto (`Ponytail Lean Engineering`):** Regras ativas contra sobre-engenharia (*Lazy Senior Dev Mode*). Reuso máximo de código, stdlib e APIs nativas.
5. **Loop Engineering Adaptativo (dois escopos):** Triage por complexidade, auto-cura (*Self-Healing*) de até 3 voltas e auditoria anti-overengineering no diff. A rotina é uma só e roda **duas vezes**: por fatia, como portão de commit em `/sdd-implement`, e por feature, como portão de merge em `/sdd-validate`. Fatia vermelha não é commitada; PR vermelha não é integrada.
6. **Entregas Ponta a Ponta:** Toda fatia é construída completa (Backend + Frontend + Testes no mesmo ciclo).

---

## 🔄 Fluxo de Slash Commands

O plugin disponibiliza 7 slash commands compostos que guiam o desenvolvimento, a qualidade e a auditoria de código. **Toda etapa finaliza sugerindo automaticamente o próximo comando!**

| Slash Command | Etapa | Descrição | Próximo Passo Sugerido |
|---|---|---|---|
| **`/sdd`** | 0. Retomada | Guardião de sessão multi-worktree: reconstrói o checkpoint de cada fluxo SDD ativo a partir de `docs/` e do Git (ideal após um `/clear`) | `👉 <comando + pasta detectados>` |
| **`/sdd-plan <feature>`** | 1. Produto | Entrevista de alinhamento lapidada e geração de `PRD` + `MVP` (N fatias) em `docs/` | `👉 /sdd-spec` |
| **`/sdd-spec`** | 2. Arquitetura | Mapeamento arquitetural holístico e geração das specs base de **todas as fatias** em `docs/specs/` | `👉 /sdd-implement` |
| **`/sdd-implement`** | 3. Código & Governança | Criação da branch (`feat/...`), commit dos docs, PR Draft e desenvolvimento e2e fatia a fatia (Backend + UI + Testes), com **loop de validação como portão de commit** | `👉 /sdd-validate` |
| **`/sdd-validate`** | 4. Qualidade | O mesmo loop no escopo da **feature inteira**: suíte completa, E2E obrigatório e Ponytail Review — pega regressão entre fatias | `👉 /sdd-finish` |
| **`/sdd-finish`** | 5. Conclusão | Geração da Spec Final pós-implementação (*as-built*), atualização de `STATE.md`, commit final, push e merge | `👉 /sdd-plan` |
| **`/sdd-audit`** | 6. Auditoria | Auditoria holística do repositório em 3 dimensões (Lean Code/Ponytail, Governança SDD/STATE.md e Cobertura de Testes) | `👉 /sdd-implement` |

---

## 🤖 Compatibilidade de Agentes

O harness são só dois diretórios de Markdown:

- `skills/` — as 7 skills (`SKILL.md` + `references/`), onde mora toda a lógica;
- `commands/` — 7 stubs de uma linha que apenas invocam a skill correspondente.

Qualquer agente que leia um desses dois formatos executa o fluxo completo. Nada mais é necessário.

| Agente | Global | No projeto | O que copiar |
|---|---|---|---|
| **Claude Code** | `~/.claude/skills/` | `.claude/skills/` | `skills/*` (+ `commands/*` em `.claude/commands/`) |
| **OpenCode** | `~/.config/opencode/skills/` | `.opencode/skills/` | `skills/*` |
| **Codex CLI** | `~/.codex/skills/` | `.codex/skills/` ou `.agents/skills/` | `skills/*` |
| **Cursor** | — | `.cursor/commands/` | `commands/*` |
| **GitHub Copilot** | — | `.github/prompts/` | `commands/*` renomeados para `*.prompt.md` |
| **Windsurf** | `~/.codeium/windsurf/workflows/` | `.windsurf/workflows/` | `commands/*` |
| **Gemini CLI** | `~/.gemini/commands/` | `.gemini/commands/` | `commands/*` convertidos para `.toml` (ver abaixo) |
| **Antigravity** | `~/.gemini/config/plugins/` | — | repositório inteiro |
| **Roo Code** | `~/.roo/commands/` | `.roo/commands/` | `commands/*` |
| **Outros** | — | `.agents/skills/` | `skills/*` |

> Agentes que suportam **Agent Skills** (`SKILL.md`) carregam a skill sob demanda e leem `references/` só quando precisa — mais barato em contexto. Agentes que só suportam slash commands usam `commands/`, que apontam para a skill; nesse caso copie **os dois** diretórios para o agente achar o conteúdo referenciado.

### Instalação

```bash
git clone https://github.com/rennanbastosc-source/sdd-harness-plugin.git /tmp/sdd-harness

# Claude Code (global)
cp -r /tmp/sdd-harness/skills/*   ~/.claude/skills/
cp -r /tmp/sdd-harness/commands/* ~/.claude/commands/

# OpenCode (global)
cp -r /tmp/sdd-harness/skills/*   ~/.config/opencode/skills/

# Codex CLI (global)
cp -r /tmp/sdd-harness/skills/*   ~/.codex/skills/

# No projeto (Cursor / Windsurf / Copilot — troque o destino conforme a tabela)
cp -r /tmp/sdd-harness/commands/* .cursor/commands/
```

Prefere versionar com a equipe? Use submódulo em vez de cópia:

```bash
git submodule add https://github.com/rennanbastosc-source/sdd-harness-plugin.git .agents/sdd-harness
```

### Gemini CLI (formato TOML)

O Gemini CLI usa TOML, não Markdown. Converta cada command uma vez:

```bash
mkdir -p ~/.gemini/commands
for f in /tmp/sdd-harness/commands/*.md; do
  n=$(basename "$f" .md)
  printf 'description = "SDD Harness: %s"\nprompt = """\n%s\n"""\n' \
    "$n" "$(cat "$f")" > ~/.gemini/commands/"$n".toml
done
```

---

## 📁 Estrutura de Artefatos Gerada no Projeto Local

Ao utilizar o plugin, a seguinte estrutura limpa é mantida em `docs/`:

```text
<raiz-do-projeto>/
└── docs/
    ├── prd/
    │   ├── PRD-auth.md
    │   └── PRD-billing.md
    ├── mvp/
    │   ├── MVP-auth.md
    │   └── MVP-billing.md
    └── specs/
        ├── spec-auth-fatia-01.md
        ├── spec-auth-fatia-02.md
        ├── spec-billing-fatia-01.md
        └── spec-billing-fatia-02.md
```

### 🔑 Fluxos paralelos sem colisão

Todo artefato carrega o **slug canônico** da feature no nome (minúsculas, sem acentos, kebab-case), e o mesmo slug nomeia a branch `feat/<slug>` e o bloco `### <slug>` no `STATE.md`. Cada subcomando `/sdd-*` resolve a feature ativa — pelo argumento, pela branch ou pelo MVP único da worktree — e opera **exclusivamente** sobre os arquivos dela.

Consequência prática: duas features em worktrees paralelas escrevem conjuntos de arquivos disjuntos, uma nunca sobrescreve as specs da outra, e as duas branches mergeiam em `docs/` sem conflito. A regra completa está em [`skills/sdd/references/workflow-guide.md`](skills/sdd/references/workflow-guide.md) (**Motor de Escopo por Feature**).

O `STATE.md` é global e recebe um bloco `### <slug>` **append-only** por feature; `/sdd-implement` garante `STATE.md merge=union` no `.gitattributes` para que o próprio Git concatene os registros de fluxos paralelos sem conflito.

Specs no formato antigo (`spec-fatia-NN.md`, sem slug) continuam sendo lidas quando a worktree tem uma única feature. Nada é renomeado automaticamente.

---

## 📄 Licença

Distribuído sob a licença [MIT](LICENSE). Livre para uso comercial e pessoal.
