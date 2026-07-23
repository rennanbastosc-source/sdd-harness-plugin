---
name: sdd-spec
description: Lê o PRD/MVP e gera a especificação técnica detalhada da fatia (docs/specs/spec-<fatia>.md) com mapeamento de banco, APIs, UI e testes.
---

# /sdd-spec [fatia-ou-funcionalidade]

Traduz uma fatia do MVP em uma especificação técnica detalhada pronta para ser implementada.

## Passos de Execução

1. **Leitura do Contexto:**
   - Lê `docs/prd/` e `docs/mvp/` para extrair os requisitos da fatia solicitada.
   - Analisa o repositório atual (usando `codebase-memory` ou busca textual) para mapear símbolos, funções, schemas de banco e componentes afetados.

2. **Geração da Spec Técnica:**
   - Cria `docs/specs/spec-<fatia>.md` usando o template em `skills/sdd/references/spec-template.md`.
   - Preenche escopo, arquivos afetados, contratos de dados, componentes UI e critérios de aceite com testes.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao finalizar a spec técnica, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> A especificação está pronta! Execute o comando para construir a funcionalidade de ponta a ponta:
> `/sdd-implement`
