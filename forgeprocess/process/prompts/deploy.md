# Processo de Deploy — Pacotes forgeprocess e docprocess

Este documento define o processo padrão de **deploy** dos processos
`forgeprocess` e `docprocess` em forma de arquivos `.zip` prontos para
distribuição.

Os artefatos gerados serão:

- `deploy/forgeprocess.zip` — pacote com o diretório `forgeprocess/`
- `deploy/docprocess.zip` — pacote com o diretório `docprocess/`

> Regra geral: **nenhum build externo**. Apenas empacotamento dos diretórios
> em `.zip`, para serem consumidos por outras ferramentas (ex.: `symforge init`).

---

## 1. Pré‑requisitos

- Estar na raiz do repositório `symforge.processes`.
- Ter o utilitário `zip` instalado (ambiente Unix‑like ou WSL).
- Garantir que:
  - `forgeprocess/` esteja consistente (incluindo `process/VERSION.md`).
  - `docprocess/` esteja consistente.

---

## 2. Comandos de empacotamento

Na raiz do repositório (`symforge.processes`), executar:

```bash
mkdir -p deploy

# Pacote forgeprocess
zip -r deploy/forgeprocess.zip forgeprocess

# Pacote docprocess
zip -r deploy/docprocess.zip docprocess
```

Notas:
- O comando `zip -r` inclui todo o conteúdo das pastas `forgeprocess/` e `docprocess/`.
- Rodar estes comandos sempre **após** atualizar os arquivos de processo
  (incluindo `forgeprocess/process/VERSION.md`).

---

## 3. Convenções de versão

- A versão canônica do ForgeProcess está em:
  - `forgeprocess/process/VERSION.md`
- Cada vez que uma mudança compatível com patch é feita:
  1. Atualizar `VERSION.md` (ex.: `0.2.3` → `0.2.4`).
  2. Regenerar `deploy/forgeprocess.zip` e `deploy/docprocess.zip`.
  3. Comitar os `.zip` em conjunto com a mudança, se for política do repositório.

---

## 4. Uso por symbiotas / LLMs

- Para publicar uma nova versão dos processos:
  1. Aplicar mudanças em `forgeprocess/` e/ou `docprocess/`.
  2. Atualizar `forgeprocess/process/VERSION.md` conforme necessário.
  3. Executar os comandos da seção 2.
  4. (Opcional) Rodar qualquer verificação configurada no projeto.
  5. Abrir PR/commit contendo os novos `deploy/*.zip`.

- Symbiotas de build/deploy podem seguir literalmente os comandos aqui descritos,
  sem introduzir ferramentas adicionais (CI/CD, Docker, etc.) no fluxo mínimo.

