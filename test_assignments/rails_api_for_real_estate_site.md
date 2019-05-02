## RoR + Ember: API для сайта продажи/аренды недвижимости

**Условия**

*Ember*

Модели:

- `Building` (здание). Поля: `class:string`, `street:string`, `house_number:string`, `floors:number`;

- `Block` (офисные блоки). Поля: `area:number`, `floor:number`;

- `Price` (цена). Поля: `value:number`, `currency:number`, `1` — рубли, `2` — доллары, `3` — евро).

Связи:

- `Building hasMany Blocks`;

- `Block belongsTo Building`;

- `Block hasMany Offers`;

- `Offer belongsTo Price`.

Создать раут `buildings`.

Создать `template buildings`, в котором будут 4 `input` поля (класс, улица, номер дома и этаж) и кнопка «Добавить».

При нажатии на кнопку «Добавить» отправлять save-запрос к API, в промисе мы добавляем созданный `building` в массив `buildings`. После этого зачищаем форму. Ниже формы отображаем массив созданных `buildings`.

**Дополнительно:**

В `template buildings` добавить возможность добавлять `block` => `offer` => `price`. То есть помимо обычных инпутов в форму создания здания добавить ещё кнопку «Добавить блок». При нажатии на неё появляется форма с инпутами для создания модели `block`, которая привязывается к модели `building`. В форме блока, соответственно, есть кнопка «Добавить предложение», при нажатии на которую появляется форма с полями `offer` и кнопкой «Добавить цену». Цена по аналогии. 

*Rails*

Создать небольшое API.

Модели:

- `Building` (здание). Поля: `class:string`, `street:string`, `house_number:string`, `floors:integer`;

- `Block` (офисные блоки). Поля: `area:integer`, `floor:integer`;

- `Offer` (предложение). Поля: `offer_type:string`, `rent` — аренда, `sale` — продажа;

- `Price` (цена). Поля: `value:integer` (limit — 8), `currency:integer`, `1` — рубли, `2` — доллары, `3` — евро).

Связи:

- `Building has_many :blocks`;

- `Block belongs_to :building`;

- `Block has_many :offers`;

- `Offer has_one :price`. 

Контроллеры:

Создать контроллер для `building` с методами `create`, `update`, `delete`, `index`, `show`. 

В `create` должна создаваться модель `Building` (без параметров в запросе, просто вызывать метод создания модели). Возвращать `render json` созданной модели.

В `update` должна сохраняться модель `Building` с соответствующим `id` (без параметров в запросе, просто вызывать метод сохранения модели). Возвращать `render json` созданной модели.

В `delete` удалять модель с соответствующим `id`.

В `show` возвращать `render json` модели `Building` с определённым `id`.

В `index` возвращать `Building`. В `params` могут быть переданы все поля модели `building` и по ним желательно вести поиск и возвращать отфильтрованные значения.

Выбор БД на ваше усмотрение. 

*SQL*

Написать одинаковые запросы на SQL и на Rails ORM. 

Найти все офисные блоки от 150 до 300 кв.м включительно, которые находятся на 1, 8 или 10 этажах, сдаются в аренду по цене не более $5000 в зданиях класса «А» на Пресненской набережной. 

*Объединение frontend + backend + БД*

С фронта отправлять запрос на созданное Rails API. В `create` методе `buildings_controller` берём поля из тела POST-запроса.