# 🚀 SDD Harness Plugin (`sdd-harness-plugin`)

> **Harness genérico, agnóstico e portátil de Spec-Driven Development (SDD) para Agentes AI.**

O **SDD Harness Plugin** traz uma metodologia robusta de engenharia de produto para transformar ideias em software funcionando de forma iterativa, previsível e sem sobre-engenharia em **qualquer linguagem, framework ou repositório**.

---

## 🎯 Por que usar Spec-Driven Development?

1. **Visão de Produto Alinhada (`PRD`):** Nenhuma linha de código é escrita sem entender a dor do usuário e o valor de negócio.
2. **Escopo Mínimo Viável (`MVP`):** Recorte rigoroso entre **Must-Have** (MVP) e **Nice-To-Have** (futuro), fatiando a entrega em etapas gerenciáveis.
3. **Especificação Técnica Estrita (`Spec`):** Arquitetura, dados, APIs, UI e testes mapeados antes da implementação.
4. **Entregas Ponta a Ponta:** Toda fatia é construída completa (Backend + Frontend + Testes no mesmo ciclo).
5. **Automação de Qualidade (`Validate`):** Deteção automática da stack do projeto e execução de linters, typecheckers e suíte de testes.

---

## 🔄 Fluxo de Slash Commands

O plugin disponibiliza 5 slash commands compostos que guiam o desenvolvedor e o agente passo a passo. **Toda etapa finaliza sugerindo automaticamente o próximo comando!**

| Slash Command | Etapa | Descrição | Próximo Passo Sugerido |
|---|---|---|---|
| **`/sdd-plan <feature>`** | 1. Produto | Entrevista de alinhamento lapidada e geração de `PRD` + `MVP` (N fatias) em `docs/` | `👉 /sdd-spec` |
| **`/sdd-spec`** | 2. Arquitetura | Mapeamento arquitetural holístico e geração das specs base de **todas as fatias** em `docs/specs/` | `👉 /sdd-implement` |
| **`/sdd-implement`** | 3. Código & Governança | Criação da branch (`feat/...`), commit dos docs, PR Draft e desenvolvimento e2e sequencial (Backend + UI + Testes) | `👉 /sdd-validate` |
| **`/sdd-validate`** | 4. Qualidade | Execução automatizada da bateria (`tsc`, `lint`, `test`, `e2e` se houver UI) | `👉 /sdd-finish` |
| **`/sdd-finish`** | 5. Conclusão | Geração da Spec Final pós-implementação (*as-built*), atualização de `STATE.md`, commit final, push e merge | `👉 /sdd-plan` |

---

## 💻 Instalação

### Opção A: Instalação Global (Todos os Projetos no seu Computador)

Clone este repositório na sua pasta global de configurações de agente:

```bash
# Para Antigravity / Gemini CLI
git clone https://github.com/SEU-USUARIO/sdd-harness-plugin.git ~/.gemini/config/plugins/sdd-harness-plugin

# Ou instale as skills diretamente em ~/.claude/skills ou ~/.gemini/config/skills
```

### Opção B: Instalação no Repositório do Projeto / Equipe

Adicione este plugin como submódulo ou clone na pasta `.claude/skills` ou `.agents/skills` do repositório:

```bash
git clone https://github.com/SEU-USUARIO/sdd-harness-plugin.git .claude/skills/sdd-harness
```

---

## 📁 Estrutura de Artefatos Gerada no Projeto Local

Ao utilizar o plugin, a seguinte estrutura limpa é mantida em `docs/`:

```text
<raiz-do-projeto>/
└── docs/
    ├── prd/
    │   └── PRD-<feature>.md
    ├── mvp/
    │   └── MVP-<feature>.md
    └── specs/
        └── spec-<feature>-fatia-XX.md
```

---

## 📄 Licença

Distribuído sob a licença [MIT](LICENSE). Livre para uso comercial e pessoal.
