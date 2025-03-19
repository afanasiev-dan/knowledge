Для отправки json можно воспользоваться методом WriteAsJson()/WriteAsJsonAsync() объекта HttpResponse. Этот метод позволяет сериализовать переданные в него объекты в формат JSON и автоматически для заголовка "content-type" устанавливает значение "application/json; charset=utf-8":

``` c#
var builder = WebApplication.CreateBuilder();
var app = builder.Build();

app.Run(async (context) =>
{
    Person tom = new("Tom", 22);
    await context.Response.WriteAsJsonAsync(tom);
});

app.Run();

public record Person(string Name, int Age);
```