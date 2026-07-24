---
name: sdd-audit
description: "Executa auditoria holística no repositório analisando código enxuto (Ponytail scan: yagni, delete, stdlib, shrink), governança SDD (STATE.md vs specs vs código) e lacunas de testes."
---

# /sdd-audit [caminho-ou-modulo-opcional]

Executa uma auditoria completa de saúde técnica, arquitetura e governança no repositório inteiro ou em um módulo específico.

---

## 🎯 As 3 Dimensões da Auditoria

1. **Dimensão 1: Lean Code Audit (Estilo Ponytail)**
   - Identifica sobre-engenharia, código morto, abstrações prematuras e reinvenção de stdlib ou APIs nativas.
   - Tags de auditoria — **fonte única da verdade em `skills/sdd/references/ponytail-guide.md`** (`delete`, `stdlib`, `yagni`, `shrink`):
     - `delete:` Código morto, retalhos sem uso ou flexibilidade especulativa.
     - `stdlib:` Código manual substituível por função nativa da linguagem/plataforma.
     - `yagni:` Abstração com apenas 1 implementação ou config não utilizada.
     - `shrink:` Oportunidade de simplificação e redução de linhas.

2. **Dimensão 2: Governança SDD & Consistência de Estado**
   - Inspeciona o alinhamento entre o código vivo e a documentação do projeto:
     - **Specs Fantasma:** Specs marcadas como `EM ANDAMENTO` ou `PENDENTE` abandonadas em `docs/specs/`.
     - **Sincronia com `STATE.md`:** Verifica se alterações em modelos de banco, Server Actions ou rotas críticas foram registradas no `STATE.md`.
     - **Invariantes do Projeto:** Garante que regras permanentes e restrições imutáveis continuam sendo respeitadas.

3. **Dimensão 3: Cobertura & Densidade de Testes**
   - Identifica componentes visuais, rotas de API e Server Actions críticas que não possuem testes unitários, de integração ou E2E (Playwright).

---

## 📋 Formato de Saída do Relatório

O relatório de auditoria deve ser exibido de forma concisa e ranqueado pelo **maior impacto / economia de código**:

```text
📊 SDD AUDIT REPORT: <Nome-do-Projeto>

--- ✂️ LEAN & ANTI-OVERENGINEERING ---
1. L45-78 [caminho/arquivo.ts] yagni: AbstractRepository com 1 implementação. Inlinear. (net: -33 linhas)
2. L12 [package.json] native: Lib externa usada para 1 format. Usar Intl.DateTimeFormat (net: -1 dep)

--- 📜 GOVERNANÇA SDD & ESTADO ---
3. [STATE.md] out-of-sync: Novo modelo de banco não registrado nos invariantes.
4. [docs/specs/spec-fatia-02.md] ghost-spec: Spec pendente sem implementação ativa.

--- 🛡️ GAPS DE QUALIDADE & TESTES ---
5. [src/actions/domain.ts] missing-test: Action crítica sem cobertura de testes.

---------------------------------------------------------
📉 Oportunidade Total: -N linhas, -M dependências, X atualizações de docs.
```

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao concluir a geração do relatório de auditoria, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> 
> - **Para aplicar as correções e refatorações identificadas:** execute `/sdd-implement` ou crie uma spec dedicada com `/sdd-spec`.
> - **Para planejar uma nova funcionalidade:** execute `/sdd-plan <nome-da-feature>`.
