# Projeto_Fundamentos_De_IA

## 📋 Sobre o Projeto

Este projeto demonstra um copiloto de Inteligência Artificial capaz de gerar textos corporativos sob demanda. Destinado a profissionais e equipes que precisam agilizar a redação de comunicados, o bot integra IA generativa para produzir conteúdos como e-mails, avisos institucionais ou resumos de reunião de forma rápida e personalizada. Basta informar o tipo de texto desejado, os tópicos a abordar, o tom da mensagem e escolher o canal de entrega. Em poucos passos, o usuário recebe um texto pronto, coeso e no estilo requerido – diretamente no Telegram ou por e-mail.

🔗 Projeto público no Make.com: [TextoIA Project](https://us2.make.com/public/shared-scenario/SAZmoqawQ31/texto-ia-project)

🤖 Bot no Telegram: @textoiabot [(clique para iniciar a conversa)](https://t.me/textoiabot)

📹 Vídeo do projeto: [(clique para assitir ao Vídeo Pitch)](https://youtu.be/1U8lJZmEshY)

## Como funciona o projeto (visão geral)

O fluxo de automação foi desenvolvido na plataforma Make.com (antigo Integromat) usando diversos módulos integrados. A seguir, explicamos o passo a passo de como a interação acontece do início ao fim:

### Passo a passo do fluxo de automação

- **Início via Telegram:** O usuário envia uma mensagem ou comando de start para o bot no Telegram. Isso aciona o módulo Telegram Bot – Watch Updates no Make.com, disparando o cenário de automação. Imediatamente, o bot responde com uma saudação e explica que pode ajudar a criar textos com IA, iniciando a coleta de informações.

- **Pergunta sobre o tipo de texto:** O bot pergunta ao usuário que tipo de texto corporativo ele deseja gerar. Exemplos: “E-mail”, “Aviso Institucional” ou “Resumo de Reunião”. Assim que o usuário responde com o tipo de texto, o cenário registra essa informação em um Data Store (banco de dados interno do Make) junto com a identificação do usuário, e passa para a próxima etapa.

- **Pergunta sobre os tópicos:** Em seguida, o bot solicita os tópicos ou pontos-chave que devem ser abordados no texto. O usuário fornece uma lista de assuntos ou detalhes importantes. A resposta é novamente armazenada no Data Store vinculada à conversa do usuário, enriquecendo o registro com os tópicos desejados.

- **Pergunta sobre o tom do texto:** O bot então pergunta qual tom de voz o texto deve ter. Pode ser um tom formal, informal, instrutivo, motivacional, etc., conforme a necessidade institucional. O usuário especifica o tom (por exemplo, “formal e direto” ou “mais casual”). Essa preferência também é salva no Data Store para ser usada na geração do texto.

- **Pergunta sobre o canal de entrega:** Por fim, o bot questiona onde o usuário quer receber o texto pronto: pelo próprio Telegram ou via e-mail. Se o usuário optar por Telegram, o fluxo seguirá para enviar a resposta no chat mesmo. Se a opção for e-mail, o bot pedirá em seguida o endereço de e-mail desejado (caso não tenha sido fornecido junto da resposta). O usuário fornece o e-mail, que é armazenado no Data Store na mesma ficha da requisição.

- **Geração do texto com IA:** Com todos os dados coletados (tipo de texto, tópicos, tom e canal/email), o cenário prossegue para a etapa de geração de conteúdo. Aqui é utilizado o módulo Make an AI Agent (Beta) – um agente de IA nativo do Make.com (usando um modelo LLM “small”). O cenário envia ao agente de IA um prompt cuidadosamente elaborado que inclui as preferências fornecidas pelo usuário. Em resposta, o agente de IA produz um texto corporativo completo, coerente e adequado às especificações dadas.

- **Entrega do resultado:** Assim que o conteúdo é gerado pela IA, o fluxo encaminha o texto final pelo canal escolhido:

  - Se o usuário escolheu Telegram, o bot envia uma mensagem no chat contendo o texto gerado, formatado e prontinho para uso.
  
  - Se o usuário preferiu e-mail, o cenário utiliza o módulo Gmail (integração do Make.com com o Gmail) para enviar o texto diretamente para o endereço fornecido. O usuário recebe o e-mail com o conteúdo em sua caixa de entrada, podendo então repassar ou ajustar conforme necessário.

- **Encerramento e reset:** Após enviar o texto, o bot finaliza o fluxo daquela solicitação. O registro correspondente no Data Store pode ser atualizado ou encerrado (marcando que o fluxo foi concluído). O bot então envia uma mensagem de conclusão ou fica pronto para uma nova solicitação. Caso o usuário queira gerar outro texto, basta iniciar novamente o processo. Com o fluxo encerrado, uma nova interação começará do zero, ou seja, será solicitado o tipo do próximo texto e assim por diante.

<img width="1286" height="641" alt="download" src="https://github.com/user-attachments/assets/4226c914-a15c-402f-b5e2-73556eef9096" />

Diagrama do cenário no Make.com (Make Scenario): O desenho acima ilustra o fluxo implementado. Nele, cada ícone representa uma etapa: começando pelo disparador do Telegram, passando por diversas operações no Data Store (armazenando e recuperando informações do usuário) e uso de routers (condicionais) para direcionar o caminho correto, até chegar no módulo AI Agent (círculo roxo) que gera o texto, seguido dos módulos de envio pelo Telegram ou Email.

### Descrição escrita do fluxo da automação (detalhado)

Quando o usuário entra em contato pelo Telegram, a automação inicia registrando essa interação. O cenário verifica no Data Store se já existe um registro de conversa em andamento com aquele usuário ou se é um novo pedido. Caso seja uma nova solicitação, o sistema cria um registro no Data Store para acompanhar as respostas do usuário passo a passo. Em seguida, o bot envia uma mensagem de boas-vindas explicando sua função e já pergunta qual é o tipo de texto desejado.

À medida que o usuário responde a cada pergunta, o cenário atualiza o registro no Data Store com a informação correspondente (tipo de texto, tópicos, tom, etc.) e avança para a próxima etapa. Essa progressão é controlada por módulos de decisão (Router): por exemplo, após armazenar o tipo de texto, a automação sabe que a próxima pergunta deve ser sobre os tópicos; uma vez recebidos os tópicos, encaminha para perguntar o tom do texto, e assim sucessivamente. Cada resposta do usuário é encaminhada pelo Telegram ao Make.com, que a mapeia para o campo correto no Data Store e determina qual será a próxima mensagem do bot.

Quando todas as informações necessárias estão coletadas no Data Store, o cenário ativa o módulo Make AI Agent para gerar o conteúdo final. Nesse momento, o agente de IA recebe um prompt consolidado com todos os detalhes fornecidos (tipo + tópicos + tom) e possivelmente instruções adicionais para formatar o texto em um contexto corporativo adequado. O modelo de IA então produz o texto solicitado. Assim que a resposta da IA é retornada ao cenário, a automação verifica o canal escolhido pelo usuário. Se for Telegram, o texto gerado é imediatamente enviado de volta ao chat do usuário via módulo do Telegram Bot. Se o canal selecionado for e-mail, o cenário utiliza o módulo Gmail para compor um e-mail contendo o texto e enviá-lo para o endereço fornecido (tudo isso de forma automática).

Por fim, o fluxo realiza qualquer limpeza ou ajuste necessário — por exemplo, marca o registro no Data Store como concluído ou reinicializa o estado daquela conversa. Caso o usuário envie alguma mensagem como “cancelar” no meio do processo, a automação possui lógica de cancelamento que interrompe o fluxo atual e reseta o registro, permitindo começar novamente se desejado. Da mesma forma, se o usuário digitar “voltar” em alguma etapa, o cenário identifica esse comando e pode retornar à pergunta anterior, ajustando o estágio no Data Store para refletir a etapa correta. Esses cuidados garantem que a informação flua de maneira organizada: desde o primeiro contato no Telegram, passando pelo armazenamento estruturado no Data Store, pela geração inteligente via IA, até a entrega final no canal apropriado.

## 🛠️ Tecnologias Utilizadas

Este projeto integra diversas tecnologias e serviços para compor a solução completa:

### Make.com (Integromat)

Plataforma de automação visual onde todo o fluxo foi construído sem a necessidade de programar do zero. Aqui definimos os módulos de escuta do Telegram, routers lógicos, chamadas à IA e integração com e-mail. O Make orquestra todas as etapas automaticamente conforme o desenho do cenário.

### Agente de IA Nativo (Make AI Agent – modelo small)

Serviço de Inteligência Artificial fornecido pelo próprio Make.com (Beta) que permite rodar modelos de linguagem (LLMs) integrados ao cenário. Utilizamos o modelo small para gerar os textos com base no prompt configurado. Essa IA generativa é similar a um modelo GPT, capaz de produzir conteúdo textual a partir das instruções dadas.

### Telegram Bot

Interface de conversação com o usuário final. Criamos um bot no Telegram (@textoiabot) através do BotFather e conectamos ao Make.com via a API do Telegram. Ele envia as perguntas ao usuário e retorna as respostas geradas, proporcionando uma experiência de chat interativa.

### Data Store (Make.com)

Banco de dados interno do Make utilizado para armazenar o estado da conversa e os dados fornecidos pelo usuário durante a interação. Cada usuário/solicitação possui um registro com campos como “Tipo”, “Tópicos”, “Tom”, “Canal”, “E-mail” e “Etapa Atual”. Isso permite que múltiplos passos ocorram em sequência, mesmo que o cenário seja acionado várias vezes (uma vez por mensagem recebida), mantendo contexto entre as execuções.

### Gmail (Integração de E-mail)

Serviço de e-mail usado para enviar o texto gerado caso o usuário opte por receber o resultado na caixa de entrada. Configuramos uma conexão com o Gmail via Make.com, de modo que a automação consiga compor e enviar e-mails em nome do usuário ou de uma conta designada, contendo o conteúdo solicitado.

(Também foram usadas ferramentas auxiliares do Make, como módulos “Tools” e cenários Router, para manipular variáveis e direcionar o fluxo condicionalmente, assegurando que cada resposta do usuário desencadeie a próxima ação apropriada.)

## 🚀 Como Executar o Projeto

Para utilizar o copiloto de IA e gerar seu texto corporativo, siga estes passos simples:

#### Inicie a conversa no Telegram:

Abra o Telegram e procure pelo bot @textoiabot [(clique para iniciar a conversa)](https://t.me/textoiabot). Em seguida, clique em Start ou envie uma mensagem qualquer para começar. O bot deverá responder com uma mensagem de boas-vindas e instruções iniciais.

#### Forneça o tipo de texto desejado:

O bot perguntará qual tipo de texto você quer criar. Responda com o tipo específico, por exemplo: E-mail, Aviso Institucional, Resumo de Reunião etc. Escolha o que melhor se encaixa na sua necessidade atual.

#### Forneça os tópicos ou pontos-chave:

Em seguida, informe os assuntos e detalhes que o texto deve incluir. Você pode escrever uma lista de tópicos, pontos de pauta ou informações importantes que deseja ver no conteúdo. Quanto mais contexto fornecer, mais personalizado será o resultado.

#### Informe o tom de voz: 

O bot irá perguntar qual deve ser o tom do texto. Escreva o estilo desejado, como formal, informal, entusiasmado, objetivo e claro, motivador etc. Esse tom guiará a forma como a IA redige o texto (palavras e estilo adequados).

#### Escolha o canal de entrega: 

Por último, indique onde quer receber o texto gerado. Responda “Telegram” para recebê-lo diretamente no chat do bot, ou “Email” para recebê-lo por e-mail.

Se escolher Telegram, o bot confirmará e iniciará o processamento da sua solicitação imediatamente.

Se escolher Email, o bot pode pedir que você forneça um endereço de e-mail caso ainda não tenha essa informação. Digite seu endereço de e-mail completo (por exemplo, fulano@empresa.com). Certifique-se de que está correto, pois o texto será enviado para esse endereço.

#### Aguarde a geração do texto: 

Após a etapa acima, o bot irá processar suas informações. Ele irá compor o prompt para a IA e aguardar a resposta com o texto pronto. Esse processo geralmente é rápido (alguns segundos), mas pode levar meio minuto ou mais dependendo do tamanho do texto ou da carga nos servidores de IA. Fique no aguardo – o bot indicará que está gerando ou simplesmente não responderá imediatamente até ter o resultado.

#### Receba o texto corporativo: 

Assim que a IA fornecer o resultado, você o receberá pelo canal escolhido:

- Via Telegram: o bot enviará uma mensagem contendo o texto solicitado. Você pode então copiá-lo e utilizá-lo conforme necessário (por exemplo, copiar o texto e colar num e-mail ou documento oficial).

- Via Email: você receberá um e-mail (no endereço fornecido) com o texto no corpo da mensagem. Verifique sua caixa de entrada (e também a pasta de spam, caso não apareça em alguns minutos na principal). O assunto do e-mail indicará que é o texto gerado pela IA e deverá conter o tipo de texto como referência.

Refine ou finalize conforme necessário: O conteúdo gerado deve servir como um rascunho avançado. Você pode utilizá-lo diretamente ou ajustá-lo manualmente se precisar adicionar algum detalhe específico ou adequar o tom. Lembre-se de revisar o texto, garantindo que está 100% alinhado com o que você quer comunicar antes de enviar ou publicar oficialmente.

#### Comandos especiais: 

Durante a conversa, se você precisar cancelar o processo a qualquer momento (por exemplo, desistir de gerar o texto atual ou recomeçar do zero), basta digitar uma palavra-chave como cancelar ou sair. O bot então abortará a sequência de perguntas e limpará os dados já recebidos para aquela solicitação. Você receberá uma confirmação de cancelamento e poderá iniciar uma nova solicitação quando quiser. Se desejar voltar uma etapa (por exemplo, você percebeu que informou o tipo de texto errado e quer corrigi-lo), pode digitar voltar assim que o bot fizer a pergunta seguinte. O fluxo então retornará à pergunta anterior e você poderá fornecer uma nova resposta, substituindo a anterior no Data Store. Esses comandos ajudam a tornar a interação mais flexível e evitar ter que concluir todo o fluxo em caso de engano.

#### Dica: 

Você pode testar diferentes combinações de tipo/tópicos/tom para ver como a IA se adapta a cada contexto. Por exemplo, experimente gerar um aviso institucional com tom motivador, ou um resumo de reunião enfatizando tópicos técnicos com tom formal. Cada variação resultará em um texto único criado para aquela situação.

## Prompt da IA (configuração do agente)

Um dos pontos-chave do projeto é o prompt utilizado para instruir a IA generativa. O prompt foi elaborado em inglês para garantir melhor compreensão por parte da IA; porém, foi estruturado de forma a assegurar que a resposta seja gerada em português do Brasil (PT-BR) e no estilo corporativo adequado. No agente de IA do Make.com, definiu-se uma mensagem com regras claras, orientando o modelo a gerar um texto completo e pronto para uso, a partir das informações estruturadas fornecidas pelo usuário. Em pseudocódigo simplificado, o prompt segue a seguinte estrutura:

```
  You are a corporate communication assistant specialized in producing clear, assertive and professional corporate messages.

  Write the message in Brazilian Portuguese (PT-BR).
  
  Your task is to generate a complete message ready for immediate use, based exclusively on the structured information provided (type of text, topics and tone of voice).
  
  The information will be provided in a structured format and must be interpreted exactly as given, without assumptions or extrapolations.
  
  Guidelines:
  1. Use clear, objective and professional language.
  2. Structure the text with a clear beginning, development and conclusion.
  3. Adapt the structure strictly according to the type of text:
     - Email: include subject, greeting, body and proper closing.
     - Meeting summary: organize the content in short, clear bullet points.
     - WhatsApp message: keep the text concise, direct and professional.
     - Institutional or internal communication: use a neutral, inclusive and informative tone.
  4. Use ONLY the information explicitly provided in the message content.
  5. If the content refers to scheduling, inviting or confirming a meeting, generate a meeting invitation consistent with the provided information.
  6. Ignore greetings such as “bom dia”, “olá”, or similar informal openings.
  7. Apply strictly the requested tone of voice.
  8. Always finalize the message in a coherent way, using an appropriate closing, signature or call to action when applicable.
  
  Strict rules:
  - Do NOT ask questions.
  - Do NOT request additional information.
  - Do NOT say that information is missing or insufficient.
  - Do NOT invent context, objectives, recipients or subjects.
  - Do NOT generate generic, unrelated or default institutional content.
  - Do NOT include emojis, informal language or explanations.
  - Return ONLY the final text, fully written and ready to be sent.
```
No prompt acima:

Tipo de texto define o formato que a IA deve seguir. Por exemplo, se o tipo for Email, o texto deve conter obrigatoriamente assunto, saudação, corpo e encerramento. Se for Meeting summary, a resposta deve ser organizada em tópicos curtos (bullet points). Se for WhatsApp message, a escrita deve ser concisa, direta e profissional. Já em Institutional/internal communication, o tom deve ser neutro, inclusivo e informativo.

Tópicos correspondem ao conteúdo principal que deve aparecer no texto final. O prompt reforça que a IA deve usar somente o que foi informado nos tópicos, evitando inserir detalhes que não foram fornecidos.

Tom de voz é a orientação de estilo (por exemplo, formal, neutro, direto) que deve ser aplicada de forma estrita, garantindo que o texto final siga o tom solicitado pelo usuário.

Essa formulação orienta o modelo de IA a gerar exatamente o texto desejado. Primeiro, o prompt define o papel da IA como assistente corporativo e fixa o idioma em PT-BR. Depois, reforça que o texto deve ser criado com base apenas nas entradas estruturadas, sem “inventar” contexto. Em seguida, o prompt impõe regras de estrutura por tipo de texto e restrições de comportamento para evitar respostas genéricas, perguntas ao usuário ou explicações. Isso garante uma saída final pronta para ser usada imediatamente no ambiente corporativo.

Exemplo de prompt real enviado ao agente: suponha que o usuário pediu um Email, com tópicos “marcação de reunião às 09h de amanhã” e tom “formal”. As informações estruturadas enviadas ao agente seriam:

```
  Tipo de texto: Email
  Tópicos: marcação de reunião às 09h de amanhã
  Tom de voz: formal
```

A partir disso, a IA gera um e-mail completo em PT-BR com assunto, saudação, corpo e encerramento, mantendo o tom formal e utilizando apenas as informações fornecidas, pronto para envio.

### Observações e limitações

#### Qualidade do modelo (small):
Optamos por usar o modelo small do Make AI Agent por razões de custo e performance. Ele produz textos bons e coerentes para tarefas simples, porém pode ter limitações em compreensão de contexto muito complexo ou produzir respostas mais genéricas em comparação com modelos maiores (como GPT-4). Nos testes realizados, os resultados atenderam bem às necessidades básicas de textos corporativos, mas é importante revisar o conteúdo antes de uso oficial.

#### Dependência de entrada do usuário:
A qualidade e acurácia do texto gerado dependem diretamente das informações fornecidas pelo usuário. Instruções vagas ou tópicos pouco claros podem resultar em um texto igualmente genérico. É recomendado que o usuário descreva os pontos principais com algum detalhe para obter um resultado mais preciso e útil.

#### Revisão humana necessária:
Embora a IA agilize a elaboração, o texto fornecido deve ser visto como um rascunho. Sempre revise o texto gerado antes de enviá-lo ou publicá-lo oficialmente. Verifique se todos os dados estão corretos, se o tom está apropriado e se não há nenhuma incoerência. A IA pode ocasionalmente produzir alguma informação incorreta ou esquecer de incluir algo que foi pedido (especialmente se a lista de tópicos for longa).

#### Limites éticos e de segurança:
Evite inserir no prompt dados sensíveis ou confidenciais da empresa, pois essas informações estão sendo processadas por um modelo de IA externo. Embora o Make.com ofereça um ambiente seguro, os modelos de linguagem grandes podem reter informações em logs. Portanto, não use o bot para gerar textos que contenham segredos comerciais, dados pessoais protegidos (LGPD) ou informações sigilosas sem as devidas precauções. Além disso, esteja ciente de que modelos de IA podem apresentar vieses ou erros; monitore se o conteúdo gerado está adequado em termos de políticas da empresa e ética profissional.

#### Armazenamento de dados temporário: 
Os dados coletados (tipo, tópicos, tom, email) são armazenados no Data Store do Make apenas para conduzir a conversa e gerar o texto. Não mantemos um banco de dados permanente dessas informações para outros fins. Ainda assim, recomenda-se não fornecer informações que você não gostaria que ficassem registradas. O e-mail fornecido é usado unicamente para o envio automático do texto e não é compartilhado com terceiros pelo cenário.

#### Fluxo de conversa linear: 
O bot foi programado para seguir um roteiro pré-definido de perguntas e respostas. Solicitações fora desse contexto podem não ser compreendidas. Por exemplo, se no meio do processo o usuário fizer uma pergunta não relacionada (“Qual a previsão do tempo?”) ou desviar do assunto, o bot provavelmente responderá com uma mensagem padrão de erro ou não entenderá, já que o foco é gerar textos corporativos. Em caso de erro ou mal-entendido, o usuário pode cancelar e começar de novo. Futuras versões poderiam incorporar mais flexibilidade ou compreensão de linguagem natural para sair e retornar ao fluxo principal, mas nesta versão inicial o escopo é intencionalmente limitado.

#### Limitações de formato: 
O texto gerado pela IA virá em formato bruto (texto simples). Caso seja necessário algum tipo de formatação específica (por exemplo, lista de tópicos com marcadores, ou texto com negrito/itálico), o usuário deverá editar manualmente após receber o rascunho. O prompt atual não inclui instruções de formatação avançada para evitar confusão, mantendo o foco no conteúdo.

#### Disponibilidade do serviço: 
Por se tratar de uma automação dependente de serviços externos (API do Telegram, servidores do Make.com e modelo de IA), a disponibilidade pode variar. Em raros casos, pode haver lentidão ou falhas se algum desses serviços estiver enfrentando problemas. Se o bot não responder ou demorar muito, aguarde alguns instantes e tente novamente. O cenário foi projetado com certas tratativas de erro simples (por exemplo, um fallback caso a IA demore ou não responda, ou caso o e-mail não seja enviado), mas nem todos os casos são cobertos.
