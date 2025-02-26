**Задача 1**
Уровень 1: Проектирование
Целью проекта будем считать - обеспечение параллельной независимой разработки функциональности веб-сервиса Mesto.
При проектировании воспользуемся 3-мя стратегиями проектирования:
* вертикальная нарезка
    * По DDD считаем, что есть 2 основных сценария: карточки (просмотр, добавление, удаление, лайки) и профиль (логин, регистрация, аватар, профиль)
* автономность команд (опционально)
    * Позволит командам выбрать собственный стек (при необходимости)
* изоляция
    * Позволит командам включить все зависимости в свой фронтенд и независимо обновлять свои части кода проекта
Для метода интеграции микрофронтендов воспользуемся Run time для обеспечения независимой доработки и выкатки функциональности соседних команд разработки (повышение гибкости и масштабирования команд разработки).
В качестве метода композиции микрофронтендов будем использовать клиентский подход (загрузка микрофронтендов на стороне клиента, в том числе в lazy режиме).

Уровень 2: Планирование изменений
Для создания микрофронтендов воспользуемся module federation (не стоит задача собрать приложение на разных стеках, поэтому выбранное решение соответствует задаче)
В сервисе Mesto по DDD можно выделить 4 функциональных модуля: host, cards, profile и registration
- Host (основное приложение)
- Cards (карточки мест, лайки)
- Profile (профиль)
- Registration (регистрация, логин)

Структура кода:
/host
  /src
    /components
       App.js		           //Корневой компонент
       Main.js              // Компонент страницы с карточками
       Header.js            // Компонент заголовка страницы
       Footer.js	           // Компонент подвала страницы
    /styles
      index.css              // Стили для компонента входа
    /utils
      auth.js                // Утилиты для аутентификации
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js

/cards
  /src
    /components
      AddPlacePopup.js           // Компонент добавления карточки
      Card.js                    // Компонент карточки в таблице (click, like, delete)
      ImagePopup.js              // Компонент открытой карточки
      PopupWithForm.js	         // Компонент удаления карточки
    /styles
      Card.css            // Стили карточки
      Places.css          // Стили таблицы карточек
      popup.css           // Стили для форм
    /utils
      auth.js             // Утилиты для аутентификации
      api.js              // Запросы к API
    index.js              // Точка входа микрофронтенда
  package.json            // Зависимости и скрипты микрофронтенда
  webpack.config.js

/profile
  /src
    /components
      EditAvatarPopup.js   // Компонент редактирования аватара
      EditProfilePopup.js    // Компонент редактирования профиля
    /styles
      popup.css           // Стили для форм
    /utils
      auth.js                // Утилиты для аутентификации
      api.js                  // Запросы к API
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js

/registration
  /src
    /components
      Login.js               // Компонент входа пользователя
      Register.js            // Компонент регистрации пользователя
      Infotooltip.js        // Компонент статусов регистрации
    /styles
      login.css              // Стили для компонента входа
      register.css           // Стили для компонента регистрации
      popup.css           // Стили для форм
    /utils
      auth.js                // Утилиты для аутентификации
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js

**Задача 2**
Описание и декомпозиция на микросервисы:
https://drive.google.com/file/d/1EoCYmVXpOBEmxGF-AbDy8ubLMr6B56fU/view?usp=sharing
