
# Решение команды «МИСИС Два миллиона»

Наша команда разработала распределенную систему для прогнозирования и формирования закупок. Основным нашим преимуществом является простота системы, скорость взаимодействия и возможности, реализованные под решение конкретных проблем бизнеса (написать конкретику вместо общих слов)

## Основные ссылки

1. [**Ссылка на админ-панель**](https://purchasing-assistant.itatmisis.ru/#)
2. [**Ссылка на чат-бота**](https://t.me/Purchasing_Assistant_bot)
*данные для входа в админ-панель указаны в документации к использованию сервиса*
3. [**Скринкаст работы сервиса**](#)

## Инструкция для запуска
```
1. git clone https://github.com/ParkieV/lct2024.git && cd lct2024
2. настройка переменных окружения и конфигураций
    2.1. backend/src/.envs/app.env # пример в backend/src/.envs/app.example.env
    2.2. backend/src/.envs/auth.env # пример в backend/src/.envs/auth.example.env
    2.3. backend/src/.envs/db.env # пример в backend/src/.envs/db.example.env
    2.4. backend/src/.envs/redis.env # пример в backend/src/.envs/redis.example.env
3. docker compose up
```

## Архитектура

![Картинка архитектуры системы]()

### Компоненты системы

#### Чат-бот

Мы реализовали чат-бот на основе Telegram API (библиотека aiogram) в виду его популярности среди пользователей и удобстве использования. Соедниение чат-бота реализовано на основе технологии WebSocket.
Пользовательский путь в чат-боте представляет из себя ориентированный граф, где есть присутсвует понятие **История** - возможность возвращаться на предыдущие этапы путем нажатия на кнопку **Назад**

Функционал чат-бота:
- Авторизация и деавторизация.
- Общий анализ закупок по годам/кварталам/месяцам и по цене/количеству.
- Просмотр и редактирование баланса, просмотр общей стоимости каждой и всех закупок.
- Создание, удаление закупки и ее выбор в случае, если она создана.
- Добавление в закупку товара. Стоимость, объем и даты поставок определяются сервисом автоматически, если товар регулярный.
- Матчинг товара с возможностью ввода с помощью аудио - реализация Speech2Text для этого. 
- График прогнозирования товара по годам/кварталам/месяцам.
- Анализ товара
  - Файл с последними N закупками товара. Число N пользователь вводит сам.
  - График статистики по закупкам товара по годам/кварталам/месяцам и по цене/количеству.
  - График по обороту дебет/кредит по годам/кварталам/месяцам и по цене/количеству.
  - График с остатками товара на складе.


![image](https://github.com/ParkieV/lct2024/assets/61056244/9dfa46ee-8aea-4e10-aad0-9fa50a4ef8c0)


#### Админ-панель

В панели администратора доступны следующие функции:
 * Зарегистрировать организацию.
 * Создавать новых пользователей.
 * Список пользователей.
 * Просматривать информацию уже существующих пользователей.
 * Редактировать информацию о существующих пользователей.
 * Удаление пользователей.
*Открытой регистрации для пользователей в админ-панели нет в целях избежания утечки данных.*
![Картинка админ-панели](images/admin_pic.png)

#### Основное API

Является ядром нашего решения. Данный сервис отвечает за сохранение данных пользователя, передает информацию о предсказаниях и аналитике, а также реализует систему авторизации. Он может быть использован отдельно от чат-бота, позволяя сохранить все основные возможности системы. Взаимодействие реализовано на основе протокола HTTP.

[Документация к API](https://purchasing-assistant.itatmisis.ru/api/docs)


## ML
---

[Документация к API](https://purchasing-assistant.itatmisis.ru/api_ml/docs)

## Backend
---
### Стек технологий
* **Python** - основной язык, на котором написано центральное API и телеграм-бот
* **FastAPI** - фреймворк для написания API сервисов
* **Pydantic** - валидация данных
* **SQLAlchemy** - взаимодействие с базой данных
* **PyJWT** - реализация JWT
* **Redis** - кэширование данных
* **Postgres** - основное хранилище данных
* **Asyncpg** - асинхронный драйвер для взаимодействия с PostgreSQL
* **Aiogramm** - асинхронная библиотека для написания тг-ботов
* **Aiohttp** - асинхронная библиотека для реализации API
* **Aiosqlite** - асинхронный драйвер для взаимодействия с локальным хранилищем SQLite
### Почему такой стек?
Архитектура системы - микросервисы. Это позволяет системе быть модульной, масштабируемой и иметь возможность заменить и дополнить сервисы без нарушения работы системы.

Также можно выделить простоту поддержки, высокую скорость работы. Архитектура системы упрощена засчет сокращения количества подключаемых сервисов. Система защищена от несанкционированного доступа с помощью JWT токенов используемых для взаимодействия с сервисами приложения.

## Frontend
---
### Стек технологий
* **ReactJS**
* **Redux-Toolkit**
* **React-Router**
* **JavaScript**
* **WebPack5**
* **Babel**
* **HTML5**
* **CSS3**
### Почему такой стек?

