# Сущности

## Покупатель

### Создание покупателя

Запрос на создание нового покупателя.(../#gdfgdfgdfgsozdanie-pokupatelq)

#### Атрибуты сущности
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string`  - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **meta** `object` `Необходимое`
    + **href** `string` - Идентификатор покупателя `Необходимое`
    + **id** `string` - Идентификатор покупателя `Необходимое`
+ **name**`string` - ФИО покупателя 
+ **discountCardNumber** `string` - Номер дисконтной карты
+ **phone** `string` - Номер телефона в произвольном формате
+ **email** `string` - Почтовый адрес

> **`POST`** 
> /counterparty

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.1/entity/retailstore/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    },
    "name": "Магазин №1"
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
    "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
  },
  "name": "Иванов Иван Иванович",
  "discountCardNumber": "MTIzNDU2Nzg5MA",
  "phone": "+7 555 123 4568",
  "email": "email@example.com"
}
```

> **Response**  
> 201

### Поиск покупателя 

Запрос на поиск существующего покупателя.

#### Параметры
| Параметр | Описание   |
|---|---|
| search | `string` *Example: 9039993344* Строка с поисковым запросом |

#### Атрибуты сущности
+ **rows** `array` - Список покупателей
    + Покупатель `object`
        + **id** `string` - Уникальный идентификатор покупателя в системе лояльности в формате GUID `Необходимое`
        + **msId** `string` - Уникальный идентификатор покупателя в системе МойСклад в формате GUID
        + **name** `string` - ФИО покупателя `Необходимое`
        + **discountCardNumber** `string` - Номер дисконтной карты 
        + **phone** `string` - Номер телефона в произвольном формате 
        + **email** `string` - Почтовый адрес

> **`GET`** 
> /counterparty?search=9039993344

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> **Response**  
> 200 (application/json)

```json
{
  "rows": [
    {
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073",
      "msId": "276a6f50-7ffd-11e6-8a84-bae50000005",
      "name": "Иванов Иван Иванович",
      "discountCardNumber": "MTIzNDU2Nzg5MA",
      "phone": "+7 555 123 4567",
      "email": "email@example.com"
    }
  ]
}
```

### Получение баланса баллов покупателя 

Запрос на получение баланса покупателя. Поиск и идентификация покупателя идет по идентификатору покупателя `id` из метаданных.
Прочие реквизиты несут информационный характер и могут не предаваться. Передача нескольких покупателей в ответе **не допускается**.


#### Атрибуты сущности   

+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href**  `string` - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Магазин №1 - Название точки продаж
+ **meta** `object` `Необходимое`
    + **href** `string` - Идентификатор покупателя `Необходимое`
    + **id** `string` - Идентификатор покупателя `Необходимое`
+ **name** `string` - ФИО покупателя 
+ **discountCardNumber** `string` - Номер скидочной карты/счета
+ **phone** `string` - Номер телефона в произвольном формате
+ **email** `string` -  Почтовый адрес  

#### Атрибуты ответа  
+ **bonusProgram** `object` - Блок информации по баллам 
    + **agentBonusBalance** `number` - Баланс баллов покупателя до продажи (текущий баланс)`Необходимое`

> **`POST`** 
> /counterparty/detail

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.1/entity/retailstore/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    },
    "name": "Магазин №1"
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
    "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
  },
  "name": "Иванов Иван Иванович",
  "discountCardNumber": "MTIzNDU2Nzg5MA",
  "phone": "+7 555 123 4567",
  "email": "email@example.com"
}
```
> **Response**  
> 200 (application/json)


> Body

```json
{
  "bonusProgram": {
    "agentBonusBalance": 500
  }
}
```
