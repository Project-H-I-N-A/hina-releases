# Hina — guia de uso

A Hina é uma companheira VTuber que mora na sua tela: um avatar animado que conversa por voz ou
texto, lembra do que você contou, pode agir no seu computador quando você permite e, se quiser, cuida
da sua casa conectada. Este guia é para quem instalou a Hina pelo instalador. Rodar a partir do
código-fonte é assunto do repositório de desenvolvimento, não deste guia.

Versão deste guia: 09/10/2026 (Hina 0.3.x, pré-lançamento). Os instaladores ainda **não são
assinados**; o sistema vai avisar, e abaixo está o que fazer.

- [1. Instalar](#1-instalar)
- [2. Chaves de API](#2-chaves-de-api)
- [3. Primeira conversa](#3-primeira-conversa)
- [4. Agente (ações no computador)](#4-agente-ações-no-computador)
- [5. Hermes (opcional, experimental)](#5-hermes-opcional-experimental)
- [6. Atualizar](#6-atualizar)
- [7. Desinstalar](#7-desinstalar)
- [8. Onde ficam seus dados](#8-onde-ficam-seus-dados)
- [9. Problemas comuns](#9-problemas-comuns)
- [10. Privacidade, licença e contato](#10-privacidade-licença-e-contato)

## 1. Instalar

Baixe o arquivo do seu sistema na página de
[Releases](https://github.com/Project-H-I-N-A/hina-releases/releases). O instalador tem entre 200 e
280 MB; o app instalado ocupa cerca de 560 MB. Precisa de internet: a Hina conversa com serviços de IA
na nuvem (veja [Chaves de API](#2-chaves-de-api)).

**Windows 10/11** — `Hina Setup x.y.z.exe`. Abra o instalador e escolha a pasta (o padrão é
`%LOCALAPPDATA%\Programs\Hina`). O SmartScreen vai mostrar "Editor desconhecido": clique em *Mais
informações* → *Executar assim mesmo*. Isso acontece porque o instalador ainda não é assinado.

**macOS (Apple Silicon)** — `Hina-x.y.z-arm64.dmg`. Arraste a Hina para *Aplicativos*. Na primeira
abertura o macOS pode dizer que o app "está danificado": não é download corrompido, é a falta de
assinatura. Abra o Terminal e rode:

```
xattr -cr /Applications/Hina.app
```

Depois abra a Hina normalmente. Ela vai pedir **Microfone** (para ouvir você) e, se você usar a
visão da tela, **Gravação de Tela**, em Ajustes do Sistema → Privacidade e Segurança.

**Linux** — `Hina-x.y.z.AppImage` (dê permissão de execução e abra), `hina_x.y.z_amd64.deb`
(`sudo apt install ./hina_x.y.z_amd64.deb`) ou `hina-x.y.z.tar.xz`. No Wayland a Hina usa um host
próprio para o pet ficar sobre as janelas; no GNOME ela abre como janela comum.

A Hina abre como **pet**: o avatar fica sobre as outras janelas, sem moldura. Pelo ícone na bandeja
do sistema você acessa *Falar (push-to-talk)*, *Ver a tela*, *Interromper fala*, *Mostrar/ocultar
chat*, *Clique atravessa*, *Fixar no topo* e *Sair*.

## 2. Chaves de API

A Hina não tem conta nem assinatura própria: ela usa a **sua** chave de um provedor de IA, e você
paga direto ao provedor pelo que usar. No primeiro boot um assistente de três passos explica isso,
mostra a estimativa de custo por hora de conversa e aponta a política de privacidade.

1. Crie uma chave em um provedor. Qualquer uma destas basta para conversar e usar o agente: **Groq**
   (rápido, recomendado), **Gemini**, **OpenAI**, **OpenRouter** ou **xAI**. O modo Live (voz em
   tempo real) precisa de uma chave do Gemini.
2. Abra a **Dashboard** (ícone na ilha de controles do avatar ou pelo chat) → **Configurações →
   Chaves**, cole a chave e salve. O botão *Obter chave ↗* abre a página do provedor.
3. Opcionais, na mesma página: **ElevenLabs** ou **Cartesia** (vozes de maior qualidade), **Deepgram**
   (ouvido em streaming). Sem elas a Hina usa as vozes e o ouvido de reserva, que já funcionam.

As chaves ficam no cofre do seu sistema (Credential Manager no Windows, Keychain no macOS, Secret
Service no Linux), nunca em texto puro. A estimativa do assistente (preços de lista de outubro de
2026) fica em torno de US$ 0,40 por hora de conversa com os padrões (cérebro 0,07, voz ElevenLabs
0,29, ouvido Groq 0,04); o pior caso, ouvido em streaming (Deepgram) ligado a hora inteira, chega a
US$ 0,83.

## 3. Primeira conversa

- **Por texto:** abra o chat (ícone da ilha ou bandeja → *Mostrar/ocultar chat*) e digite. Enter envia.
- **Por voz:** toque no microfone da ilha de controles para a escuta automática, ou **segure** para
  falar e solte. Pelo bandeja, *Falar (push-to-talk)* faz o mesmo. Em Configurações → Ouvido dá para
  ligar a palavra de ativação ("ei Hina") e ajustar quanto silêncio ela espera antes de responder.
- **Interromper:** fale por cima ou clique em *Interromper fala* na bandeja.
- **Avatar e voz:** os ícones da ilha trocam o avatar (Live2D, VRM ou PNGTuber) e a voz. A persona
  (jeito de falar, humor, memórias) é editada na Dashboard → **Persona**.
- **Modo janela:** pelo chat você pode *Abrir no navegador*; a Hina vira uma página normal
  (`http://127.0.0.1:8000`) com os mesmos controles, e o pet fecha. Para voltar, *Voltar ao modo pet*.
- **Memória:** ela lembra entre sessões. Em Dashboard → **Memória** você vê, busca e apaga o que
  ficou guardado.

Dica: a Hina responde em português por padrão. Em Configurações → Geral → *Idioma da interface* você
troca a interface para English; a persona segue o idioma em que você fala com ela.

## 4. Agente (ações no computador)

Com o agente ligado a Hina lê arquivos, pesquisa na web, roda comandos, abre programas, cria tarefas
em segundo plano e, se você permitir, usa o navegador e controla a tela. Tudo isso fica **desligado
até você ligar**.

1. Dashboard → **Agente** → ligue o agente.
2. Escolha a **pasta raiz**: o agente só enxerga essa pasta (e as *Pastas extras autorizadas* que
   você adicionar). No pet, *Definir a pasta raiz da Hina* abre o seletor do sistema.
3. Permissões: por padrão cada ação sensível (escrever arquivo, rodar comando, mandar mensagem)
   **pede sua confirmação** na tela, com os argumentos completos. Você responde *uma vez*, *sempre*
   ou *negar*. Em Dashboard → Agente dá para liberar ou bloquear ferramenta por ferramenta.
4. Leitura (arquivos e web) e tarefas em segundo plano (**Kanban**) aparecem na janela de atividade
   do pet; cada tarefa mostra o que fez.

O que o agente não faz: sair da pasta raiz, usar chaves de API que não são do serviço escolhido, ou
executar algo que você negou. Se a Hina disser que fez algo, ela mostra a evidência (saída do comando,
arquivo criado).

## 5. Hermes (opcional, experimental)

O Hermes é um agente externo (Nous Research) que pode assumir o "cérebro" da Hina. Nesta versão ele
**não vem no instalador**: precisa estar instalado e configurado na máquina por você, e a Hina o usa
pelo perfil `hina-chat`. Enquanto o Hermes está ativo, o agente nativo fica em espera.

Liga e desliga em Dashboard → **Agente → Hermes**. Se o Hermes não responder, a Hina avisa e volta
ao cérebro nativo sozinha. Trate como experimental: o conjunto de testes do Hermes ainda está sendo
fechado para o 1.0.

## 6. Atualizar

A Hina verifica novas versões ao abrir e avisa quando há uma. Em Dashboard → **Configurações →
Atualizações** você escolhe receber **versões beta** (chegam antes, podem ter defeitos) ou só as
estáveis.

- **Windows e Linux:** a atualização baixa e instala sozinha quando você aceita.
- **macOS:** enquanto o app não é assinado, a atualização automática não funciona. Baixe o `.dmg`
  novo, substitua a Hina em *Aplicativos* e repita o `xattr -cr`. Seus dados e chaves ficam.

No Windows o instalador guarda uma cópia de si mesmo (~216 MB) em `%LOCALAPPDATA%\hina-updater`
para a atualização automática; pode apagar à mão sem afetar o app.

## 7. Desinstalar

**Windows:** Configurações → Aplicativos → Hina → Desinstalar (ou `Uninstall Hina.exe` na pasta do
programa). Depois, se quiser apagar tudo: `%APPDATA%\Hina` (dados, memória, configuração),
`%LOCALAPPDATA%\hina-updater` e as entradas "com.rhayron.hina" no Gerenciador de Credenciais.

**macOS:** arraste a Hina de *Aplicativos* para o Lixo. Dados em
`~/Library/Application Support/Hina`; chaves no Keychain (busque "com.rhayron.hina").

**Linux:** apague o AppImage ou `sudo apt remove hina`. Dados em `~/.config/Hina`; chaves no cofre
do sistema (Secret Service).

Os dados apagados não voltam: a memória da Hina fica só nessa pasta.

## 8. Onde ficam seus dados

| O quê | Onde | Sai do seu computador? |
|---|---|---|
| Configuração (`config.yaml`), personas, memória, telemetria | pasta de dados acima | não |
| Chaves de API | cofre do sistema | só para o provedor da chave |
| Conversas | enviadas ao provedor de IA escolhido para gerar a resposta | sim, ao provedor |
| Áudio do microfone | enviado ao provedor de ouvido (STT) só enquanto a escuta está ativa | sim, ao provedor |
| Tela (visão) | só quando você aciona *Ver a tela* ou liga a visão | sim, ao provedor |
| Logs | `logs/` na pasta de dados; o *pacote de suporte* da Dashboard redige chaves | só se você enviar |

A política completa está em [PRIVACY.md](https://github.com/Project-H-I-N-A/hina-releases/blob/main/PRIVACY.md).

## 9. Problemas comuns

- **"Hina não conseguiu iniciar" / "O servidor interno não respondeu".** Outra Hina já está aberta
  ou algo ocupa a porta 8000. Feche a outra instância (bandeja → Sair) e abra de novo. O caminho do
  log aparece no aviso.
- **"Outro serviço ocupa a porta da Hina: identidade não verificada."** Há um programa estranho na
  porta 8000. A Hina se recusa a usar a tela dele por segurança. Feche o programa e reabra a Hina.
- **Ela não me ouve.** Confira a permissão de microfone do sistema e o dispositivo em Configurações →
  Ouvido. O ouvido fica desligado até existir a chave do motor escolhido (Groq por padrão; Deepgram,
  ElevenLabs Scribe ou Gemini se você trocou).
- **Ela responde "não sei fazer isso" para uma ação.** O agente está desligado ou a ferramenta foi
  bloqueada em Dashboard → Agente.
- **Voz de reserva em vez da escolhida.** A chave do provedor de voz acabou ou está inválida; a Hina
  tenta de novo em 10 minutos.
- **macOS diz que o app está danificado.** Veja [Instalar](#1-instalar): `xattr -cr`.
- **Outro dispositivo na rede não acessa.** Por padrão a Hina só atende no próprio computador. O
  acesso pela rede exige HTTPS e um token; é configuração avançada, fora deste guia.

## 10. Privacidade, licença e contato

- [Licença](https://github.com/Project-H-I-N-A/hina-releases/blob/main/LICENSE): gratuita para uso
  pessoal e não comercial; todos os direitos reservados.
- [Política de privacidade](https://github.com/Project-H-I-N-A/hina-releases/blob/main/PRIVACY.md).
- Bugs e dúvidas: [issues do hina-releases](https://github.com/Project-H-I-N-A/hina-releases/issues).
  As issues são públicas: não cole chaves, dados pessoais nem trechos de conversa. Prefira anexar o
  *pacote de suporte* (Dashboard → Configurações → Geral → Suporte → *Baixar pacote de suporte*), que já
  redige segredos.
