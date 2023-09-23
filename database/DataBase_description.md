# В этом файле будет описан процесс создания и функционирования базы данных приложения

# База данных будет разворачиваться на сервере MSSQL

## Скрипт создания базы данных
```sql
CREATE database Permit_web_app IF NOT EXISTS
```

# Структура базы данных
База данных будет состоять из следующих таблиц:
- "Company" - таблица с компаниями-подрядчиками
- "Visitor" - таблица с данными о посетителях
- "Supervisor" - таблица с данными кураторах подрядчиков
- "Access_area" - таблица с данными о зонах доступа
- "Goal" - таблица с данными о целях посещения


# Структура таблицы "Company"
| Поле | Тип данных | Описание |
| --- | --- | --- |
| Id | int | Идентификатор компании |
| Name | nvarchar(50) | Название компании |
| SupervisorId | int | Идентификатор куратора компании |

# Скрипт создания таблицы "Company"
```sql 
IF OBJECT_ID('Company', 'U') IS NULL
CREATE TABLE Company (
    Id int NOT NULL PRIMARY KEY,
    Name nvarchar(50) NOT NULL,
    SupervisorId int NOT NULL FOREIGN KEY REFERENCES Supervisor(Id)
)
```
# Структура таблицы "Visitor"
| Поле | Тип данных | Описание |
| --- | --- | --- |
| Id | int | Идентификатор посетителя |
| Name | nvarchar(50) | Имя посетителя |
| Surname | nvarchar(50) | Фамилия посетителя |
| Patronymic | nvarchar(50) | Отчество посетителя |
| Birthday | date | Дата рождения посетителя |
|IIN | nvarchar(12) | ИИН посетителя |
| CompanyId | int | Идентификатор компании, в которой работает посетитель |
| BlackList | bit | Признак нахождения посетителя в черном списке |

# Скрипт создания таблицы "Visitor"
```sql
IF OBJECT_ID('Visitor', 'U') IS NULL
CREATE TABLE Visitor (
    Id int NOT NULL PRIMARY KEY,
    Name nvarchar(50) NOT NULL,
    Surname nvarchar(50) NOT NULL,
    Patronymic nvarchar(50),
    Birthday date,
    IIN nvarchar(12) NOT NULL,
    CompanyId int NOT NULL FOREIGN KEY REFERENCES Company(Id)
    BlackList bit NOT NULL DEFAULT 0
)
```
# Структура таблицы "Supervisor"
| Поле | Тип данных | Описание |
| --- | --- | --- |
| Id | int | Идентификатор куратора |
| Name | nvarchar(50) | Имя Дирекции |

# Скрипт создания таблицы "Supervisor"
```sql
IF OBJECT_ID('Supervisor', 'U') IS NULL
CREATE TABLE Supervisor (
    Id int NOT NULL PRIMARY KEY,
    Name nvarchar(15) NOT NULL
)
```
# Структура таблицы "Access_area"

| Поле | Тип данных | Описание |
| --- | --- | --- |
| Id | int | Идентификатор зоны доступа |
| Name | nvarchar(50) | Название зоны доступа |

# Скрипт создания таблицы "Access_area"
```sql
IF OBJECT_ID('Access_area', 'U') IS NULL
CREATE TABLE Access_area (
    Id int NOT NULL PRIMARY KEY,
    Name nvarchar(50) NOT NULL
)
```
# Структура таблицы "Goal"

| Поле | Тип данных | Описание |
| --- | --- | --- |
| Id | int | Идентификатор цели посещения |
| Name | nvarchar(50) | Название цели посещения |

# Скрипт создания таблицы "Goal"
```sql
IF OBJECT_ID('Goal', 'U') IS NULL
CREATE TABLE Goal (
    Id int NOT NULL PRIMARY KEY,
    Name nvarchar(50) NOT NULL
)
```




