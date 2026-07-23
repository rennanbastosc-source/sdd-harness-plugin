---
name: sdd-validate
description: Executa a bateria de qualidade automatizada e portão fechado detectando a stack do repositório (tsc, lint, vitest/pytest, e2e/playwright).
---

# /sdd-validate

Executa a validação rigorosa de qualidade no repositório com lógica de portão fechado.

## Passos de Execução

1. **Triage de Complexidade & Risco:**
   - Analisa o `git diff` e os módulos alterados para determinar o nível de risco:
     - **🟢 Baixa Complexidade:** Alterações visuais simples, correções de texto, refatorações isoladas. Roda `tsc`, `lint` e testes unitários existentes. Permite 1 volta de self-healing.
     - **🔴 Alta Complexidade / Risco Crítico:** Mudanças em auth, regras de negócio/cálculos, schemas de banco ou fluxos de UI multi-etapas. Aciona a bateria profunda com Self-Healing de até 3 voltas, testes E2E e Auditoria Ponytail.

2. **Loop de Auto-Cura (Self-Healing Loop):**
   - Executa a bateria (`tsc`, `lint`, `test`, `e2e`).
   - Se ocorrer qualquer falha: **extrai o log bruto**, diagnostica a causa raiz, aplica a correção no código e **re-executa a bateria automaticamente** (até 3 voltas). **NUNCA MASCARE ERROS**.

3. **Auditoria Ponytail Anti-Overengineering:**
   - Inspeciona o `git diff` procurando oportunidades de simplificação (`skills/sdd/references/ponytail-guide.md`):
     - `yagni:` Remove abstrações ou configs preparadas sem necessidade.
     - `delete:` Remove código morto ou retalhos desnecessários.
     - `shrink:` Simplifica estruturas complexas para formas enxutas e nativas.
   - Aplica os cortes/simplificações sem quebrar a suíte de testes.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Após a bateria completa ser concluída com 100% de sucesso (tudo verde), o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> Toda a bateria de validação (`tsc`, `lint`, `tests`, `e2e`) passou com 100% de sucesso! Execute o comando para gerar a spec final pós-implementação, atualizar documentos e realizar o commit/push/merge:
> `/sdd-finish`
