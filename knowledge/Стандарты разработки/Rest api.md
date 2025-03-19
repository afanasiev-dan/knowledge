(Representational State Transfer)
Это стиль архитектуры для разработки сетевых приложений. REST определяет набор ограничений и описывает, как ресурсы могут быть представлены, и как с ними можно взаимодействовать посредством стандартных протоколов, таких как HTTP. Веб-сервисы, следующие принципам REST, называют RESTful API.)

**Ресурсы и URI (Uniform Resource Identifier):**

- REST ориентирован на ресурсы, которые могут быть представлены и идентифицированы с помощью URI.

``` c#
// Пример URI для ресурса "пользователь"
/api/users
```


**HTTP Методы:**

- Операции над ресурсами представлены стандартными HTTP методами (GET, POST, PUT, DELETE).
```c#
// HTTP GET запрос для получения списка пользователей
[HttpGet("/api/users")]
public IActionResult GetUsers()
{
    // Логика получения пользователей
}

// HTTP POST запрос для создания нового пользователя
[HttpPost("/api/users")]
public IActionResult CreateUser([FromBody] User newUser)
{
    // Логика создания пользователя
}

// HTTP PUT запрос для обновления информации о пользователе
[HttpPut("/api/users/{id}")]
public IActionResult UpdateUser(int id, [FromBody] User updatedUser)
{
    // Логика обновления пользователя
}

// HTTP DELETE запрос для удаления пользователя
[HttpDelete("/api/users/{id}")]
public IActionResult DeleteUser(int id)
{
    // Логика удаления пользователя
}

```

**Представление данных (Content Negotiation):**

Клиент и сервер могут использовать разные форматы представления данных, такие как JSON или XML.

```c#
// Указание формата данных в HTTP заголовке
Accept: application/json
Content-Type: application/json

```

**Состояние и состояние ресурса:**
Каждый ресурс в REST API должен содержать всю информацию, необходимую для его понимания и изменения.

```c#
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    // Другие свойства пользователя
}
```


**Безсостояничность (Statelessness):**
Каждый запрос от клиента к серверу должен содержать всю необходимую информацию.

```c#
// Безсостояничный метод для получения пользователя по идентификатору
[HttpGet("/api/users/{id}")]
public IActionResult GetUserById(int id)
{
    // Логика получения пользователя по id
}
```

**Гипермедиа как средство передачи состояния (HATEOAS):**
Клиент получает гиперссылки в ответе от сервера, что позволяет ему навигироваться по API.

```c#
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    public List<Link> Links { get; set; }
}

public class Link
{
    public string Rel { get; set; }
    public string Href { get; set; }
}
```