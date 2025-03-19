Позволяет перебирать элементы коллекции без непосредственного доступа к ней. Полезен, когда есть несколько реализаций итеративных классов с разными типами данных, для их унификации и создаётся итератор

### Пример реализации паттерна Итератор

#### 1. Интерфейс Итератора

```c#
public interface IIterator
{
    bool HasNext();
    object Next();
}
```

#### 2. Интерфейс Коллекции

```c#
public interface IAggregate
{
    IIterator CreateIterator();
}

```


#### 3. Конкретный Итератор

```c#
public class ConcreteIterator : IIterator
{
    private readonly ConcreteAggregate _aggregate;
    private int _currentIndex = 0;

    public ConcreteIterator(ConcreteAggregate aggregate)
    {
        _aggregate = aggregate;
    }

    public bool HasNext()
    {
        return _currentIndex < _aggregate.Count;
    }

    public object Next()
    {
        return _aggregate[_currentIndex++];
    }
}
```

#### 4. Конкретная Коллекция

```c#
public class ConcreteAggregate : IAggregate
{
    private readonly List<object> _items = new List<object>();

    public IIterator CreateIterator()
    {
        return new ConcreteIterator(this);
    }

    public int Count => _items.Count;

    public object this[int index]
    {
        get => _items[index];
        set => _items.Insert(index, value);
    }
}
```


#### 5. Использование паттерна Итератор

```c#
public class ConcreteAggregate : IAggregate
{
    private readonly List<object> _items = new List<object>();

    public IIterator CreateIterator()
    {
        return new ConcreteIterator(this);
    }

    public int Count => _items.Count;

    public object this[int index]
    {
        get => _items[index];
        set => _items.Insert(index, value);
    }
}
```
