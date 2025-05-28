# <a name="RU"></a>Требования к запуску проекта
- Создать базу данных. Работоспособность программы была проверена при созданной БД в pgAdmin4
- Необходимо заполнить файл user-service.properties в config-service...resources для доступа к БД:
    - **Адрес БД** ```spring.datasource.url:``` \
      Пример: ```spring.datasource.url = jdbc:postgresql://localhost:5432/Users```
    - **Имя пользователя БД** ```spring.datasource.username```
    - **Пароль данного пользователя** ```spring.datasource.password```
- Последовательность запуска микросервисов:
     1. eureka-service
     2. config-service
     3. api-gateway
     4. user-service
     5. Подождать секунд 30 пока все микросервисы полностью не заработают
- Чтобы увидеть Eureka перейти после запуска проекта по ссылке:  http://localhost:8080/eureka/
- Чтобы работать с User-service перейти после запуска проекта по ссылке:  http://localhost:8080/api/users
## Тестирование Circuit Breaker
- Работоспособность Circuit Breaker была протестирована с использованием Postman
- Чтобы протестировать работу fallback метода в api-gateway:
    1. Запускаем все миркосервисы
    2. проверяем что подача запроса (например GET http://localhost:8080/api/users) user-service работает 
    3. Останавливаем user-service
    4. Сразу после этого при постоянном вызове методов user-service наблюдаем работу fallback метода
- Чтобы протестировать работу fallback метода в user-service:
    1. Запускаем все миркосервисы
    2. проверяем что подача запроса (например GET http://localhost:8080/api/users) user-service работает
    3. (На windows) Останавливаем службу postgresql (через services.msc или диспетчер задач)
    4. Сразу после этого при постоянном вызове методов user-service наблюдаем работу fallback методов user-service
# Требования к проекту
Добавить к существующей системе паттерны: gateway api, service discovery, circuit breaker, 
external configuration - реализации данных паттернов можно найти в модулях spring cloud.