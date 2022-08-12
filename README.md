# Mensageria: o que é?
É um conceito de comunicação entre sistemas distribuidos com troca de mensagens.

![Como funciona](/images/1_Gdwao93tU0lhQ1WnXIdG7Q.png)

## Eventos
São gatilhos que ocorrem no sistema e que é enviado como uma notificação para outras partes da solução. Esses eventos são enviados como mensagens, normalmente utilizando um protocolo chamado AMQP.

## Message Broker
É um servidor intermediário que gerencia o enfileiramento, armazenagem e disparo dos eventos (mensagens). Normalmente, recebe as mensagens pelo **Producer**. Pode transformar a mensagem no padrão formal do protocolo para o padrão que o consumer entende.

Alguns desses casos incluem:

**GCP: Pub/Sub**

**AWS: SNS**

**RabbitMQ**

**Kafka**

## Producer
Pode ser uma aplicação ou um script gera a mensagem e envia para o Message Broker ou diretamente para a fila (queue).

## Tópico
É quem encaminha a mensagem publicada para todos os assinantes consumidores. Ele consegue rotear a mensagem para todos os interessados. Está embutido no trabalho do message broker.

## Consumer
Responsável por solicitar da fila uma mensagem e decidir o que fazer com ela. O consumer pode retornar a mensagem para a fila caso decida.


# Em que caso usar?
Nossa API de  centro de distribuição, quando recebe um novo registro, precisa notificar o Senninha e MaaS para criar um provider e o dmitri para cadastrar a cidade. Caso um desses sistemas esteja fora dor ar, teremos que ficar sabendo que a falha na comunição falhou e teremos que reencarminhar novamente essa request manualmente, já que o processo de cadastro e todas as etapas que o compõem seguem uma sequencia sincrona.

Utilizando mensagens, podemos, após o cadastro de um novo centro de distribuição, enviar para um broker uma notificação de que um novo centro de distribuição foi criado e ele pode disparar isso para 1 ou N filas (subscribers) de aplicações que se interessam pela informação. Esse processamento muda para assincrono e podemos tentar inúmeras vezes uma comunição com um dos sistemas externos até que ele volte a funcionar e retorne sucesso.

# Referencias
https://www.ibm.com/br-pt/cloud/learn/message-brokers

https://en.wikipedia.org/wiki/Message_broker

https://www.blogdoft.com.br/2021/02/06/o-que-sao-mensageria-eventos-filas-e-topicos/

https://medium.com/@devbrito91/mensageria-1330c6032049