# Automacoes pessoais

Sincronizacao automatica de `DoanCasotti/DeskcommCRM`, branch `main`, com `melgarafael/DeskcommCRM`.

- Executa a cada 3 dias (dias 1, 4, 7... do mes, 09:41 UTC), e manualmente pela aba Actions.
- Repositorio publico e runner Linux padrao: execucoes gratuitas do GitHub Actions. Nao usa runners pagos nem publica artefatos.
- Atualiza somente por fast-forward, sem force push. Se a main do fork tiver commits proprios ou o original reescrever o historico, interrompe com erro. Faca contribuicoes em branches separadas.
- Usa uma deploy key exclusiva do fork, armazenada no secret `DESKCOMM_SYNC_SSH_KEY`. A chave privada nunca pertence aos arquivos publicos.
- Nao executa codigo do projeto original, nao altera outras branches e nao sincroniza tags ou pastas locais.
- Confere o SHA remoto depois de cada push e so marca a rodada como verde quando a `main` do fork corresponde ao original.
- Registra em `status/deskcomm.json` o commit sincronizado. Um commit de registro so e criado quando essa versao muda.

## Limites do agendamento

GitHub Actions pode atrasar ou descartar execucoes agendadas em periodos de carga. Se uma rodada for descartada, a seguinte (3 dias depois) cobre. Em repositorios publicos, agendamentos sao desativados apos 60 dias sem commit. Para isso nunca acontecer, o workflow faz um commit de manutencao em `status/deskcomm.json` quando o original fica mais de 30 dias sem mudar.

A garantia: toda rodada verde termina com a `main` do fork no mesmo SHA da `main` do original (conferido depois do push). Rodada vermelha manda e-mail do GitHub. A unica causa esperada de vermelho e commit direto na `main` do fork — nunca commite nela; use branches.

O GitHub Actions do proprio fork fica desligado (Settings > Actions): o fork e espelho, e cada sincronizacao rodaria o CI inteiro do original nele, com falhas e e-mails.

## Executar e acompanhar

Abra [Actions](https://github.com/DoanCasotti/automacoes/actions/workflows/sync-deskcomm.yml), selecione **Run workflow** para executar manualmente e consulte os logs. Erros de divergencia exigem revisao do historico; a automacao nao descarta seus commits.

Para revogar o acesso, remova a deploy key `automacoes-sync-DeskcommCRM` nas configuracoes de `DoanCasotti/DeskcommCRM` e desative o workflow.

Documentacao: [cobranca](https://docs.github.com/en/billing/concepts/product-billing/github-actions), [agendamento](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule), [deploy keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys).
