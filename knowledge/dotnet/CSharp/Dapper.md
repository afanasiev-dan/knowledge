Dapper - это микро-ORM, который предоставляет высокую производительность и простоту использования при работе с базами данных. Dapper позволяет разработчикам выполнять SQL-запросы и маппить результаты на объекты в коде.

Основные особенности Dapper:

- Производительность: Dapper обычно работает быстрее, чем другие ORM-фреймворки, потому что он не генерирует код и не использует отражение.
- Простота: Dapper имеет очень простой и понятный API, который позволяет разработчикам быстро начать работу с базами данных.
- Поддержка асинхронных операций: Dapper поддерживает асинхронные операции, что делает его идеальным для использования в асинхронных приложениях.
- Поддержка множества баз данных: Dapper поддерживает множество баз данных, включая SQL Server, PostgreSQL, MySQL, SQLite и другие.

``` c#
using (var connection = new SqlConnection(connectionString))
{
    var customers = connection.Query<Customer>("SELECT * FROM Customers WHERE Age > @Age", new { Age = 25 });

    foreach (var customer in customers)
    {
        Console.WriteLine($"{customer.Id} - {customer.Name}");
    }
}

```

``` c#
public class Dog
{
    public int? Age { get; set; }
    public Guid Id { get; set; }
    public string Name { get; set; }
    public float? Weight { get; set; }

    public int IgnoredProperty { get { return 1; } }
}

var guid = Guid.NewGuid();
var dog = connection.Query<Dog>("select Age = @Age, Id = @Id", new { Age = (int?)null, Id = guid });

Assert.Equal(1,dog.Count());
Assert.Null(dog.First().Age);
Assert.Equal(guid, dog.First().Id);
```