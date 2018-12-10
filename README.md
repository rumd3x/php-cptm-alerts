# php-cptm-alerts
Notificações em tempo real sobre mudanças de status nas linhas dos trens e metrôs de São Paulo diretamente no canal do Slack.

![Notificação Exemplo](/docs/images/notificacoes.png)

## Getting started
### Workspace
1. Você precisará de um Workspace no slack. Se não tiver [crie-o](https://slack.com/get-started)

### Token
1. Você precisará gerar um token para o seu Workspace se comunicar com o projeto.

2. Para isso [crie um App no seu Workspace](https://api.slack.com/apps)

![App no Workspace](/docs/images/app.jpg)

3. Após criado o App, vá até **Bot Users** no menu lateral e crie um Bot para seu App.

4. Após criado o Bot, vá até **OAuth & Permissions** no menu lateral. Na seção **Scope** dê a permissão *chat:write:bot* e *bot* para o seu App. Será solicitado que o App seja reinstalado no Workspace para as novas permissões.

![App configurado corretamente](/docs/images/appconfig.jpg)

5. Após dadas as permissões e reinstalado o App salve a **Bot User OAuth Access Token** ela será necessária para configurar o projeto.

### Configurando o Projeto

1. Clone o repositório para uma pasta em seu servidor: 
```sh
git clone https://github.com/rumd3x/php-cptm-alerts.git
```

2. Vá até a pasta do projeto: `cd php-cptm-alerts`.

3. Instale as dependências: `composer install`.

4. Crie o seu arquivo de configurações do projeto: `cp .env.example .env`.

5. Edite o arquivo `.env`. Em `SLACK_CHANNEL` coloque o canal do slack em que o bot publicará as alterações de status. Em `SLACK_KEY` coloque o **Bot User OAuth Access Token** salvo anteriormente.

6. Para verificar o status das linhas execute `php /caminho/do/projeto/run.php`.

7. Para receber automaticamente as mudanças de status coloque o comando num cron. Exemplo:
```sh
* * * * * php /caminho/do/projeto/run.php >> /caminho/do/log/run.log 2>&1
```

### Debugando
#### Se você fez tudo acima corretamente e não está recebendo notificações em seu canal do slack:
* Verifique se o composer foi executado corretamente
* Verifique a saída do php nos logs do cron (Ou execute o comando redirecionando a saída para um arquivo).
* Verifique os logs do projeto  no arquivo `/caminho/do/projeto/Storage/Logs/app.log`
* Verifique se o usuário rodando o php está no grupo de permissões correto
* Verifique se o arquivo *.env* tem permissão de leitura 
* Verifique se a pasta *Storage* tem permissão de escrita

## Todo
* Rodar o projeto em um Container do Docker.
* Funcionalidade para permitir receber notificações apenas de **linhas especifícas**.
* Funcionalidade para permitir receber notificações apenas de **eventos específicos**.
* Funcionalidade para permitir notificações apenas em **dias específicos**. 
