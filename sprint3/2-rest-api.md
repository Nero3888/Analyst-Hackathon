# REST API

## Клиенты REST API

Клиенты REST API:
- Web-приложение
- Мобильное приложение
- REST API-интерфейс продавца
- REST API-интерфейс администратора


## Роли

- Анонимный пользователь
- Зарегистрированный покупатель
- Зарегистрированный продавец
- Модератор
- Администратор

## Запросы и ответы

### 1. Получение списка всех продуктов

`GET /goods/ HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
</br>
</br>

`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
[
	{
		"goodId": "77efa7c2-c082-4025-a8b9-aba8a3a49c39",
		"goodName": "Молоко 2,5%",
		"description": "Молоко коровье пастеризованное 2,5% жирности",
		"group": "Молочные продукты",
		"cost": "89",
		"sellerName": "Молочное море",
		"status": "В наличии",
		"remainingNumber": "19",
		"createdAt": "2022-06-22T11:28:28.258884Z",
		"updatedAt": "2022-06-22T11:28:28.258884Z"
	},
	{
		"goodId": "c035ab89-ab50-4778-b05d-9e9f82a50996",
		"goodName": "Сливки 20%",
		"description": "Сливки из коровьего молока нормализованные 20% жирности",
		"group": "Молочные продукты",
		"cost": "169",
		"sellerName": "Брянский молочник",
		"status": "В наличии",
		"remainingNumber": "7",
		"createdAt": "2022-06-22T22:57:46.221684Z",
		"updatedAt": "2022-06-22T22:57:46.221684Z"
	}
	{
		...
	}
]
```
Запрос доступен для ролей: анонимный пользователь, зарегистрированный покупатель, зарегистрированный продавец, модератор, администратор.


### 2. Получение отфильтрованного списка продуктов

#### 2.1. Поиск по ключевому слову 

`GET /goods?q=Молоко HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
</br>
</br>

`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
[
	{
		"goodId": "77efa7c2-c082-4025-a8b9-aba8a3a49c39",
		"goodName": "Молоко 2,5%",
		"description": "Молоко коровье пастеризованное 2,5% жирности",
		"group": "Молочные продукты",
		"cost": "89",
		"sellerName": "Молочное море",
		"status": "В наличии",
		"remainingNumber": "19",
		"createdAt": "2022-06-22T11:28:28.258884Z",
		"updatedAt": "2022-06-22T11:28:28.258884Z"
	},
	{
		...
	}
]
```

#### 2.2. Поиск по стоимости 

`GET /goods?$filter=cost le 100 HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
</br>
</br>

`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
[
	{
  	    "goodId": "77efa7c2-c082-4025-a8b9-aba8a3a49c39",
  	    "goodName": "Молоко 2,5%",
  	    "description": "Молоко коровье пастеризованное 2,5% жирности",
 	    "group": "Молочные продукты",
  	    "cost": "89",
		"sellerName": "Молочное море",
		"status": "В наличии",
		"remainingNumber": "19",
		"createdAt": "2022-06-22T11:28:28.258884Z",
		"updatedAt": "2022-06-22T11:28:28.258884Z"
	}
	{
		...
	}
]
```
Запрос доступен для ролей: анонимный пользователь, зарегистрированный покупатель, зарегистрированный продавец, модератор, администратор.


### 3. Получение информации о конкретном продукте

`GET /goods/77efa7c2-c082-4025-a8b9-aba8a3a49c39/ HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
</br>
</br>

`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

```json
{
	"goodId": "77efa7c2-c082-4025-a8b9-aba8a3a49c39",
	"goodName": "Молоко 2,5%",
	"description": "Молоко коровье пастеризованное 2,5% жирности",
	"group": "Молочные продукты",
	"cost": "89",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "19",
	"createdAt": "2022-06-22T11:28:28.258884Z",
	"updatedAt": "2022-06-22T11:28:28.258884Z"
},
```
Запрос доступен для ролей: анонимный пользователь, зарегистрированный покупатель, зарегистрированный продавец, модератор, администратор.


### 4. Добавление товара в корзину 

`POST /carts HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 204`<br>
`Content-Type: application/json; charset=utf-8`<br>

`{`<br>
`     "created_by": userID = h6582x95-4052-4u5t-8432-41fef90045b,`<br>
`     "order_items": [f7462e95-4f00-4e5a-8432-41fef909805c, c035ab89-ab50-4778-b05d-9e9f82a50996]`<br>
`     "subtotal": 258,`<br>
`     "tax_percentage": 0,`<br>
`		"tax_total": 0,`
`     "total": 258,`<br>
`}`

</br>
</br>

`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, модератора,  администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
   	"order_items": ["f7462e95-4f00-4e5a-8432-41fef909805c", "c035ab89-ab50-4778-b05d-9e9f82a50996"],
   	"subtotal": 258,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 258,
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 5. Изменение количества товара в корзине 

`PUT /carts/h6582x95-4052-4u5t-8432-41fef90045b HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 583`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
   	"order_items": ["f7462e95-4f00-4e5a-8432-41fef909805c", "c035ab89-ab50-4778-b05d-9e9f82a50996"],
   	"subtotal": 427,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 427,
}
```

`GET /carts/h6582x95-4052-4u5t-8432-41fef90045b`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	  			"count": 1
			},
	  		{
				"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
				"count": 2
			}
		},
   	"subtotal": 427,
    	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 427,
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 6. Удаление товара из корзины 

`PUT /carts/h6582x95-4052-4u5t-8432-41fef90045b HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 106`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
				"count": 1
	  		},
	  	},
}
```


`GET /carts/h6582x95-4052-4u5t-8432-41fef90045b`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
				"count": 1
	  		},
			{
				"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
				"count": 1
			},
		},
		"subtotal": 69,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 69,
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 7. Оформление заказа 

`POST /orders HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 204`<br>
`Content-Type: application/json; charset=utf-8`<br>

```json
{
	"created_by": userID = h6582x95-4052-4u5t-8432-41fef90045b,
	"order_items": [f7462e95-4f00-4e5a-8432-41fef909805c, c035ab89-ab50-4778-b05d-9e9f82a50996]
	"subtotal": 258,
	"tax_percentage": 0,
	"tax_total": 0,
	"total": 258,
	"deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 1",
	"deliveryTime": "2022-06-29T12:00:00.258884Z",
}
```

`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
		"orderId": "e436agi54-ef12-4492-r32d-6e2f53v491984",
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	  			"count": 1
			},
	  		{
				"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
				"count": 1
				}
		},
     "subtotal": 258,
     "tax_percentage": 0,
		"tax_total": 0,
     "total": 258,
	  "deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 1",
     "deliveryTime": "2022-06-29T12:00:00.258884Z",
	  "deliverystatus": "В обработке",
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 8. Изменение места доставки заказа 

`PUT /orders/e436agi54-ef12-4492-r32d-6e2f53v491984 HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 106`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
   	"deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 51",
}
```

`GET /orders/e436agi54-ef12-4492-r32d-6e2f53v491984`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
		"orderId": "e436agi54-ef12-4492-r32d-6e2f53v491984",
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	  			"count": 1
	  		},
	  		{
				"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
				"count": 1
			},
		},
   	"subtotal": 258,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 258,
		"deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 51",
   	"deliveryTime": "2022-06-29T12:00:00.258884Z",
		"deliverystatus": "В обработке",
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 9. Получение списка заказов пользователя 

`GET /orders?$userID=h6582x95-4052-4u5t-8432-41fef90045b HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
</br>
</br>

`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для зарегистрированного покупателя; PUT, PATCH,DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
		"orderId": "e436agi54-ef12-4492-r32d-6e2f53v491984",
   	"order_items": 
		{
			{
				"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	 			"count": 1
	  		},
	  		{
				"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
				"count": 1
			},
		},
   	"subtotal": 258,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 258,
		"deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 51",
   	"deliveryTime": "2022-06-29T12:00:00.258884Z",
		"deliverystatus": "В обработке",
}

{
	...
}
```
Запрос доступен для ролей: зарегистрированный покупатель, администратор.


### 10. Отмена заказа 

`DELETE orders/e436agi54-ef12-4492-r32d-6e2f53v491984`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 200 OK`<br>

`GET /orders/e436agi54-ef12-4492-r32d-6e2f53v491984`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 204 No Content`<br>
`Allow: [GET, HEAD, OPTIONS - для зарегистрированного покупателя; PUT, PATCH,DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
Запрос доступен для ролей: зарегистрированный покупатель, зарегистрированный продавец, администратор.


### 11. Изменение статуса заказа 

`PATCH /orders/e436agi54-ef12-4492-r32d-6e2f53v491984 HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 106`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
		"deliverystatus": "Выполняется",
}
```

`GET /orders/e436agi54-ef12-4492-r32d-6e2f53v491984`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
   	"created_by": userID = "h6582x95-4052-4u5t-8432-41fef90045b",
		"orderId": "e436agi54-ef12-4492-r32d-6e2f53v491984",
   	"order_items": 
		{
			{
			"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	  		"count": 1
	  		},
	  		{
			"goodID": "c035ab89-ab50-4778-b05d-9e9f82a50996",
			"count": 1
			},
		},
   	"subtotal": 258,
   	"tax_percentage": 0,
		"tax_total": 0,
   	"total": 258,
		"deliveryAdress": "г. Калуга, ул. Тульская, д. 34/2, кв. 51",
   	"deliveryTime": "2022-06-29T12:00:00.258884Z",
		"deliverystatus": "Выполняется",
}
```
Запрос доступен для ролей: зарегистрированный продавец, администратор.


### 12. Добавление отзыва о товаре (на модерацию)

`POST moderation/revievs HTTP/1.1 ` <br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 690`<br>
`Content-Type: application/json; charset=utf-8`<br>

```json
{
   	"created_by": "h6582x95-4052-4u5t-8432-41fef90045b",
	"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"sellerID": "y5698e95-2r10-6f4o-3471-52hgf654325v",
	"score": 5,
	"review": "Товар понравился",
}
```
</br>
</br>

`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH, DELETE - для модератора, администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

```json
{
   	"revievID": "g9749r45-4h00-8b3e-59ynd87942v",
	"created_by": "h6582x95-4052-4u5t-8432-41fef90045b",
	"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"sellerID": "y5698e95-2r10-6f4o-3471-52hgf654325v",
	"score": 5,
	"review": "Товар понравился",
}
```
Запрос доступен для ролей: зарегистрированный покупатель.


### 13. Редактирование отзыва о товаре 

`PUT moderation/revievs/g9749r45-4h00-8b3e-59ynd87942v HTTP/1.1 HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
  	"score": 4,
	"review": "Товар понравился, но быстро испортился",
}
```

`GET moderation/revievs/g9749r45-4h00-8b3e-59ynd87942v`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для зарегистрированного покупателя; PUT, PATCH, DELETE - для модератора, администратора;  - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
  	"revievID": "g9749r45-4h00-8b3e-59ynd87942v",
	"created_by": "h6582x95-4052-4u5t-8432-41fef90045b",
	"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"sellerID": "y5698e95-2r10-6f4o-3471-52hgf654325v",
	"score": 4,
	"review": "Товар понравился, но быстро испортился",
}
```
Запрос доступен для ролей: зарегистрированный покупатель.


### 14. Публикация отзыва о товаре после модерации

`POST /revievs HTTP/1.1 ` <br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 690`<br>
`Content-Type: application/json; charset=utf-8`<br>

```json
{
  	"created_by": "h6582x95-4052-4u5t-8432-41fef90045b",
	"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"sellerID": "y5698e95-2r10-6f4o-3471-52hgf654325v",
	"score": 4,
	"review": "Товар понравился, но быстро испортился",
}
```
</br>
</br>

`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH, DELETE - для модератора, администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

```json
{
  	"revievID": "g9749r45-4h00-8b3e-59ynd87942v",
	"created_by": "h6582x95-4052-4u5t-8432-41fef90045b",
	"goodID": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"sellerID": "y5698e95-2r10-6f4o-3471-52hgf654325v",
	"score": 4,
	"review": "Товар понравился, но быстро испортился",
}
```
Запрос доступен для ролей: модератор, администратор.


### 15. Удаление отзыва о товаре 

`DELETE /revievs/g9749r45-4h00-8b3e-59ynd87942v`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 200 OK`<br>

`GET /revievs/g9749r45-4h00-8b3e-59ynd87942v`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 204 No Content`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH, DELETE - для модератора, администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

Запрос доступен для ролей: зарегистрированный покупатель, модератор, администратор.


### 16. Добавление товара в интернет-магазин (на модерацию)

`POST /moderation/goods HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 204`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
   	"goodName": "Творог 5% 200гр.",
   	"description": "Творог рассыпчатый 5% 200гр.",
	"group": "Молочные продукты",
	"cost": "79",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "9",
	"certificate": "",
	"createdAt": "2022-06-23T00:24:23.384413Z",
	"updatedAt": "2022-06-23T00:24:23.385413Z"
}
```
</br>
</br>


`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS, PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для модератора, администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

```json
{
	"goodId": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"goodName": "Творог 5% 200гр.",
	"description": "Творог рассыпчатый 5% 200гр.",
	"group": "Молочные продукты",
	"cost": "79",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "9",
	"certificate": "",
	"createdAt": "2022-06-23T00:24:23.384413Z",
	"updatedAt": "2022-06-23T00:24:23.385413Z"
}
```
Запрос доступен для ролей: зарегистрированный продавец.


### 17. Редактирование товара в интернет-магазине 
`PUT /moderation/goods/77efa7c2-c082-4025-a8b9-aba8a3a49c39`<br>
`Host: 127.0.0.1:8000`<br>
```json
{
	"cost": "99"`<br>
}
```

`GET /moderation/goods/77efa7c2-c082-4025-a8b9-aba8a3a49c39`<br>
`HTTP 200 OK`<br>
`Allow: [GET, HEAD, OPTIONS - для анонимного пользователя, зарегистрированного покупателя; PUT, PATCH - для зарегистрированного продавца, администратора; DELETE - для администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>
```json
{
	"goodId": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"goodName": "Творог 5% 200гр.",
	"description": "Творог рассыпчатый 5% 200гр.",
	"group": "Молочные продукты",
	"cost": "99",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "9",
	"certificate": "",
	"createdAt": "2022-06-23T00:24:23.384413Z",
	"updatedAt": "2022-06-23T00:24:23.385413Z"
}
```
Запрос доступен для ролей: модератор, администратор.

### 18. Добавление товара в интернет-магазин (после модерации)
`POST /goods HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 204`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
	"goodName": "Творог 5% 200гр.",
 	"description": "Творог рассыпчатый 5% 200гр.",
	"group": "Молочные продукты",
	"cost": "79",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "9",
	"createdAt": "2022-06-23T00:24:23.384413Z",
	"updatedAt": "2022-06-23T00:24:23.385413Z"
}
```
</br>
</br>

`HTTP 201 Created`<br>
`Allow: [GET, HEAD, OPTIONS, PUT, PATCH - для зарегистрированного продавца, модератора, администратора; DELETE - для модератора, администратора]`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

```json
{
	"goodId": "f7462e95-4f00-4e5a-8432-41fef909805c",
	"goodName": "Творог 5% 200гр.",
	"description": "Творог рассыпчатый 5% 200гр.",
	"group": "Молочные продукты",
	"cost": "79",
	"sellerName": "Молочное море",
	"status": "В наличии",
	"remainingNumber": "9",
	"createdAt": "2022-06-23T00:24:23.384413Z",
	"updatedAt": "2022-06-23T00:24:23.385413Z"
}
```

### 19. Удаление товара из интернет-магазина 

`DELETE /goods/77efa7c2-c082-4025-a8b9-aba8a3a49c39`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 200 OK`<br>

`GET /goods/77efa7c2-c082-4025-a8b9-aba8a3a49c39`<br>
`Host: 127.0.0.1:8000`<br>
`HTTP 204 No Content`<br>
`Allow: GET, PUT, PATCH, DELETE, HEAD, OPTIONS`<br>
`Content-Type: application/json`<br>
`Vary: Accept`<br>

Запрос доступен для ролей: администратор.

### 20. Создание профиля 

`POST http://127.0.0.1:8000/admin/auth/user/3/change/ HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 101`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
	"username": "Seller",
	"password1": "1234567890Seller",
	"password2": "1234567890Seller",	
	_continue: Save and continue editing
}
```

`HTTP/1.1 302 Found`<br>
`Date: Thu, 23 Jun 2022 01:05:18 GMT`<br>
`Server: WSGIServer/0.2 CPython/3.10.4`<br>
`Content-Type: text/html; charset=utf-8`<br>
`Location: /admin/auth/user/3/change/`<br>

<br>

`POST http://127.0.0.1:8000/admin/auth/user/3/change/ HTTP/1.1`<br>
`Host: 127.0.0.1:8000`<br>
`Content-Length: 101`<br>
`Content-Type: application/json; charset=utf-8`<br>
```json
{
	"username": "Seller",
	"first_name": "Молочное море",
	"last_name": ,
	"email": "molmore@nomail.ru",
	"is_active": "on",
	"is_staff": "on",
	"user_permissions": 4,
	"user_permissions": 12,
	"user_permissions": 8,
	"user_permissions": 16,
	"user_permissions": 20,
	"user_permissions": 29,
	"user_permissions": 30,
	"user_permissions": 32,
	"user_permissions": 24,
	"last_login_0": ,
	"last_login_1": ,
	"date_joined_0": 2022-06-23,
	"date_joined_1": 01:05:18,
	"initial-date_joined_0": 2022-06-23,
	"initial-date_joined_"1: 01:05:18,
	_save: Save
}
```
<br>

`HTTP/1.1 302 Found`<br>
`Date: Thu, 23 Jun 2022 01:11:49 GMT`<br>
`Server: WSGIServer/0.2 CPython/3.10.4`<br>
`Content-Type: text/html; charset=utf-8`<br>
`Location: /admin/auth/user/`<br>

<br>
<br>
Запрос доступен для ролей: анонимный пользователь, зарегистрированный покупатель, зарегистрированный продавец, администратор.

### 21. Редактирование профиля 

`POST /admin/auth/user/2/change/ HTTP/1.1`<br>
`Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9`<br>
`Accept-Encoding: gzip, deflate, br`<br>
`Accept-Language: ru-RU,ru;q=0.9,en-US;q=0.8,en;q=0.7`<br>
`Cache-Control: max-age=0`<br>
`Connection: keep-alive`<br>
`Content-Length: 548`<br>

```json
{
	"username": "Authorized_user",
	"first_name": "Иван",
	"last_name": "Иванов",
	"email": "iva@nomemail.ru",
	"is_active": "on",
	"user_permissions": 4,
	"user_permissions": 12,
	"user_permissions": 8,
	"user_permissions": 16,
	"user_permissions": 20,
	"user_permissions": 32,
	"user_permissions": 24,
	"last_login_0": 2022-06-22,
	"last_login_1": 12:03:13,
	"date_joined_0": 2022-06-22,
	"date_joined_1": 11:56:42,
	"initial-date_joined_0": 2022-06-22,
	"initial-date_joined_1": 11:56:42,
	_save: Save
}
```
<br>

`HTTP/1.1 302 Found`<br>
`Date: Thu, 23 Jun 2022 02:09:40 GMT`<br>
`Server: WSGIServer/0.2 CPython/3.10.4`<br>
`Content-Type: text/html; charset=utf-8`<br>
`Location: /admin/auth/user/`<br>

Запрос доступен для ролей: анонимный пользователь, зарегистрированный покупатель, зарегистрированный продавец, администратор.

### 22. Удаление профиля 

`POST /admin/auth/user/3/delete/ HTTP/1.1`<br>
`Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9`<br>
`Accept-Encoding: gzip, deflate, br`<br>
`Host: 127.0.0.1:8000`<br>
`Origin: http://127.0.0.1:8000`<br>
`Referer: http://127.0.0.1:8000/admin/auth/user/3/delete/`<br>
<br>

`HTTP/1.1 302 Found`<br>
`Date: Thu, 23 Jun 2022 02:01:44 GMT`<br>
`Server: WSGIServer/0.2 CPython/3.10.4`<br>
`Content-Type: text/html; charset=utf-8`<br>
`Location: /admin/auth/user/`<br>
<br>
<br>

`GET /admin/auth/user/ HTTP/1.1`
`Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9`
`Accept-Encoding: gzip, deflate, br`

<br>

`HTTP/1.1 200 OK`
`Date: Thu, 23 Jun 2022 02:01:44 GMT`
`Server: WSGIServer/0.2 CPython/3.10.4`
`Content-Type: text/html; charset=utf-8`

Запрос доступен для ролей: администратор.