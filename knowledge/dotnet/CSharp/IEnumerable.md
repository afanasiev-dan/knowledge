`IEnumerable<T>` представляет собой коллекцию объектов, которые можно перечислить с помощью цикла `foreach`. Он поддерживает операции фильтрации, проекции и сортировки, но выполняет их немедленно, то есть при каждом выполнении запроса данные извлекаются из источника данных и обрабатываются. 

Пример:
```c#
IEnumerable<int> numbers = Enumerable.Range(1, 10);
IEnumerable<int> evenNumbers = numbers.Where(n => n % 2 == 0);

foreach (int number in evenNumbers)
    Console.WriteLine(number);
```