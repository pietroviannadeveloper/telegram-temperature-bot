# Bot de Clima Utilizando OpenWeather (n8n)

Este repositório contém um workflow do n8n que integra um bot do Telegram com a API da OpenWeatherMap para retornar clima e temperatura em tempo real para a cidade informada pelo usuário.

## Arquivo do workflow

- `Bot de Clima Utilizando OpenWeather.json` :contentReference[oaicite:0]{index=0}

## Requisitos

- n8n (Community Edition ou Cloud)
- Token de bot do Telegram (BotFather)
- Chave de API da OpenWeatherMap

## Funcionalidade

O workflow:
1. Recebe mensagens via `Telegram Trigger`.
2. Valida se a mensagem começa com `clima` ou `temperatura` (com ou sem `/`) usando um nó `If` com regex.
3. Extrai o nome da cidade do texto da mensagem.
4. Consulta o OpenWeatherMap com idioma `pt_br`.
5. Responde no mesmo chat do Telegram com:
   - Nome da cidade retornado pela API
   - Descrição do tempo
   - Temperatura (arredondada)
   - Sensação térmica (arredondada)

Mensagens que não seguem o padrão recebem uma instrução de uso.

## Comandos suportados

O nó `If` aceita mensagens iniciadas por:

- `clima <cidade>`
- `temperatura <cidade>`
- `/clima <cidade>`
- `/temperatura <cidade>`

Exemplos:
- `clima São Paulo,br`
- `temperatura Rio de Janeiro,br`
- `/clima berlin,de`

## Como importar no n8n

1. Abra o n8n.
2. No menu do editor, selecione a opção de importar workflow (ex.: “Import from file”).
3. Selecione o arquivo `Bot de Clima Utilizando OpenWeather.json`.
4. Salve o workflow.

## Configuração de credenciais (obrigatório)

Este workflow utiliza credenciais do n8n (não há segredos “hardcoded” no JSON).

### Telegram
- Crie uma credencial do tipo Telegram (Telegram API).
- Informe o token do bot (BotFather).
- No workflow, associe essa credencial aos nós:
  - `Telegram Trigger`
  - `Telegram`
  - `Send a text message`

### OpenWeatherMap
- Crie uma credencial do tipo OpenWeatherMap.
- Informe a API key.
- No workflow, associe essa credencial ao nó:
  - `OpenWeatherMap`

## Configurações já aplicadas no workflow

- Validação do comando via regex: `^(\/)?(clima|temperatura)\b` (case-insensitive). :contentReference[oaicite:1]{index=1}
- Extração dinâmica da cidade a partir do texto recebido (remove o comando e espaços). :contentReference[oaicite:2]{index=2}
- Idioma do retorno configurado para `pt_br` no OpenWeatherMap. :contentReference[oaicite:3]{index=3}
- Mensagem de resposta inclui o nome da cidade retornado pela API e arredonda temperatura/sensação. :contentReference[oaicite:4]{index=4}
- Mensagem de instrução no caminho “false” do `If`. :contentReference[oaicite:5]{index=5}

## Execução em produção

- Em instalações onde o workflow puder ser ativado/publicado, deixe o workflow ativo para responder automaticamente.
- Se o n8n estiver rodando localmente e o Telegram Trigger estiver em modo webhook, o n8n precisa estar acessível publicamente (HTTPS) para receber atualizações do Telegram. Alternativas comuns incluem rodar em um servidor ou usar um túnel (ex.: Cloudflare Tunnel/ngrok), dependendo da sua arquitetura.

## Solução de problemas

- Resposta em inglês:
  - Confirme que o nó OpenWeatherMap está com `language = pt_br`. :contentReference[oaicite:6]{index=6}

- Não responde ao enviar mensagem:
  - Verifique se o workflow está ativo/publicado no n8n.
  - Verifique se o Telegram Trigger está recebendo updates (saída do nó).

- Cidade não encontrada:
  - O usuário deve tentar `cidade,país` (ex.: `Santos,br`) para reduzir ambiguidade.
