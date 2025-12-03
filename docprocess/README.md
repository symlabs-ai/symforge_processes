# DocProcess

Processo para criar e publicar um artigo a partir de materiais fornecidos pelo usuário, com handoff para WordPress e notificação.

## Visão Geral
- Entrada: links/trechos enviados pelo usuário + preferências de estilo/tom.
- Saída: artigo final (após revisão), publicado em WordPress e notificado por e-mail.
- Symbiotas: `process_manager` (orquestra e publica) e `article_writer` (gera o texto).

## Etapas
1) Coleta de materiais: receber links, PDFs, conversas, etc.  
2) Coleta de estilo: registrar tom, público e requisitos de voz.  
3) Escrita: gerar rascunho (~1000 palavras) com base nos materiais + estilo.  
4) Validação: ajustar conforme feedback (tom, remoções, revisões).  
5) Publicação: enviar artigo final ao WordPress.  
6) Notificação: confirmar publicação por e-mail com cópia do artigo.

## Arquivos
- `process.md`: descrição narrativa do fluxo.
- `process.yml`: definição estruturada (IDs, entradas/saídas, symbiotas).
- `symbiotes/`: prompts dos agentes usados no fluxo.

## Como usar
1) Preencha/forneça os materiais e o briefing de estilo.  
2) Siga as etapas em `process.md` (ou use `process.yml` para orquestração automatizada).  
3) Ao final, valide o artigo, publique e confirme a notificação ao usuário.
