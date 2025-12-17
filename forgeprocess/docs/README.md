# Documentação do Projeto

Esta pasta contém a documentação principal do projeto, organizada de forma a servir tanto a **usuários finais do produto** quanto a **desenvolvedores e agentes/symbiotas** que irão trabalhar na base de código.

Em alto nível:

- `docs/product/` — documentação focada em **uso do produto final**.
- `docs/integrations/` — documentação focada em **integrações e guias técnicos** para quem implementa o produto.

---

## `docs/product/` — Guia para Usuários e Agentes de Uso

Esta pasta reúne documentos que explicam **como usar o produto final**, do ponto de vista de quem consome as capacidades expostas (CLI, API, fluxo de trabalho, etc.).

Destinos típicos:

- Tutoriais de uso da CLI ou API principal.
- Guias de fluxo (ex.: “como executar um ciclo padrão”, “como configurar o produto para um time”).
- Exemplos de cenários reais de uso, que ajudam agentes e humanos a entender **o que o produto faz** e **como ele deve se comportar**.

Para symbiotas/LLMs:

- Use `docs/product/` como **fonte de verdade funcional** sobre a experiência do usuário e os contratos de uso do produto.
- Ao gerar respostas ou handoffs voltados a usuários finais, referencie estes documentos como base.

---

## `docs/integrations/` — Guia para Desenvolvedores e Integrações de Terceiros

Esta pasta reúne guias de **integração técnica** com ferramentas e serviços externos relevantes ao projeto como um todo.

Subdiretórios típicos:

- `docs/integrations/forgebase_guides/`  
  - Regras e guias do ForgeBase (arquitetura, Clean/Hex, CLI-first, persistência, etc.).
- `docs/integrations/forge_llm_guides/`  
  - Guias de uso do Forge LLM Client/SDK, incluindo:
    - providers (OpenRouter, Ollama, Gemini, Llama.cpp),
    - integração com MCP,
    - hooks/middlewares, observabilidade, error handling,
    - tool calling, streaming, JSON mode, etc.

Para desenvolvedores e symbiotas de código (como o `forge_coder`):

- Use `docs/integrations/` como **guia técnico** para implementar o produto final:
  - entender como conectar com provedores externos,
  - como aplicar as regras do ForgeBase na arquitetura,
  - como instrumentar observabilidade, segurança e integrações MCP.
- Quando precisar decidir **como** integrar (e não apenas **o que** o produto deve fazer), comece por aqui.

---

## Como Navegar

- Se o objetivo é **usar o produto** ou explicar seu uso para stakeholders/usuários:
  - comece por `docs/product/`.
- Se o objetivo é **desenvolver, integrar ou manter** o produto:
  - comece por `docs/integrations/`, em especial:
    - `docs/integrations/forgebase_guides/`,
    - `docs/integrations/forge_llm_guides/`.

Sempre que criar novos artefatos de documentação:

- Coloque guias de **uso** em `docs/product/`.
- Coloque guias de **integração técnica** em `docs/integrations/`.

