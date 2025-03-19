ACID — это акроним, который описывает четыре основных свойства транзакций в реляционных базах данных. Эти свойства гарантируют надежность и целостность данных при выполнении транзакций. ACID расшифровывается следующим образом:

1. **Atomicity (Атомарность)**: Транзакция должна быть выполнена полностью или не выполнена вовсе. Если какая-либо часть транзакции не может быть выполнена, вся транзакция должна быть отменена, и база данных должна вернуться в состояние, которое было до начала транзакции.
    
2. **Consistency (Согласованность)**: Транзакция должна переводить базу данных из одного согласованного состояния в другое. Это означает, что все правила и ограничения базы данных должны быть соблюдены до и после выполнения транзакции.
    
3. **Isolation (Изоляция)**: Транзакции должны быть изолированы друг от друга. Это означает, что одновременно выполняющиеся транзакции не должны влиять друг на друга. Изоляция гарантирует, что промежуточные состояния транзакции не видны другим транзакциям.
    
4. **Durability (Долговечность)**: После завершения транзакции все изменения, внесенные этой транзакцией, должны быть сохранены в базе данных и оставаться там даже в случае сбоя системы.
    

### Примеры ACID в действии

#### 1. Атомарность

Предположим, у нас есть банковская система, и мы хотим перевести деньги с одного счета на другой.

```csharp
using (var transaction = connection.BeginTransaction())
{
    try
    {
        // Снимаем деньги с одного счета
        var updateAccount1 = "UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1";
        var command1 = new SqlCommand(updateAccount1, connection, transaction);
        command1.ExecuteNonQuery();

        // Добавляем деньги на другой счет
        var updateAccount2 = "UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2";
        var command2 = new SqlCommand(updateAccount2, connection, transaction);
        command2.ExecuteNonQuery();

        // Фиксируем транзакцию
        transaction.Commit();
    }
    catch (Exception)
    {
        // Откатываем транзакцию в случае ошибки
        transaction.Rollback();
    }
}

```

Если любая из операций не удается, транзакция будет откатана, и база данных вернется в исходное состояние.

#### 2. Согласованность

Предположим, у нас есть ограничение на баланс счета, который не может быть отрицательным.


```csharp
CREATE TABLE Accounts (
    AccountID INT PRIMARY KEY,
    Balance DECIMAL(10, 2) CHECK (Balance >= 0)
);
```


Если мы попытаемся выполнить транзакцию, которая нарушает это ограничение, транзакция будет отменена.


```csharp
using (var transaction = connection.BeginTransaction())
{
    try
    {
        // Снимаем деньги с одного счета
        var updateAccount1 = "UPDATE Accounts SET Balance = Balance - 200 WHERE AccountID = 1";
        var command1 = new SqlCommand(updateAccount1, connection, transaction);
        command1.ExecuteNonQuery();

        // Добавляем деньги на другой счет
        var updateAccount2 = "UPDATE Accounts SET Balance = Balance + 200 WHERE AccountID = 2";
        var command2 = new SqlCommand(updateAccount2, connection, transaction);
        command2.ExecuteNonQuery();

        // Фиксируем транзакцию
        transaction.Commit();
    }
    catch (Exception)
    {
        // Откатываем транзакцию в случае ошибки
        transaction.Rollback();
    }
}
```


Если баланс счета становится отрицательным, транзакция будет отменена.

#### 3. Изоляция

Предположим, у нас есть две транзакции, которые изменяют один и тот же счет.


```csharp
using (var transaction1 = connection.BeginTransaction())
{
    try
    {
        // Снимаем деньги с одного счета
        var updateAccount1 = "UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1";
        var command1 = new SqlCommand(updateAccount1, connection, transaction1);
        command1.ExecuteNonQuery();

        // Фиксируем транзакцию
        transaction1.Commit();
    }
    catch (Exception)
    {
        // Откатываем транзакцию в случае ошибки
        transaction1.Rollback();
    }
}

using (var transaction2 = connection.BeginTransaction())
{
    try
    {
        // Снимаем деньги с того же счета
        var updateAccount2 = "UPDATE Accounts SET Balance = Balance - 50 WHERE AccountID = 1";
        var command2 = new SqlCommand(updateAccount2, connection, transaction2);
        command2.ExecuteNonQuery();

        // Фиксируем транзакцию
        transaction2.Commit();
    }
    catch (Exception)
    {
        // Откатываем транзакцию в случае ошибки
        transaction2.Rollback();
    }
}
```


Изоляция гарантирует, что промежуточные состояния транзакций не видны друг другу.

#### 4. Долговечность

Предположим, у нас есть транзакция, которая изменяет баланс счета.

```csharp
using (var transaction = connection.BeginTransaction())
{
    try
    {
        // Снимаем деньги с одного счета
        var updateAccount1 = "UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1";
        var command1 = new SqlCommand(updateAccount1, connection, transaction);
        command1.ExecuteNonQuery();

        // Добавляем деньги на другой счет
        var updateAccount2 = "UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2";
        var command2 = new SqlCommand(updateAccount2, connection, transaction);
        command2.ExecuteNonQuery();

        // Фиксируем транзакцию
        transaction.Commit();
    }
    catch (Exception)
    {
        // Откатываем транзакцию в случае ошибки
        transaction.Rollback();
    }
}
```

После завершения транзакции все изменения будут сохранены в базе данных и останутся там даже в случае сбоя системы.

Эти принципы ACID обеспечивают надежность и целостность данных в реляционных базах данных, что является критически важным для многих приложений, особенно в финансовой и других отраслях, где точность и надежность данных имеют первостепенное значение.