# Política de privacidade da Hina

Última atualização: 2 de outubro de 2026 · [English](PRIVACY.en.md)

## Em uma frase

A Hina roda no seu computador. O que sai dele é o que você manda para os provedores de IA que você
mesmo configura com as suas chaves, mais o pouco que o app precisa para abrir o avatar e procurar
atualização. Não existe servidor da Hina recebendo os seus dados.

## 1. Quem é responsável

A Hina é mantida pelo **Project H.I.N.A.** e é gratuita para uso pessoal
([licença](https://github.com/Project-H-I-N-A/hina-releases/blob/main/LICENSE)). Ela não tem conta
de usuário, não pede cadastro e não cobra nada: as chaves de API são suas, e cada provedor cobra
você diretamente.

Contato: abra uma issue em
[github.com/Project-H-I-N-A/hina-releases/issues](https://github.com/Project-H-I-N-A/hina-releases/issues).
As issues são públicas: não coloque nelas dados pessoais, chaves de API nem trechos de conversa.

## 2. O que fica só no seu computador

Tudo isto fica na pasta de dados do app e nunca é enviado pela Hina:

- **Windows:** `%APPDATA%\Hina`
- **macOS:** `~/Library/Application Support/Hina`
- **Linux:** `~/.config/Hina`

O que fica lá:

- **Memória da conversa:** histórico, fatos que ela guarda sobre você e o índice de busca, um banco
  por par avatar + persona. Você vê, edita e apaga tudo na aba Memória da Dashboard.
- **Personalidade:** o perfil de estilo que evolui com o uso.
- **Telemetria de uso:** tempo de resposta, tokens e custo estimado de cada turno, para a Dashboard
  mostrar o seu gasto. Fica num banco local e pode ser desligada em Configurações.
- **Registro do servidor** (`logs/server.log`): mensagens técnicas, que podem citar trechos do que
  você disse.
- **Suas chaves de API:** no cofre do sistema (Credential Manager no Windows, Keychain no macOS,
  Secret Service no Linux). O app instalado não grava chaves em texto.
- **Configuração e preferências** da interface.

Desinstalar o app **não apaga** essa pasta. Para apagar tudo, remova a pasta depois de desinstalar.

## 3. O que sai do seu computador, e para quem

A Hina só manda dados para serviços que você escolheu e configurou com a sua própria chave, com uma
exceção (a voz de reserva, abaixo). Cada serviço tem a própria política de privacidade e as próprias
regras de retenção; a Hina não controla o que eles fazem com o que recebem.

| O que é enviado | Para onde | Quando |
|---|---|---|
| O texto da conversa: o que você escreve ou fala, mais o contexto de memória que a Hina anexa | O provedor de linguagem escolhido em Configurações. Padrão: Google Gemini. Alternativas: Groq, OpenAI, xAI e OpenRouter | Em todo turno de conversa |
| O áudio do seu microfone | O provedor de reconhecimento de fala: Deepgram (padrão), Groq Whisper (sem chave da Deepgram) ou Google (modo Live) | Só enquanto a escuta está ligada (botão do microfone ou push-to-talk) |
| O texto das respostas, para virar voz | ElevenLabs (padrão), Google Gemini ou Cartesia. **Sem nenhuma chave de voz**, o serviço gratuito edge-tts da Microsoft (`speech.platform.bing.com`) | Em toda resposta falada. A voz de reserva funciona mesmo sem você configurar nada |
| Capturas da sua tela | O modelo de visão (padrão: Google Gemini) | Só quando você liga "Ver a tela" no menu do pet ou a "Percepção contínua da tela" (desligada por padrão). A opção "Ocultar segredos vistos na tela (privacidade)" tenta apagar senhas e chaves antes do envio, sem garantia |
| O áudio do computador (o que está tocando) | O provedor de fala ou, se você ligar a identificação de música, o ACRCloud | Só com "Ouvir áudio do PC" ligado no menu do pet |
| Imagens da sua câmera | **Ninguém.** O rastreamento facial roda dentro do app (MediaPipe) | Só com "Rastreamento facial" ligado. Os arquivos do modelo são baixados de `cdn.jsdelivr.net` e `storage.googleapis.com` na primeira vez |
| Conteúdo de arquivos, resultado de comandos e páginas lidas pelo agente | O provedor de linguagem | Quando você pede uma ação ao agente. Ferramentas que escrevem, apagam ou executam pedem a sua confirmação, a não ser que você marque "sempre permitir" |
| Dados dos conectores (agenda, e-mail, Spotify, Telegram, Discord) | O provedor de linguagem e o próprio serviço conectado | Só se você conectar o serviço na Dashboard |
| A conversa inteira | O Hermes Agent, se você o instalar e ligar, e daí para o provedor configurado no perfil dele | Só no modo Hermes. A memória e o aprendizado da Hina ficam pausados nesse modo |
| Métricas de latência (tempos e tamanhos, sem o texto) | Langfuse | Só se você configurar as chaves do Langfuse e ligar o envio |

## 4. Conexões que o app faz sozinho

Mesmo sem chave nenhuma, o app instalado faz estas requisições:

- **`cubism.live2d.com`:** o núcleo do Live2D, carregado toda vez que a janela abre. Ele não vem no
  instalador por causa da licença.
- **`cdn.jsdelivr.net`:** a biblioteca de avatares Spine, só se você usar um avatar Spine.
- **`github.com`:** cerca de 30 segundos depois de abrir, a Hina verifica se há versão nova em
  `Project-H-I-N-A/hina-releases`. Nenhum dado seu vai nessa verificação, e a atualização só é
  baixada e instalada se você confirmar.
- **`speech.platform.bing.com`:** a voz de reserva da Microsoft, só quando não há chave de voz.

## 5. Rede local e sincronização

A Hina só aceita conexões do próprio computador (`127.0.0.1`). O acesso pela rede local e a
sincronização entre computadores vêm desligados e sem interface; ligar exige editar a configuração e
definir um token.

## 6. Pacote de suporte

Em Configurações há "Baixar pacote de suporte": um zip com versão, sistema, provedores, flags, a
configuração com os valores das chaves apagados e o fim do registro do servidor. Ele só é criado
quando você clica, e só vai para onde você mandar. O registro pode citar trechos da conversa:
revise antes de enviar.

## 7. Seus controles

- **Apagar memória, fatos e histórico:** Dashboard, aba Memória.
- **Desligar telemetria, visão, escuta, áudio do PC e rastreamento facial:** Configurações e o menu
  do pet.
- **Trocar ou remover chaves:** Configurações. Remover a chave desliga o serviço correspondente.
- **Apagar tudo:** desinstale, remova a pasta de dados (§2) e apague as entradas da Hina no cofre do
  sistema.

## 8. O que a Hina não faz

Não tem conta nem analytics próprio, não envia relatório de erro automático, não vende nem
compartilha dados e não usa os seus dados para treinar nada. Se um provedor usa o que recebe para
treinar modelos, isso é regra dele e depende do plano que você contratou (planos gratuitos costumam
permitir). Confira a política de cada provedor que você configurar.

## 9. Mudanças nesta política

Toda mudança aparece nas notas da versão que a traz, e o texto novo vale a partir dessa versão. A
data no topo deste arquivo indica a última atualização.
