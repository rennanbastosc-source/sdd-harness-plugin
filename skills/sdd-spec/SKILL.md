---
name: sdd-spec
description: Lê o PRD/MVP e gera as especificações técnicas base de todas as fatias do MVP (docs/specs/spec-<fatia>.md) com mapeamento holístico de banco, APIs, UI e testes.
---

# /sdd-spec [fatia-ou-funcionalidade-opcional]

Mapeia a arquitetura técnica e gera as especificações técnicas base de **todas as fatias** previstas no MVP, fornecendo uma visão arquitetural holística antes de criar qualquer linha de código.

## Passos de Execução

1. **Análise de Contexto Arquitetural:**
   - Lê `docs/prd/` e `docs/mvp/` para identificar o fatiamento completo do escopo.
   - Inspeciona a estrutura do repositório (usando `codebase-memory` ou busca textual) para mapear símbolos, funções, modelos de banco (Prisma/ORM), APIs e componentes UI afetados por cada fatia.

2. **Geração das Specs Técnicas Base:**
   - Para cada fatia do MVP, gera a especificação correspondente em `docs/specs/spec-<fatia>.md` (ex: `spec-fatia-01.md`, `spec-fatia-02.md`) usando o template em `skills/sdd/references/spec-template.md`.
   - Preenche o escopo funcional, arquivos a alterar/criar, contratos de dados, interfaces visuais, critérios de aceite e plano de testes (unitários, integração e e2e se tocar UI).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao finalizar a geração das specs técnicas de todas as fatias, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> As especificações de todas as fatias estão mapeadas! Execute o comando para criar a branch da feature, abrir a PR e iniciar a implementação sequencial de ponta a ponta:
> `/sdd-implement`
