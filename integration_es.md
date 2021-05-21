
# Documentacion Basica para Intregacion
 
 La idea de este documento, es tener una base para iniciar el proceso de integracion con perfit. A continuacion se listan los elementos basicos para una integracion funcional, pero toda informacion que se pueda agregar podra ser usada para mejorar la integracion.

# Webhooks

Perfit proveera una url a la cual se debe enviar mediante un Request  de tipo **POST**  la informacion correspondiente a cada topic.

El Request tiene que contener en el body un request de tipo  application/json, y debe tener la siguiente estructura

```javascript
{
	"topic": "",
	"data": {
	}
}
```

## Topics

* Product
	*  product-updated  
	*  product-created
	*  product-deleted
*  Customer
	* customer-created
	* customer-updated  
* Order
	*  order-created
	*   order-paid
	*  order-packed 
	* order-fulfilled
    
* Otros    
	*   newsletter.subscribed
	*   cart.created

# Endpoints

Desde nuestra aplicacion debemos poder obtener informacion para utilizar en nuestros automations, por lo que necesitamos los siguientes endpoints.

El metodo que usamos es **GET {urlBase}/{endpoint}**
 
#### Orders
*  /orders/{orderId}
```javascript
{
	"topic": "",
	"data": {
		"id": "",
		...
	}
}
```
* /orders/{orderId}/products
	
```javascript
{
	"topic": "",
	"data":  [
		{
			"id": ""
			...
		},
		...
	]
}
```
*   /cart/{cartId} (en caso de que lo manejen por separado el carrito de la order)
   
#### Productos   
*   /products
	* ?filters.type=most_selling (filtro para mas vendidos)
	* ?filters.type=new (filtro para mas recientes)

```javascript
{
	"topic": "",
	"data":  [
		{
			"id": ""
			...
		},
		...
	]
}
```

#### Customers
    
*   /customers
*   /customers/{customerId}
    
    Dependendiendo del flujo de instalacion, tambien vamos a necesitar un endpoint el cual nos permita configurar la url destindo de los webhooks.
    
*   POST /configwebhook

## Ordenes

*   /orders/{orderId}
```javascript
{
	"data": {
		"id": "1234",
		...
	}
}
```
*   /orders/{orderId}/products
```javascript
{
	"data": [
		{
		"id": "1234",
		...
		}
	]
}
```
## Entidades


### Producto:

```javascript
{
	"id": "",
	"price": "10.23",
	"image": "",
	"link": "",
	"title": "",

	// optativos:
	"discount_price": "",
	"category": "",
	"attributes" : {
	},
	"sku": ""
}
```

### Orden

```javascript
{
	"id": "",
	"total": "10.23",
	"products": [ 
		{
			"id": "",
			 ...
		 },
		 ....
	],
	"customer_id": "",
	"email": "",

	// optativos:
	"address": "",
	"paymethod": "",
	"attributes" : {
	},
	"shipping_method": ""
}
```
