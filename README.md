# Deploy Automatizado com Notificações

Este repositório contém um workflow do GitHub Actions que automatiza o processo de deploy e envia notificações sobre o seu andamento via Slack e e-mail. O workflow é projetado para ser executado tanto em pushes para a branch principal quanto em um cronograma predefinido.

## Funcionalidades

- **Deploy Automático**: O código é implantado automaticamente em um servidor VPS via SSH.
- **Notificações**: Envia atualizações sobre o status do deploy para o Slack e por e-mail.
- **Agendamento**: Executa o deploy em um horário específico, além de responder a pushes na branch principal.

## Como Funciona

1. Quando você envia alterações para a branch principal do GitHub, o sistema inicia automaticamente o processo de atualização do seu site ou aplicativo.
2. O sistema também está programado para fazer essa atualização automaticamente em um horário específico (no caso, às 1h da manhã do dia 2 de janeiro, no horário de Brasília).
3. Você receberá mensagens no Slack e por e-mail informando se a atualização foi agendada e quando ela for concluída com sucesso.


O workflow é dividido em dois jobs principais:

1. **notify-and-schedule**: 
   - Acionado por pushes na branch `main` e pelo cronograma definido.
   - Envia notificações de agendamento via Slack e e-mail.

2. **deploy**:
   - Executado apenas no evento agendado.
   - Realiza o checkout do código.
   - Conecta-se ao servidor VPS via SSH e atualiza o código.
   - Envia notificações de sucesso após o deploy.

## Configuração

Para utilizar este workflow, você precisa configurar os seguintes secrets no seu repositório GitHub:

- `SLACK_WEBHOOK`: URL do webhook do Slack para notificações.
- `EMAIL_HOST`: Endereço do servidor de e-mail.
- `EMAIL_PORT`: Porta do servidor de e-mail.
- `EMAIL_USERNAME`: Nome de usuário do e-mail.
- `EMAIL_PASSWORD`: Senha do e-mail.
- `EMAIL_TO`: Endereço de e-mail para receber as notificações.
- `HOST`: Endereço IP ou hostname do seu servidor VPS.
- `USER`: Nome de usuário para acesso SSH ao VPS.
- `PASS`: Senha para acesso SSH ao VPS.
- `PORT`: Porta SSH do seu VPS (geralmente 22).

## Personalização

Você pode personalizar este workflow editando o arquivo `.github/workflows/deploy.yml`:

- Modifique o cronograma de execução ajustando a linha `cron`.
- Altere o caminho do projeto no servidor VPS na seção `script` do job `deploy`.
- Personalize as mensagens de notificação conforme necessário.

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests com melhorias ou correções.
