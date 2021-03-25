## Возврат 

### Создание возврата 

Запрос на создание нового возврата. В составе запроса может быть указана ссылка на документ продажи. Операции с баллами в составе возврата не передаются.
Система лояльности, на основании информации из связанной продажи, самостоятельно начисляет/списывает баллы при необходимости.

#### Атрибуты сущности   

+ **retailStore** `object` `Необходимое`
    + **meta** `object`
        + **href**: `string` - Идентификатор точки продаж `Необходимое`
        + **id**: `string - Идентификатор точки продаж `Необходимое`
    + **name**: `string` - Название точки продаж
+ **name**: `string` Номер возврата
+ **moment**: `string` Дата возврата
+ **meta** `object` - Реквизиты возврата в формате метаданных `Необходимое`
    + **href** `string` - Идентификатор возврата (URL) `Необходимое`
    + **id** `string` - Идентификатор возврата `Необходимое`
+ **demand** `object` - Реквизиты продажи в формате метаданных
    + **meta** `object`
        + **href** `string` - Идентификатор продажи (URL) `Необходимое`
        + **id** `string` Необходимое) - Идентификатор продажи `Необходимое`
+ **agent** `object` - Реквизиты покупателя в формате метаданных
    + **meta** `object`
        + **href**: `string` - Идентификатор покупателя `Необходимое`
        + **id**: `string` - Идентификатор покупателя `Необходимое`
    + **name**: `string` - ФИО покупателя
    + **discountCardNumber**: `string` - Номер скидочной карты/счета
    + **phone**: `string` - Номер телефона в произвольном формате
    + **email**: `string` - Почтовый адрес
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных
        + **meta** `object`
            + **href**: `string` - Идентификатор товара/услуги `Необходимое`
            + **id**: `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity**: `number` - Количество в чеке (3 зн. после запятой)
    + **price**: `number` - Цена за единицу (2 зн. после запятой)
    + **discountPercent**: `number` - Процент скидки (2 зн. после запятой)
    + **discountedPrice**: `number` - Цена с учетом скидки (2 зн. после запятой)
+ **cashSum**: `number` - Возвращено наличными
+ **noCashSum**: `number` - Возвращено картой


> **`POST`** 
> /retailsalesreturn

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
  "name": "00001",
  "moment": "2016-04-27 15:43:00",
  "meta": {
    "href": "",
    "id": ""
  },
  "demand": {
    "meta": {
      "href": "",
      "id": ""
    }
  },
  "agent": {},
  "positions": [
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/9c56720c-e8a7-4fdc-aea4-7104f28207be",
          "id": "9c56720c-e8a7-4fdc-aea4-7104f28207be"
        }
      },
      "quantity": 123.456,
      "price": 123.45,
      "discountPercent": 49.99,
      "discountedPrice": 62.95
    }
  ],
  "cashSum": 62.95,
  "noCashSum": 283.1
}
```
> **Response**  
> 201



