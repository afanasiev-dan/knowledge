- S: Single Responsibility Principle (Принцип единственной ответственности).
- O: Open-Closed Principle (Принцип открытости-закрытости).
- L: Liskov Substitution Principle (Принцип подстановки Барбары Лисков).
- I: Interface Segregation Principle (Принцип разделения интерфейса).
- D: Dependency Inversion Principle (Принцип инверсии зависимостей).

###  Коротко
SOLID — это акроним, обозначающий пять основных принципов объектно-ориентированного программирования и проектирования. Эти принципы помогают создавать более гибкие, поддерживаемые и расширяемые системы. Вот краткое объяснение каждого принципа с примерами на C#.

### S — Single Responsibility Principle (Принцип единственной ответственности)

Класс должен иметь только одну причину для изменения, то есть он должен выполнять только одну задачу.

#### Пример

``` csharp
public class Order
{
    public void AddItem(string item){}

    public void RemoveItem(string item){}

    public void PrintOrder(){}
}

```

### O — Open/Closed Principle (Принцип открытости/закрытости)

Классы должны быть открыты для расширения, но закрыты для модификации.
#### Пример

``` csharp
public class Rectangle
{
    public double Width { get; set; }
    public double Height { get; set; }
}

public class Rectangle : Shape
{ 
	public double Width { get; set; } 
	public double Height { get; set; } 
	public override double Area => Width * Height; 
}

public class AreaCalculator
{
    public double CalculateArea(Rectangle rectangle)
    => rectangle.Width * rectangle.Height;
}
```

### L — Liskov Substitution Principle (Принцип подстановки Барбары Лисков)

Объекты в программе должны быть заменяемы экземплярами их подтипов без изменения правильности выполнения программы.

#### Пример

``` csharp
public class Bird
{
    public virtual void Fly()
	    => Console.WriteLine("Flying");
}

public class Sparrow : Bird
{
    public override void Fly()
        => Console.WriteLine("Sparrow flying");
}

public Programm{
	static void main(){
		Bird bird = new Sparrow();
		bird.Fly();
	}
}

```

### I — Interface Segregation Principle (Принцип разделения интерфейса)

Много специализированных интерфейсов лучше, чем один универсальный.

#### Пример

``` csharp
public interface IWorkable
{
    void Work();
}

public interface IEatable
{
    void Eat();
}

public class Worker : IWorkable, IEatable
{
    public void Work()
		=> Console.WriteLine("Working");

    public void Eat()
	    => Console.WriteLine("Eating");
}

public class Robot : IWorkable
{
    public void Work()
        => Console.WriteLine("Working");
}
```

### D — Dependency Inversion Principle (Принцип инверсии зависимостей)

Модули верхних уровней не должны зависеть от модулей нижних уровней. Оба типа модулей должны зависеть от абстракций. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

#### Пример
``` csharp
public interface IMessageService
{
    void SendMessage(string message);
}

public class EmailService : IMessageService
{
    public void SendMessage(string message)
	    => Console.WriteLine("Sending email: " + message);
}

public class NotificationService
{
    private readonly IMessageService _messageService;

    public NotificationService(IMessageService messageService)
	    => _messageService = messageService;

    public void SendNotification(string message)
	    => _messageService.SendMessage(message);
}
```

### Подробно
##### Принцип единственной ответственности
(Single Responsibility Principle) [link](https://metanit.com/sharp/patterns/5.2.php)
Класс должен быть ответственен лишь за что-то одно. Если класс отвечает за решение нескольких задач, его подсистемы, реализующие решение этих задач, оказываются связанными друг с другом. Изменения в одной такой подсистеме ведут к изменениям в другой.

Каждый компонент должен иметь одну и только одну причину для изменения.

Плохо
``` c#
class Report

{

    `public` `string` `Text {` `get``;` `set``; } =` `""``;`

    `public` `void` `GoToFirstPage() =>`

        `Console.WriteLine(``"Переход к первой странице"``);`

    `public` `void` `GoToLastPage() =>`

        `Console.WriteLine(``"Переход к последней странице"``);`

    `public` `void` `GoToPage(``int` `pageNumber) =>`

        `Console.WriteLine($``"Переход к странице {pageNumber}"``);`

    `public` `void` `Print()`

    `{`

        `Console.WriteLine(``"Печать отчета"``);`

        `Console.WriteLine(Text);`

    `}`

`}`
```

Хорошо
```c#
`class` `Report`

`{`

    `public` `string` `Text {` `get``;` `set``; } =` `""``;`

    `public` `void` `GoToFirstPage() =>`

        `Console.WriteLine(``"Переход к первой странице"``);`

    `public` `void` `GoToLastPage() =>`

        `Console.WriteLine(``"Переход к последней странице"``);`

    `public` `void` `GoToPage(``int` `pageNumber) =>`

        `Console.WriteLine($``"Переход к странице {pageNumber}"``);`   

`}`

`//  обязанность - печать отчета`

`class` `Printer`

`{`

    `public` `void` `PrintReport(Report report)`

    `{`

        `Console.WriteLine(``"Печать отчета"``);`

        `Console.WriteLine(report.Text);`

    `}`

`}`
```
##### Принцип открытости/закрытости
(Open-Closed Principle) [link](https://metanit.com/sharp/patterns/5.2.php)

Сущности программы должны быть открыты для расширения, но закрыты для изменения. Суть этого принципа состоит в том, что система должна быть построена таким образом, что все ее последующие изменения должны быть реализованы с помощью добавления нового кода, а не изменения уже существующего.

Плохо
```c#
`class` `Cook`

`{`

    `public` `string` `Name {` `get``;` `set``; }`

    `public` `Cook(``string` `name)`

    `{`

        `this``.Name = name;`

    `}`

    `public` `void` `MakeDinner()`

    `{`

        `Console.WriteLine(``"Чистим картошку"``);`

        `Console.WriteLine(``"Ставим почищенную картошку на огонь"``);`

        `Console.WriteLine(``"Сливаем остатки воды, разминаем варенный картофель в пюре"``);`

        `Console.WriteLine(``"Посыпаем пюре специями и зеленью"``);`

        `Console.WriteLine(``"Картофельное пюре готово"``);`

    `}`

`}`
```


Хорошо (Паттерн стратегия)
```c#
`class` `Cook`

`{`

    `public` `string` `Name {` `get``;` `set``; }`

    `public` `Cook(``string` `name)`

    `{`

        `this``.Name = name;`

    `}`

    `public` `void` `MakeDinner(IMeal meal)`

    `{`

        `meal.Make();`

    `}`

`}`

`interface` `IMeal`

`{`

    `void` `Make();`

`}`

`class` `PotatoMeal : IMeal`

`{`

    `public` `void` `Make()`

    `{`

        `Console.WriteLine(``"Чистим картошку"``);`

        `Console.WriteLine(``"Ставим почищенную картошку на огонь"``);`

        `Console.WriteLine(``"Сливаем остатки воды, разминаем варенный картофель в пюре"``);`

        `Console.WriteLine(``"Посыпаем пюре специями и зеленью"``);`

        `Console.WriteLine(``"Картофельное пюре готово"``);`

    `}`

`}`

`class` `SaladMeal : IMeal`

`{`

    `public` `void` `Make()`

    `{`

        `Console.WriteLine(``"Нарезаем помидоры и огурцы"``);`

        `Console.WriteLine(``"Посыпаем зеленью, солью и специями"``);`

        `Console.WriteLine(``"Поливаем подсолнечным маслом"``);`

        `Console.WriteLine(``"Салат готов"``);`

    `}`

`}`
```


Хорошо (паттерн "Шаблонный метод")
``` c#
`abstract` `class` `MealBase`

`{`

    `public` `void` `Make()`

    `{`

        `Prepare();`

        `Cook();`

        `FinalSteps();`

    `}`

    `protected` `abstract` `void` `Prepare();`

    `protected` `abstract` `void` `Cook();`

    `protected` `abstract` `void` `FinalSteps();`

`}`

`class` `PotatoMeal : MealBase`

`{`

    `protected` `override` `void` `Cook()`

    `{`

        `Console.WriteLine(``"Ставим почищенную картошку на огонь"``);`

        `Console.WriteLine(``"Варим около 30 минут"``);`

        `Console.WriteLine(``"Сливаем остатки воды, разминаем варенный картофель в пюре"``);`

    `}`

    `protected` `override` `void` `FinalSteps()`

    `{`

        `Console.WriteLine(``"Посыпаем пюре специями и зеленью"``);`

        `Console.WriteLine(``"Картофельное пюре готово"``);`

    `}`

    `protected` `override` `void` `Prepare()`

    `{`

        `Console.WriteLine(``"Чистим и моем картошку"``);`

    `}`

`}`

`class` `SaladMeal : MealBase`

`{`

    `protected` `override` `void` `Cook()`

    `{`

        `Console.WriteLine(``"Нарезаем помидоры и огурцы"``);`

        `Console.WriteLine(``"Посыпаем зеленью, солью и специями"``);`

    `}`

    `protected` `override` `void` `FinalSteps()`

    `{`

        `Console.WriteLine(``"Поливаем подсолнечным маслом"``);`

        `Console.WriteLine(``"Салат готов"``);`

    `}`

    `protected` `override` `void` `Prepare()`

    `{`

        `Console.WriteLine(``"Моем помидоры и огурцы"``);`

    `}`

`}`
```
##### Принцип подстановки Барбары Лисков
(Liskov Substitution Principle) [link](https://metanit.com/sharp/patterns/5.3.php)

Этот принцип гласит, что объекты старших классов должны быть заменимы объектами подклассов, и приложение при такой замене должно работать так, как ожидается.

``` c#
// Нарушение LSP
public class Bird
{
    public virtual void Fly() { /*...*/ }
}

public class Ostrich : Bird
{
    public override void Fly()
    {
        // Не должны летать, но метод предоставлен в базовом классе.
        throw new InvalidOperationException("Ostriches cannot fly.");
    }
}

// Соблюдение LSP
public interface IFlyable
{
    void Fly();
}

public class Sparrow : IFlyable
{
    public void Fly() { /*...*/ }
}

public class Ostrich : Bird // Наследуется от Bird, но не реализует IFlyable
{
    // Метод Fly не переопределяется, так как страусы не летают.
}

```

##### Принцип единственной ответственности
(Interface Segregation Principle - ISP) [link](https://metanit.com/sharp/patterns/5.4.php)
Клиенты не должны зависеть от интерфейсов, которые они не используют. Классы не должны быть вынуждены реализовывать интерфейсы, которые они не используют.

```c#
// Нарушение ISP
public interface IWorker
{
    void Work();
    void TakeBreak();
}

public class Manager : IWorker
{
    public void Work() { /*...*/ }
    public void TakeBreak() { /*...*/ }
}

public class Programmer : IWorker
{
    public void Work() { /*...*/ }
    public void TakeBreak() { /*...*/ }
}

// Соблюдение ISP
public interface IWorkable
{
    void Work();
}

public interface IBreakable
{
    void TakeBreak();
}

public class Manager : IWorkable, IBreakable
{
    public void Work() { /*...*/ }
    public void TakeBreak() { /*...*/ }
}

public class Programmer : IWorkable
{
    public void Work() { /*...*/ }
}

```
##### Принцип единственной ответственности
(Dependency Inversion Principle - DIP) [link](https://metanit.com/sharp/patterns/5.5.php)
Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба типа модулей должны зависеть от абстракций. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

```c#
// Нарушение DIP
public class LightBulb
{
    public void TurnOn() { /*...*/ }
    public void TurnOff() { /*...*/ }
}

public class Switch
{
    private readonly LightBulb _bulb;

    public Switch()
    {
        _bulb = new LightBulb();
    }

    public void Toggle()
    {
        // Зависимость от конкретной реализации LightBulb
        if (_bulb.IsOn())
            _bulb.TurnOff();
        else
            _bulb.TurnOn();
    }
}

// Соблюдение DIP
public interface ISwitchable
{
    void TurnOn();
    void TurnOff();
}

public class LightBulb : ISwitchable
{
    public void TurnOn() { /*...*/ }
    public void TurnOff() { /*...*/ }
}

public class Switch
{
    private readonly ISwitchable _device;

    public Switch(ISwitchable device)
    {
        _device = device;
    }

    public void Toggle()
    {
        // Инверсия зависимости - теперь Switch зависит от абстракции (интерфейса)
        if (_device.IsOn())
            _device.TurnOff();
        else
            _device.TurnOn();
    }
}

```