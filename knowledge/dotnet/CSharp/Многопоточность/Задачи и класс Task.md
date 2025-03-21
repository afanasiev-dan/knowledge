Библиотека TPL (Task Parallel Library) основана на концепции задач, представляющих длительные операции. Задача в .NET реализована классом `Task` из пространства имен `System.Threading.Tasks`. Такая задача может выполняться асинхронно в потоке из пула или синхронно в текущем потоке, но важно понимать, что задача – это не поток.


Три способа создания и запуска задачи:

```csharp
Task task1 = new Task(() => Console.WriteLine("Task1 is executed"));
task1.Start();
 
Task task2 = Task.Factory.StartNew(() => Console.WriteLine("Task2 is executed"));
 
Task task3 = Task.Run(() => Console.WriteLine("Task3 is executed"));
```

### Ожидание завершения задачи

Чтобы приложение ожидало завершения задачи, можно использовать метод Wait() объекта Task:

```csharp
task1.Wait();
```

Стоит отметить, что метод Wait() блокирует вызывающий поток, в котором запущена задача, пока эта задача не завершит свое выполнение.