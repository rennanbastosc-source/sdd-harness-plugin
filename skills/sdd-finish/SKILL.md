---
name: sdd-finish
description: Atualiza os arquivos de estado do projeto (STATE.md, BACKLOG.md, etc.) e finaliza a fatia entregue com commit no padrão Conventional Commits.
---

# /sdd-finish

Finaliza o ciclo da fatia entregue e registra as alterações no controle de versão e documentação.

## Passos de Execução

1. **Atualização da Spec:**
   - Marca o status da spec ativa como `CONCLUÍDO` em `docs/specs/spec-*.md`.

2. **Atualização do Estado do Repositório:**
   - Atualiza `STATE.md` (se existir) adicionando novos invariantes vivos ou alterações estruturais.
   - Atualiza `BACKLOG.md` / `STATE_ARCHIVE.md` (se existirem) removendo itens concluídos.

3. **Commit dos Artefatos:**
   - Prepara e executa a mensagem de commit utilizando **Conventional Commits** em PT-BR (ex: `feat(modulo): adiciona fluxo de...`).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao concluir o commit e o fechamento da fatia, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> 
> - **Se houver mais fatias pendentes no MVP:** execute `/sdd-spec Fatia-XX` (substituindo pelo nome da próxima fatia).
> - **Se o MVP foi 100% concluído e você vai iniciar um novo produto/feature:** execute `/sdd-plan <nome-da-nova-feature>`.
