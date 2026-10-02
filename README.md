# Automacoes pessoais

Sincronizacao automatica de `DoanCasotti/DeskcommCRM`, branch `main`, com `melgarafael/DeskcommCRM`.

- Executa a cada hora, no minuto 17 (UTC), e manualmente pela aba Actions.
- Repositorio publico e runner Linux padrao: execucoes gratuitas do GitHub Actions. Nao usa runners pagos nem publica artefatos.
- Atualiza somente por fast-forward, sem force push. Se a main do fork tiver commits proprios ou o original reescrever o historico, interrompe com erro. Faca contribuicoes em branches separadas.
- Usa uma deploy key exclusiva do fork, armazenada no secret `DESKCOMM_SYNC_SSH_KEY`. A chave privada nunca pertence aos arquivos publicos.
- Nao executa codigo do projeto original, nao altera outras branches e nao sincroniza tags ou pastas locais.
- Registra em `status/deskcomm.json` o commit sincronizado. Um commit de registro so e criado quando essa versao muda.

## Limites do agendamento

GitHub Actions pode atrasar execucoes. Em repositorios publicos, agendamentos podem ser desativados apos 60 dias sem atividade. Os registros de novas versoes geram atividade real; se o original ficar parado por muito tempo, verifique a aba Actions e reative o workflow se necessario.

## Executar e acompanhar

Abra [Actions](https://github.com/DoanCasotti/automacoes/actions/workflows/sync-deskcomm.yml), selecione **Run workflow** para executar manualmente e consulte os logs. Erros de divergencia exigem revisao do historico; a automacao nao descarta seus commits.

Para revogar o acesso, remova a deploy key `automacoes-sync-DeskcommCRM` nas configuracoes de `DoanCasotti/DeskcommCRM` e desative o workflow.

Documentacao: [cobranca](https://docs.github.com/en/billing/concepts/product-billing/github-actions), [agendamento](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule), [deploy keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys).
