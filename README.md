 
# Задание № 1 (проект сдается без запуска кода)
## Базовая функциональность, которая есть сейчас:
- загрузка фотографий;
- удаление фотографий;
- сбор и учет лайков под фото;
- создание профиля и его редактирование;

### Структура проекта
- `src` - исходный код всего проекта
- `src/components` - компоненты
- `src/blocks` - стили в формате БЭМ
- `src/utils` - утилиты для вызова АПИ

 ### Компоненты и модули

- `App` - корневой компонент текущего проекта, собирает все компоненты вместе и управляет логикой взаимодействия, кроме того содержит роутинг
- `Main` - основное тело приложения, содержит информацию о пользователе и карточки мест
- `Register`, `Login` - формы регистрации и логина в систему 
- `EditProfilePopup` - Pop-up для редактирования профиля пользователя 
- `AddPlacePopup` - Pop-up редактирования места 
- `EditAvatarPopup` - Pop-up редактирования аватара 
- `ImagePopup` - Pop-up для просмотра изображения 

## Разделение проекта на микрофронты. Стратегии
Есть 2 стратегии разделения на  микрофронты, а именно:
- горизонтальная (разделение по функциям, на одной странице несколько функций)
 - вертикальная (разделение по пути, на странице только одна функция)

Я использовал вертикальную нарезку.

При выборе инструмента для микрофронтов мой выбор был сделан в пользу **Webpack Module Federation** по следующим причинам:
- динамическая загрузка кода;
- совместное использование зависимостей;
- изоляция и независимость;
- гибкость в разработке;

### Структура файлов нового проекта на основе микрофронтов
Все микрофоонты находятся в папке **microfrontends**:
1. `host` (port 8080) - основной микрофронтенд, который будет осуществлять сборку, оркестрацию и  управлять роутингов. 
2. `users`(port 8081) - фронтенд функционала пользователями: регистрация, логин в систему, отображение и управление данными пользователей
3. `places` (port 8082) - фронтенд функционала места: лента мест, карточки, лайки, создание и удаление мест, редактирование мест

У всех микрофронтов будет одинаковая структура, а именно:
- `components` - набор компонентов
- `blocks` - стили
- `utils` - вызовы api
- `images` - картинки, логотипы, иконки, которые относятся к конкретному микрофронту

### Запуск
# Задание № 1 (проект сдается без запуска кода)


# Задание №2
 ### Компоненты и модули
 - `API Gateway` - начальная страница проекта. Проверяет валидность JWT токена и наличие его идентификатора в списке отозванных.
Отозванные JWT хранятся в базе данных Redis и удаляются после истечения срока действия

- `Сервис отчетов` - формировует отчеты по запросу пользователей. В базе данных хранятся основные шаблоны отчетов, шаблоны можно создавать новые. На основании запроса пользователя собирает информацию от других сервисов.

- `Сервис торговых площадок` - сервис создания торговых площадок с операциями CRUD.

- `Сервис услуг` - сервис CRUD операций с услугами и предоставления ID услуги в случае ее участия в аукционе.

- `Сервис товаров` - сервис CRUD операций с товарами и с предоставлением ID акциона в случае участия товара в аукционе.

- `Сервис управления заказами` - сервис отвечает за заказы товаров и услуг напрямую или через аукцион. Позволяет отслеживать статус заказов и взаимодействует с платежной системой.

- `Сервис управления аукционами` - сервис организации процесса аукциона. Хранит в себе параметры аукциона и историю ставок. В процессе аукциона создает заказ для последующей оплаты.

- `Сервис управления аккаунтами` -  сервис отвечает за пользователей системы и генерацию JWT токенов. При аутентификации пользователя генерируется JWT токен и добавляется в Redis. Ключ = ID пользователя, значение = json массив с идентификаторами JWT и другими признаками пользователя. Срок действия записи = максимальный срок действия JWT в таблице. Этот механизм позволит отзывать ранее выданные сертификаты.

 - `Сервис управления заявками аукциона` - серви управления и обработки заявок аукциона. 

- `Сервис технической поддержки` - сервис отвечает за  регистрацию заявок в техническую поддержку.

- `Сервис нотификации` -  сервис уведомлеяет заинтересованный стороны через websocet или через smtp на почту.

- `Платежный сервис` отвечает за взаимодействие с платежными системами. Позволяет проводить платежи, Отслеживает статусы платежей, Генерирует события прохождения транзакции

**Схема решения в корне. Файл Схема архитектурного решения на основе микрофронтов.drawio**

**UPD**
- Задание 1 сдается без запуска кода. Исправил.
- Сервис ТП есть, описан  и есть на диаграмме. На предмет персонала немного не понял, но буду думать! 
