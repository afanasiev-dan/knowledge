##### Коротко 
R это традиционный брокер сообщений, поддерживающий различные модели обмена сообщениями, такие как очереди, топики и маршрутизация на основе 
ключей.

##### Подробно 
Это средство обмена сообщениями с открытым исходным кодом, которое реализует протокол Advanced Message Queuing Protocol (AMQP). Он поддерживает несколько шаблонов обмена сообщениями, таких как точка-точка, публикация/подписка и запрос/ответ. RabbitMQ известен своей надежностью и стойкостью. Он часто используется для создания надежных и масштабируемых систем, которые должны обрабатывать большой объем данных.


**Основные особенности:**
1. **Модель очередей:** Сообщения в RabbitMQ передаются через очереди, что позволяет реализовывать различные сценарии маршрутизации и обработки сообщений.
2. **Поддержка различных протоколов:** RabbitMQ поддерживает AMQP, MQTT, STOMP и другие протоколы.
3. **Персистентность сообщений:** Сообщения могут сохраняться на диск, но основной акцент делается на доставке сообщений, а не на долговременном хранении.
4. **Поддержка подтверждений:** Подписчики могут подтверждать получение сообщений, что позволяет реализовать надёжную доставку.

```c#
using RabbitMQ.Client;
using System.Text;

var factory = new ConnectionFactory() { HostName = "localhost" };
using (var connection = factory.CreateConnection())
using (var channel = connection.CreateModel())
{
    channel.QueueDeclare(queue: "hello", durable: false, exclusive: false, autoDelete: false, arguments: null);

    string message = "Hello RabbitMQ";
    var body = Encoding.UTF8.GetBytes(message);

    channel.BasicPublish(exchange: "", routingKey: "hello", basicProperties: null, body: body);
    Console.WriteLine(" [x] Sent {0}", message);
}

```