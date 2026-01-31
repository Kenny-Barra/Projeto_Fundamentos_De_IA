# Projeto_Fundamentos_De_IA

## 🛠️ Tecnologias Utilizadas

Este projeto integra diversas tecnologias e serviços para compor a solução completa:

###Make.com (Integromat)

Plataforma de automação visual onde todo o fluxo foi construído sem a necessidade de programar do zero. Aqui definimos os módulos de escuta do Telegram, routers lógicos, chamadas à IA e integração com e-mail. O Make orquestra todas as etapas automaticamente conforme o desenho do cenário.

###Agente de IA Nativo (Make AI Agent – modelo small)

Serviço de Inteligência Artificial fornecido pelo próprio Make.com (Beta) que permite rodar modelos de linguagem (LLMs) integrados ao cenário. Utilizamos o modelo small para gerar os textos com base no prompt configurado. Essa IA generativa é similar a um modelo GPT, capaz de produzir conteúdo textual a partir das instruções dadas.

###Telegram Bot

Interface de conversação com o usuário final. Criamos um bot no Telegram (@textoiabot) através do BotFather e conectamos ao Make.com via a API do Telegram. Ele envia as perguntas ao usuário e retorna as respostas geradas, proporcionando uma experiência de chat interativa.

###Data Store (Make.com)

Banco de dados interno do Make utilizado para armazenar o estado da conversa e os dados fornecidos pelo usuário durante a interação. Cada usuário/solicitação possui um registro com campos como “Tipo”, “Tópicos”, “Tom”, “Canal”, “E-mail” e “Etapa Atual”. Isso permite que múltiplos passos ocorram em sequência, mesmo que o cenário seja acionado várias vezes (uma vez por mensagem recebida), mantendo contexto entre as execuções.

###Gmail (Integração de E-mail)

Serviço de e-mail usado para enviar o texto gerado caso o usuário opte por receber o resultado na caixa de entrada. Configuramos uma conexão com o Gmail via Make.com, de modo que a automação consiga compor e enviar e-mails em nome do usuário ou de uma conta designada, contendo o conteúdo solicitado.

(Também foram usadas ferramentas auxiliares do Make, como módulos “Tools” e cenários Router, para manipular variáveis e direcionar o fluxo condicionalmente, assegurando que cada resposta do usuário desencadeie a próxima ação apropriada.)
