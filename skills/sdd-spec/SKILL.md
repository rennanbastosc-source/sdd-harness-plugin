---
name: sdd-spec
description: Lê o PRD/MVP e gera as especificações técnicas base de todas as fatias do MVP (docs/specs/spec-<fatia>.md) com mapeamento holístico de banco, APIs, UI e testes.
---

# /sdd-spec [fatia-ou-funcionalidade-opcional]

Mapeia a arquitetura técnica e gera as especificações técnicas base de **todas as fatias** previstas no MVP, fornecendo uma visão arquitetural holística antes de criar qualquer linha de código.

## Passos de Execução

1. **Análise de Contexto Arquitetural:**
   - Lê `docs/prd/` e `docs/mvp/` para identificar o fatiamento completo do escopo e **conta o número `N` de fatias enumeradas no MVP** (`Fatia 01`, `Fatia 02`, …).
   - Inspeciona a estrutura do repositório (usando `codebase-memory` ou busca textual) para mapear símbolos, funções, modelos de banco (Prisma/ORM), APIs e componentes UI afetados por cada fatia.

2. **Geração das Specs Técnicas Base:**
   - Gera **exatamente uma spec por fatia** (`N` fatias → `N` arquivos `docs/specs/spec-<fatia>.md`, ex: `spec-fatia-01.md`, `spec-fatia-02.md`) usando o template em `skills/sdd/references/spec-template.md`.
   - Preenche o escopo funcional, arquivos a alterar/criar, contratos de dados, interfaces visuais, critérios de aceite e plano de testes (unitários, integração e e2e se tocar UI).
   - Cada spec nasce com `Status: PENDENTE` (cabeçalho e Checkpoint de Execução) — é `/sdd-implement` que fará a transição `PENDENTE → EM ANDAMENTO → CONCLUÍDO`.

3. **Verificação de Cobertura (portão fechado):**
   - Confirma que o número de arquivos `spec-*.md` gerados é **igual a `N`**. Exibe um mapa `Fatia → spec` e sinaliza explicitamente qualquer fatia do MVP que tenha ficado **sem spec**. Não conclua o comando com cobertura incompleta.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao finalizar a geração das specs técnicas de todas as fatias, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> As especificações de todas as fatias estão mapeadas! Execute o comando para criar a branch da feature, abrir a PR e iniciar a implementação sequencial de ponta a ponta:
> `/sdd-implement`
