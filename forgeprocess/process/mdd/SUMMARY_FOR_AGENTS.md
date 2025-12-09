# MDD — SUMMARY_FOR_AGENTS

Este resumo serve como **guia rápido para LLMs e symbiotas** atuando na fase de
**Market Driven Development (MDD)**.

## 1. Visão Rápida

- Fase que transforma **hipótese de mercado** em **decisão de MVP**.
- Resultado final: decisão explícita em `docs/aprovacao_mvp.md` / `docs/revisao_estrategica.md` / `docs/rejeicao_projeto.md`.
- Todos os artefatos são Markdown versionados em Git.
- Entrada típica do ciclo: `docs/hipotese.md`.
- Saída para próxima fase (BDD): `docs/aprovacao_mvp.md` + visão/artefatos consolidados.

## 2. Etapas Principais (IDs)

Ver detalhes em `process/mdd/MDD_process.md` e `process/docs/PROCESS_IDS.md`.

- `mdd.01.concepcao_visao` — Concepção da Visão  
  - De `docs/hipotese.md` → `docs/visao.md`.
- `mdd.02.sintese_executiva` — Síntese Executiva  
  - De `docs/visao.md` → `docs/sumario_executivo.md`.
- `mdd.03.pitch_valor` — Pitch de Valor  
  - De visão+sumário → `docs/pitch_deck.md`.
- `mdd.04.validacao_publica` — Validação Pública Inicial  
  - De visão+sumário+pitch → `docs/sites/site_A/B/C.md` + resultados.
- `mdd.05.avaliacao_estrategica` — Avaliação Estratégica  
  - De resultados → decisão (`aprovacao_mvp` / `revisao_estrategica` / `rejeicao_projeto`).
- `mdd.06.handoff_bdd` — Handoff para BDD  
  - De decisão aprovada → início do BDD Process.

## 3. Artefatos Principais

- `docs/hipotese.md` — hipótese de mercado.
- `docs/visao.md` — visão de produto.
- `docs/sumario_executivo.md` — síntese executiva.
- `docs/pitch_deck.md` — narrativa de pitch.
- `docs/sites/site_A.md`, `site_B.md`, `site_C.md` — landing pages de validação.
- `docs/resultados_validacao.md` — análise de resultados.
- `docs/revisao_estrategica.md`, `docs/aprovacao_mvp.md`, `docs/rejeicao_projeto.md` — decisão.

## 4. Symbiotas Relevantes

- `mdd_coach`  
  - Conduz diálogos, estrutura visão, ajuda a preencher artefatos de MDD.
- `mdd_publisher`  
  - Converte artefatos MDD em PDFs, PPTX, HTML (saídas em `project/output/docs/`).
- `jorge_forge`  
  - Audita ao final da fase se o processo/artefatos seguiram o ForgeProcess.

