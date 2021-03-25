## Продажа 

### Расчет скидок для продажи 

Запрос на пересчет скидок для операции продажи. В запросе передается продажа без применения скидок. В ответе ожидается продажа со всеми примененными скидками. В случае округления суммы чека, допускается разбиение одной позии на две.

Если проишло разбиение позиции, то необходимо учитывать значение в поле sn (серийные номера). Правило следующее - количество серийных номеров изначальной позиции совпадает с количеством серийных номеров в позициях, получившихся в результате разбиения. Так же, количество серийных номеров должно быть равно количеству товара (поле quantity).

После расчета скидок, приложение уже никак не меняет состав чека и не применяет другие скидки.
     
#### Атрибуты сущности  
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **agent** `object` - Реквизиты покупателя в формате метаданных`Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Идентификатор покупателя`Необходимое`
        + **id** `string` - Идентификатор покупателя`Необходимое`
    + **name** `string` - ФИО покупателя 
    + **discountCardNumber** `string` - Номер скидочной карты/счета
    + **phone** `string` - Номер телефона в произвольном формате 
    + **email** `string` - Почтовый адрес 
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных`Необходимое`
        + **meta** `object```Необходимое`
            + **href** `string` - Идентификатор товара/услуги `Необходимое`
            + **id** `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity** `number` - Количество в чеке (3 зн. после запятой) `Необходимое`
    + **price** `number` - Цена за единицу (2 зн. после запятой) `Необходимое`
    + **sn** `array` - Список серийных номеров в формате метаданных
          + **meta** `object` `Необходимое`
              + **href** `string` - Идентификатор серийного номера  `Необходимое`
              + **id** `string` - Идентификатор серийного номера `Необходимое`
          + **name** `string` - Серийный номер `string` 
+ **bonusProgram** `object` - Блок информации по баллам `object` 
    + **transactionType** `enum[string]` - Тип операции с баллами (начисление - EARNING, списание - SPENDING) 
        + Default: EARNING
        + Members 
            + EARNING
            + SPENDING     

> **`POST`** 
> /retaildemand/recalc

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
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com"
  },
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
      "sn": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/thing/2b5eb22f-139e-11e6-9464-e4de00000073",
            "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
          },
          "name": "7895545"
        }
      ]
    }
  ],
  "bonusProgram": {
    "transactionType": "EARNING"
  }
}
```

#### Атрибуты ответа  
+ **agent** `object` - Реквизиты покупателя в формате метаданных `Необходимое`
    + **meta** `object` `Необходимое`
        + **href**: `string` - Идентификатор покупателя `Необходимое`
        + **id**: `string` - Идентификатор покупателя `Необходимое`
    + **name**: `string` - ФИО покупателя
    + **discountCardNumber**: `string` - Номер скидочной карты/счета
    + **phone**: `string` - Номер телефона в произвольном формате
    + **email**: `string` - Почтовый адрес  
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных `Необходимое`
        + **meta** `object` `Необходимое`
            + **href**: `string` - Идентификатор товара/услуги `Необходимое`
            + **id**: `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity**: `number` - Количество в чеке (3 зн. после запятой) `Необходимое`
    + **price**: `number` - Цена за единицу (2 зн. после запятой) `Необходимое`
    + **discountPercent**: `number` - Процент скидки (2 зн. после запятой). от 0 до 100 `Необходимое`
    + **discountedPrice**: `number` - Цена с учетом скидки (2 зн. после запятой) `Необходимое`
    + **sn** `array` - Коллекция уникальных идентификаторов серийных номеров в формате метаданных. Если массив не пуст, то количество товаров в позиции (quantity) должно быть равно количеству серийных номеров, переданных в значении атрибута
          + **meta** `object` `Необходимое`
              + **href**: `string` - Идентификатор серийного номера `Необходимое`
              + **id**: `string` - Идентификатор серийного номера `Необходимое`
          + **name**: `string` - Серийный номер
+ **bonusProgram** `object` - Блок информации по баллам
    + **transactionType**: `enum[string]` - Тип операции с баллами (начисление - EARNING, списание - SPENDING)
        + Default: EARNING
        + Members 
            + EARNING
            + SPENDING
    + **agentBonusBalance**: `number` - Баланс баллов покупателя до продажи
    + **bonusValueToSpend**: `number` - Сколько может быть списано баллов за продажу
    + **bonusValueToEarn**: `number` - Сколько может быть начислено баллов за продажу
    + **agentBonusBalanceAfter**: `number` - Баланс баллов покупателя после продажи
    + **paidByBonusPoints**: `number` - Сумма оплаченная бонусами (2 зн. после запятой)
    + **receiptExtraInfo**: `string` - Дополнительный текст для вывода в чеке, может содержать переносы строк.

> **Response**   
> 200 (application/json)

> Headers

```
Content-Type:application/json
```

> Body

```json
{
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com"
  },
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
      "discountedPrice": 62.95,
      "sn": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/thing/2b5eb22f-139e-11e6-9464-e4de00000073",
            "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
          },
          "name": "7895545"
        }
      ]
    }
  ],
  "bonusProgram": {
    "transactionType": "EARNING",
    "agentBonusBalance": 500,
    "bonusValueToSpend": 0,
    "bonusValueToEarn": 150,
    "agentBonusBalanceAfter": 650,
    "paidByBonusPoints": 0,
    "receiptExtraInfo": "Спасибо за участие в нашей программе!"
  }
}
```

### Создание продажи 

Запрос на создание новой продажи. Если при продаже начислялись или списывались баллы, информация об этом указывается в секции `bonusProgram`

#### Атрибуты сущности  
  
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string`- Идентификатор точки продаж `Необходимое`
        + **id**: `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **name** `string` - Номер продажи
+ **moment** `string` - Дата продажи
+ **meta** `object` - Реквизиты продажи в формате метаданных `Необходимое`
    + **href** `string` - Идентификатор продажи (URL) `Необходимое`
    + **id** `string` - Идентификатор продажи `Необходимое`
+ **agent** `object` - Реквизиты покупателя в формате метаданных
    + **meta** `object`
        + **href** `string` - Идентификатор покупателя `Необходимое`
        + **id** `string` - Идентификатор покупателя `Необходимое`
    + **name** `string` - ФИО покупателя
    + **discountCardNumber** `string` - Номер скидочной карты/счета
    + **phone** `string` - Номер телефона в произвольном формате
    + **email** `string` - Почтовый адрес
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных
        + **meta** `object`
            + **href** `string` - Идентификатор товара/услуги `Необходимое`
            + **id** `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity** `number` - Количество в чеке (3 зн. после запятой)
    + **price** `number` - Цена за единицу (2 зн. после запятой)
    + **discountPercent** `number` - Процент скидки (2 зн. после запятой)
    + **discountedPrice** `number` - Цена с учетом скидки (2 зн. после запятой)
+ **bonusProgram** `object` - Блок информации по баллам
    + **bonusValueToSpend** `number` - Сколько может быть списано баллов за продажу
    + **bonusValueToEarn** `number` - Сколько может быть начислено баллов за продажу
+ **cashSum** `number` - Оплачено наличными
+ **noCashSum** `number` - Оплачено картой

> **`POST`** 
> /retaildemand

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
  "moment": "2016-04-18 15:06:00",
  "meta": {
    "href": "",
    "id": ""
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com"
  },
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
  "bonusProgram": {
    "bonusValueToSpend": 0,
    "bonusValueToEarn": 150
  },
  "cashSum": 62.95,
  "noCashSum": 283.1
} 
```


> **Response**  
> 201
