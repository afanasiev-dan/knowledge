Для указания базового образа используется инструкция `FROM`.  
Для указания рабочей директории используется инструкция `WORKDIR`.  
Для копирования файлов инструкция `COPY`.  
**RUN** позволяет выполнить определенную команду при построении образа.  
**CMD** является входной точкой для запуска приложения.

Пример Dockerfile для приложения написанного на Go.

```Dockerfile
FROM golang:1.21
WORKDIR /app
COPY main.go .
RUN go build -o hello-go main.go
CMD ["./hello-go"]
```