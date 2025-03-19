- **Mutex**: Используется для синхронизации доступа к ресурсам между потоками и процессами.
- **Semaphore**: Используется для ограничения количества потоков, которые могут одновременно доступаться к ресурсу.
- **SemaphoreSlim**: Легковесная версия `Semaphore`, предназначенная для использования внутри одного процесса.

``` csharp
int x = 0;
Mutex mutexObj = new();

// запускаем пять потоков
for (int i = 1; i < 6; i++)
{
    Thread myThread = new(Print);
    myThread.Name = $"Поток {i}";
    myThread.Start();
}

void Print()
{
    mutexObj.WaitOne();     // приостанавливаем поток до получения мьютекса
    x = 1;
    for (int i = 1; i < 6; i++)
    {
        Console.WriteLine($"{Thread.CurrentThread.Name}: {x}");
        x++;
        Thread.Sleep(100);
    }
    mutexObj.ReleaseMutex();    // освобождаем мьютекс
}
```