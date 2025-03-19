Этот паттерн используется для обеспечения надежной передачи сообщений между микросервисами. Вместо того чтобы сразу отправлять сообщение в очередь, микросервис сохраняет его в локальной базе данных (outbox). После успешного выполнения транзакции сообщение отправляется в очередь. Если транзакция откатывается, сообщение не отправляется.
- Outbox Pattern обеспечивает атомарность операций и гарантирует, что сообщения будут отправлены только после успешного выполнения транзакции.

Пример использования Outbox Pattern:
```c#
public class OrderService
{
    private readonly IOrderRepository _orderRepository;
    private readonly IMessageQueue _messageQueue;

    public OrderService(IOrderRepository orderRepository, IMessageQueue messageQueue)
    {
        _orderRepository = orderRepository;
        _messageQueue = messageQueue;
    }

    public void PlaceOrder(Order order)
    {
        using (var transaction = _orderRepository.BeginTransaction())
        {
            try
            {
                _orderRepository.SaveOrder(order);
                _orderRepository.SaveOutboxMessage(new OutboxMessage { OrderId = order.Id, Status = "OrderPlaced" });
                transaction.Commit();

                // Отправка сообщения в очередь после успешного выполнения транзакции
                var outboxMessage = _orderRepository.GetOutboxMessage(order.Id);
                _messageQueue.Send(outboxMessage);
            }
            catch
            {
                transaction.Rollback();
                throw;
            }
        }
    }
}

```
