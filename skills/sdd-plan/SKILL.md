---
name: sdd-plan
description: Inicia a entrevista de produto para a funcionalidade e gera o PRD (docs/prd/PRD-<feature>.md) e o escopo do MVP fatiado (docs/mvp/MVP-<feature>.md).
---

# /sdd-plan [nome-da-feature]

Comando inicial do fluxo SDD (Spec-Driven Development). Abre a conversa de alinhamento de produto e gera os artefatos base em `docs/`.

## Passos de Execução

1. **Entrevista de Produto Refinada (Respostas em PT-BR):**
   - Qual é a dor principal ou objetivo de negócio desta funcionalidade?
   - Quem é o público-alvo (motoristas, gestores, admin, etc.) e o contexto de uso?
   - Quais são os recursos essenciais (Must-Have) sem os quais o MVP não funciona?
   - Quais são as restrições técnicas, de segurança ou regras de negócio imutáveis?
   - Como essa funcionalidade será fatiada em entregas incrementais (`Fatia 01`, `Fatia 02`, etc.)?

2. **Geração dos Artefatos de Produto:**
   - Cria `docs/prd/PRD-<nome-da-feature>.md` usando o template em `skills/sdd/references/prd-template.md`.
   - Cria `docs/mvp/MVP-<nome-da-feature>.md` usando o template em `skills/sdd/references/mvp-template.md` com o fatiamento detalhado do escopo em fatias.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao finalizar a geração do PRD e MVP, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> Execute o comando para mapear e criar as especificações técnicas base de todas as fatias do MVP:
> `/sdd-spec`
