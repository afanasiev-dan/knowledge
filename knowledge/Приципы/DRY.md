(Don't Repeat Yourself)
Это принцип разработки программного обеспечения, который подразумевает, что каждая часть знаний или логики в системе должна иметь единственное, неизменное представление в системе. Следование принципу DRY помогает избежать избыточности кода, упрощает поддержку и снижает вероятность ошибок.

### Избегание дублирования кода в методах
```c#
// Нарушение принципа DRY
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int Subtract(int a, int b)
    {
        return a - b;
    }

    public int Multiply(int a, int b)
    {
        return a * b;
    }

    public int Divide(int a, int b)
    {
        return a / b;
    }
}

// Соблюдение принципа DRY
public class Calculator
{
    private int PerformOperation(int a, int b, Func<int, int, int> operation)
    {
        return operation(a, b);
    }

    public int Add(int a, int b)
    {
        return PerformOperation(a, b, (x, y) => x + y);
    }

    public int Subtract(int a, int b)
    {
        return PerformOperation(a, b, (x, y) => x - y);
    }

    public int Multiply(int a, int b)
    {
        return PerformOperation(a, b, (x, y) => x * y);
    }

    public int Divide(int a, int b)
    {
        return PerformOperation(a, b, (x, y) => x / y);
    }
}

```

### Использование циклов для обработки коллекций
```c#
// Нарушение принципа DRY
public class Printer
{
    public void PrintNumbers(int[] numbers)
    {
        foreach (var number in numbers)
        {
            Console.WriteLine(number);
        }
    }

    public void PrintStrings(string[] strings)
    {
        foreach (var str in strings)
        {
            Console.WriteLine(str);
        }
    }
}

// Соблюдение принципа DRY
public class Printer
{
    private void PrintItems<T>(T[] items)
    {
        foreach (var item in items)
        {
            Console.WriteLine(item);
        }
    }

    public void PrintNumbers(int[] numbers)
    {
        PrintItems(numbers);
    }

    public void PrintStrings(string[] strings)
    {
        PrintItems(strings);
    }
}

```
### Использование базовых классов или интерфейсов
```c#
// Нарушение принципа DRY
public class Circle
{
    public double Radius { get; set; }

    public double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Square
{
    public double Side { get; set; }

    public double CalculateArea()
    {
        return Side * Side;
    }
}

// Соблюдение принципа DRY
public interface IShape
{
    double CalculateArea();
}

public class Circle : IShape
{
    public double Radius { get; set; }

    public double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Square : IShape
{
    public double Side { get; set; }

    public double CalculateArea()
    {
        return Side * Side;
    }
}

```