# Documentação de Engenharia de Agentes e Harness (P26-2A-557F-D130-1422-DA84)

> **Requisito da Rubrica (25 pontos):** Uso obrigatório de no mínimo **3 agentes diferentes** (sendo obrigatoriamente **1 agente dedicado a teste e validação**), documentando em qual *harness* operaram e relacionando as *skills* na pasta `skills/`.

> Projeto #15: Lista de Tarefas Colaborativa (Shared To-Do). Estudante: Leonardo Ceratti dos Santos, RA 2026107850, turma 2A.

## 1. Ambiente de Orquestração (Harness Utilizado)

- **Harness Principal:** <<PREENCHER: harness realmente usado, com versão. Ex.: VS Code + GitHub Copilot (harness Local) ou opencode>>
- **Modelo(s) Base:** <<PREENCHER: modelos que apareceram nas sessões>>
- **Estratégia de Coordenação:** Os agentes operaram de forma modular sobre a subpasta `P26-2A-557F-D130-1422-DA84/`, compartilhando o esquema do D1 (`migrations/`), os contratos JSON das Cloudflare Pages Functions e a verificação automatizada via `validar-local.mjs`. Cada agente carrega a sua skill antes de agir; o agente de teste não edita arquivos.

---

## 2. Agentes Criados e Responsabilidades (Mínimo de 3 Agentes)

### Agente 1: Arquiteto Serverless, Cloudflare D1 e Segurança Discord OAuth2
- **Papel:** Modelagem do esquema relacional no Cloudflare D1 (`migrations/0001_init.sql` e `0002_shared_todo.sql`), fluxo de autenticação Discord OAuth2 e validação das regras de negócio no servidor (`functions/`, `lib/util.js`).
- **Skill Utilizada:** [`skills/serverless-d1-discord/SKILL.md`](./skills/serverless-d1-discord/SKILL.md)
- **Entregas Realizadas:**
  - Tabelas `discord_users`, `lists`, `list_members` e `tasks` com índices.
  - Login Discord com `state` anti-CSRF e sessão em cookie assinado (HMAC), em `functions/api/auth/`.
  - Rotas de listas e tarefas que checam sessão, associação à lista e responsável no servidor.
- **Como foi usado:** <<PREENCHER: o que você pediu, o que o agente fez e o que você corrigiu>>

### Agente 2: Especialista em Interface Web Vanilla (HTML5, CSS3 e DOM)
- **Papel:** Interface responsiva e acessível em HTML5, CSS3 e JavaScript puro, consumindo as rotas serverless via `fetch`; DOM montado sem `innerHTML` com texto de usuário.
- **Skill Utilizada:** [`skills/vanilla-dom-ui/SKILL.md`](./skills/vanilla-dom-ui/SKILL.md)
- **Entregas Realizadas:**
  - `public/index.html`, `public/styles.css` e `public/app.js`: login, listas, código de acesso, tarefas, subtarefas, responsável com avatar do Discord e conclusão.
  - Perfil do Discord (nome e avatar) no cabeçalho e rodapé com a Chave Única `P26-2A-557F-D130-1422-DA84`.
- **Como foi usado:** <<PREENCHER: o que você pediu, o que o agente fez e o que você corrigiu>>

### Agente 3: Agente de Teste, Auditoria de Segurança e Validação (Obrigatório)
- **Papel:** Verificação independente: inspeção dos contratos de API, tentativas de contornar as validações do servidor, auditoria da rubrica de 100 pontos e execução dos testes.
- **Skill Utilizada:** [`skills/teste-validacao/SKILL.md`](./skills/teste-validacao/SKILL.md)
- **Entregas Realizadas:**
  - `tests/api.test.mjs`: casos de sessão forjada ou expirada, não-membro, responsável inválido, subtarefa inválida, SQL injection e CSRF.
  - `skills/teste-validacao/scripts/auditar.mjs`: confere rotas autenticadas, esquema e o site publicado (HTTPS, 401 sem login, `/api/status`).
  - Execução do `validar-local.mjs` e relatório em `docs/evidencias/`.
- **Como foi usado:** <<PREENCHER: o que o agente verificou, o que encontrou e o que foi corrigido depois>>

---

## 3. Evidências

Prints e logs das sessões dos agentes e o relatório do agente de teste ficam em `docs/evidencias/`.
<<PREENCHER: liste os arquivos que você colocou lá>>
