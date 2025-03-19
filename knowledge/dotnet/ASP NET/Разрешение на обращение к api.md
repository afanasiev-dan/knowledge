В api нужно добавлять разрешение на обращение к этому api
https://stacktuts.com/how-to-resolve-typeerror-failed-to-fetch-error-on-blazor-in-asp-net-core

```csharp
services.AddCors(options =>
{
    options.AddPolicy("AllowAll", builder =>
    {
        builder.AllowAnyOrigin()
               .AllowAnyMethod()
               .AllowAnyHeader();
    });
});
```

```csharp
app.UseCors("AllowAll");
```