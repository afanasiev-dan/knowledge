00:20:26
Видел ли ты во что превращается код CLR


00:20:30
Что такое CLR
  

00:33:58
Что такое память и как мы с ней работаем.
Управляемая и не управляемая память.
Как мы работаем в потоках с памятью.


00:36:06
Режимы работы GC. Station, server.


00:38:03
Как получается, что у нас объекты лежать в разнsх поколениях, для чего нужны эти поколения?


00:39:21
Что такое дефрагментация память в GC.


00:39:21
У нас ест два приложения, одно на c#, второе на c++, и тебе нужно не через память и не через api какую-то провзаимодействовать с одним и тем же объектом в памяти. И есть такое понятие как маршален. Что это и как с ним работать? Где это работает?

Ответ
Только под виндой работает.


00:39:21
Что такое бд, что такое acid


00:47:44
Как сама postgres обеспечивает атомарность транзакций?

Представь ситуацию, у нас была какая-то большая транзакция, и мы в рамках этой транзакции что-то писали, и в этот момент у нас отключилось питание. Когда питание включится назад, postgres свою задачу до конца доведёт? Или обнулится и скажет что она ничего не знает?


00:39:21
Влияет ли как-то механизм мультиверсионности на изоляцию транзакций в postgres?
Как изоляция транзакций обеспечивается в postgreSQL.
К примеру, у меня есть несколько транзакций, которые хотят поработать с одним и тем же набором данных  и есть такой механизм, называется mvcc для многоверсионности. Каждая транзакция имеет свою версию данных. Это позволяет несколким транзакциям работать с одним и той же таблице без блокировок, на чтение например.
  

00:52:28
Что ты знаешь про индексы в postgres?


00:53:56
У нас есть таблица, колонка, мы на колонку вешаем индекс. В каких ситуациях индекс не даст прирост или вообще замедлит работу.

Когда у нас есть большой объём данных и мы в результате запроса выбираем большой кусок, то просто игнорируются индексы и начинает обходить всё?

Есть встроенные операции, такие как ToLower, которые игнорируют индексы?


00:55:44
Что такое покрывающий индекс? Covering index


00:57:07
Что такое IQuerable, что такое отложенное выполнение? Как с этим работать? И для чего это нужно?