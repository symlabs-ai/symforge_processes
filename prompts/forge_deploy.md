# Forge Deploy

Este prompt guia o processo de deploy do ForgeProcess.

## Fonte da Verdade

O arquivo `process/VERSION.md` é a **fonte única da verdade** para a versão do ForgeProcess.

Formato do arquivo:
```markdown
# ForgeProcess Version

X.Y.Z
```

## Procedimento de Deploy

### 1. Bump de Versão

Leia `process/VERSION.md` e incremente a versão seguindo SemVer:
- **MAJOR** (X): Mudanças incompatíveis com versões anteriores
- **MINOR** (Y): Novas funcionalidades compatíveis
- **PATCH** (Z): Correções de bugs compatíveis

Atualize os seguintes arquivos com a nova versão:
1. `process/VERSION.md` (fonte da verdade)
2. `process/PROCESS.yml` (campo `version:`)

### 2. Commit e Tag

```bash
# Navegar para a raiz do repositório (pasta pai de forgeprocess/)
cd /caminho/para/symforge.processes

# Adicionar alterações
git add forgeprocess/process/VERSION.md forgeprocess/process/PROCESS.yml

# Commit com mensagem padronizada
git commit -m "chore(process): bump ForgeProcess version to X.Y.Z"

# Criar tag no formato vX.Y.Z
git tag -a vX.Y.Z -m "ForgeProcess vX.Y.Z"

# Push do commit e da tag
git push && git push --tags
```

### 3. Gerar Artefato de Deploy

```bash
# Apagar zip antigo
rm deploy/forgeprocess.zip

# Gerar novo zip (a partir de dentro da pasta, sem incluir "forgeprocess/" no path)
cd forgeprocess
zip -r ../deploy/forgeprocess.zip . \
  -x "*.pyc" \
  -x "__pycache__/*" \
  -x "*.egg-info/*" \
  -x ".pytest_cache/*" \
  -x "*.log"
cd ..

# Commit do novo artefato
git add deploy/forgeprocess.zip
git commit -m "chore(deploy): update forgeprocess.zip to vX.Y.Z"
git push
```

## Checklist de Deploy

- [ ] Versão incrementada em `process/VERSION.md`
- [ ] Versão sincronizada em `process/PROCESS.yml`
- [ ] Commit realizado com mensagem padronizada
- [ ] Tag `vX.Y.Z` criada e pushed
- [ ] `deploy/forgeprocess.zip` recriado
- [ ] Artefato commitado e pushed

## Exemplo Completo

```bash
# Supondo versão atual 0.2.5, incrementando para 0.2.6

# 1. Atualizar VERSION.md para 0.2.6
# 2. Atualizar PROCESS.yml version: "0.2.6"

# 3. Commit e tag
cd /mnt/c/Users/palha/dev/symforge.processes
git add forgeprocess/process/VERSION.md forgeprocess/process/PROCESS.yml
git commit -m "chore(process): bump ForgeProcess version to 0.2.6"
git tag -a v0.2.6 -m "ForgeProcess v0.2.6"
git push && git push --tags

# 4. Regenerar zip (sem incluir "forgeprocess/" no path)
rm deploy/forgeprocess.zip
cd forgeprocess
zip -r ../deploy/forgeprocess.zip . \
  -x "*.pyc" -x "__pycache__/*" -x "*.egg-info/*" -x ".pytest_cache/*" -x "*.log"
cd ..

# 5. Commit do artefato
git add deploy/forgeprocess.zip
git commit -m "chore(deploy): update forgeprocess.zip to v0.2.6"
git push
```

## Notas

- Sempre execute a partir da raiz do repositório (`symforge.processes/`)
- O `.gitignore` não deve conter `forgeprocess/`
- Tags devem seguir o padrão `vX.Y.Z` (com prefixo `v`)
- O zip exclui arquivos de cache e logs automaticamente
