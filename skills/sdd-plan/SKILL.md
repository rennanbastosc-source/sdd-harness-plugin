---
name: sdd-plan
description: Inicia a entrevista de produto para a funcionalidade e gera o PRD (docs/prd/PRD-<feature>.md) e o escopo do MVP fatiado (docs/mvp/MVP-<feature>.md).
---

# /sdd-plan [nome-da-feature]

Comando inicial do fluxo SDD (Spec-Driven Development). Abre a conversa de alinhamento de produto e gera os artefatos base em `docs/`.

## Passos de Execução

1. **Entrevista de Produto (Respostas em PT-BR):**
   - Qual é a dor principal ou objetivo de negócio desta funcionalidade?
   - Quem é o público-alvo (motoristas, gestores, admin, etc.)?
   - Quais são os 3 recursos fundamentais sem os quais a funcionalidade não funciona (Must-Have)?
   - Quais são as restrições ou regras de negócio imutáveis?

2. **Geração dos Artefatos:**
   - Cria `docs/prd/PRD-<nome-da-feature>.md` usando o template em `skills/sdd/references/prd-template.md`.
   - Cria `docs/mvp/MVP-<nome-da-feature>.md` usando o template em `skills/sdd/references/mvp-template.md` com o fatiamento inicial (`Fatia 01`, `Fatia 02`, etc.).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao finalizar a geração do PRD e MVP, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> Execute o comando para criar a especificação técnica da primeira fatia:
> `/sdd-spec Fatia-01`
