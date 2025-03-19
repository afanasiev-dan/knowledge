В контексте веб-разработки, Action filters - это механизм в ASP.NET MVC, который позволяет разработчикам добавлять поведение к действиям контроллера. Они могут быть использованы для обработки аутентификации, авторизации, кэширования, маршрутизации и других задач. 

Пример кода, демонстрирующего использование Action фильтров в ASP.NET MVC:

```csharp
public class MyController : Controller
{
    [Authorize]
    public ActionResult MyAction()
    {
        // код действия
    }
}

```

В этом примере мы используем атрибут [Authorize] перед методом MyAction. Этот атрибут является Action фильтром, который проверяет, авторизован ли пользователь перед выполнением действия. Если пользователь не авторизован, он будет перенаправлен на страницу входа.

| Тип фильтра        | Синхронный интерфейс | Асинхронный интерфейс     |
| ------------------ | -------------------- | ------------------------- |
|                    |                      |                           |
| Фильтр авторизации | IAuthorizationFilter | IAsyncAuthorizationFilter |
| Фильтр ресурсов    | IResourceFilter      | IAsyncResourceFilter      |
| Фильтр действий    | IActionFilter        | IAsyncActionFilter        |
| Фильтр исключений  | IExceptionFilter     | IAsyncExceptionFilter     |
| Фильтр результатов | IResultFilter        | IAsyncResultFilter        |
