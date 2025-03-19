**Redis** – это очень быстрое хранилище данных основанное на принципе, что кэш также может быть надежным хранилищем.

Быстродействие Redis основано на том, что работа с данными всегда происходит в оперативной памяти, а не через медленный жесткий диск. В то же время данные сохраняются на диск, чтобы их можно было восстановить по мере необходимости, так что Redis надежен и поддерживает снепшоты и резервные копии.

Каждая запись в редисе представляет собой `ключ` и соответсвующее ему `значение`. В качестве значений могут выступать различные типы данных, такие как строки, списки, словари.  
Поэтому вы можете хранить данные естественным образом, как вы бы это сделали на своем любимом языке программирования, в отличие от того, чтобы пытаться их уместить их в множество таблиц или `JSON`-документах.

Взаимодействие с базой данных происходит с помощью простого набора команд, таких как `SET` для создания данных, или `GET` для их получения.

Исторически Redis широко применяется как кэш для основной базы данных, но он также отлично подходит и в качестве основного хранилища, в которой необходимость кэширования отпадает.

На сегодняшний день Redis больше чем обычное key-value хранилище.  
Для данных с отношениями есть **Redis Graph** и язык запросов **Cipher**, чтобы воспользоваться преимуществами документо-ориентированных баз используйте **Redis JSON**, для временных рядов есть **Redis TimeSeries**, а **Redis Search** превратит вашу базу данных в полнотекстовый поисковый движок.

https://www.youtube.com/watch?v=nma6sLjjKQs

Библиотека
Install-Package StackExchange.Redis

``` c#
public class UserService
{
    private readonly ApplicationContext _db;
    private readonly IDistributedCache _cache;

    public UserService(ApplicationContext context, IDistributedCache distributedCache)
    {
        _db = context;
        _cache = distributedCache;
    }

    public async Task<User?> GetUser(int id)
    {
        var userString = await _cache.GetStringAsync(id.ToString());
        var user = userString != null ? JsonSerializer.Deserialize<User>(userString) : null;

        if (user == null)
        {
            user = await _db.Users.FindAsync(id);

            if (user != null)
            {
                Console.WriteLine($"{user.Name} извлечен из базы данных");
                userString = JsonSerializer.Serialize(user);
                await _cache.SetStringAsync(user.Id.ToString(), userString, new DistributedCacheEntryOptions
                {
                    AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(2)
                });
            }
        }
        else
        {
            Console.WriteLine($"{user.Name} извлечен из кэша");
        }

        return user;
    }
}

```