## Возврат 

### Создание возврата 

Запрос на создание нового возврата. В составе запроса может быть указана ссылка на документ продажи. Операции с баллами в составе возврата не передаются.
Система лояльности, на основании информации из связанной продажи, самостоятельно начисляет/списывает баллы при необходимости.

#### Атрибуты сущности   

+ **retailStore** `object` `required`
    + **meta** `object`
        + **href**: `string` - Идентификатор точки продаж `required`
        + **id**: `string - Идентификатор точки продаж `required`
    + **name**: `string` - Название точки продаж
+ **name**: `string` Номер возврата
+ **moment**: `string` Дата возврата
+ **meta** `object` - Реквизиты возврата в формате метаданных `required`
    + **href** `string` - Идентификатор возврата (URL) `required`
    + **id** `string` - Идентификатор возврата `required`
+ **demand** `object` - Реквизиты продажи в формате метаданных
    + **meta** `object`
        + **href** `string` - Идентификатор продажи (URL) `required`
        + **id** `string` required) - Идентификатор продажи `required`
+ **agent** `object` - Реквизиты покупателя в формате метаданных
        + **meta** `object`
            + **href**: `string` - Идентификатор покупателя `required`
            + **id**: `string` - Идентификатор покупателя `required`
        + **name**: `string` - ФИО покупателя
        + **discountCardNumber**: `string` - Номер скидочной карты/счета
        + **phone**: `string` - Номер телефона в произвольном формате
        + **email**: `string` - Почтовый адрес
+ **positions** `array` - Перечень всех позиций чека
    + `object`
        + **assortment** `object` - Реквизиты позиции в формате метаданных
            + **meta** `object`
                + **href**: `string` - Идентификатор товара/услуги `required`
                + **id**: `string` - Идентификатор товара/услуги `required`
        + **quantity**: `number` - Количество в чеке (3 зн. после запятой)
        + **price**: `number` - Цена за единицу (2 зн. после запятой)
        + **discountPercent**: `number` - Процент скидки (2 зн. после запятой)
        + **discountedPrice**: `number` - Цена с учетом скидки (2 зн. после запятой)
+ **cashSum**: `number` - Возвращено наличными
+ **noCashSum**: `number` - Возвращено картой


> **`POST`** 
> http://example.com/baseurl/api/moysklad/loyalty/1.0/retailsalesreturn

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



