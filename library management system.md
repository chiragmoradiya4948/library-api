# Library management system API #

This API allows you to reserve/order a book from library.

## Opearion configured on end point ##

1) Status of API end
2) List of books available in library
3) Get inforamtion about single book
4) Submit an order
5) Get all orders
6) Get an order with order ID
7) Update an order
8) Delete an order
9) API Authentication


## Implementation on lab ##

### 1) Status ###

GET `/status`

Returns the status of the API.

#### hands on : Go to EC2 > Auto scaling group, Enter name of ASG & Click on 'Create a launch template'
####
<img src="/Images/Rest-API 1.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

### 2) List of books available in library ###

GET `/books`

Returns a list of books.

Optional query parameters:

- type: fiction or non-fiction
- limit: a number between 1 and 20.


### 3) Get a single book detail ###

GET `/books/:bookId`

Retrieve detailed information about a book.


### 4) Submit an order ###

POST `/orders`

Allows you to submit a new order. Requires authentication.

The request body needs to be in JSON format and include the following properties:

 - `bookId` - Integer - Required
 - `customerName` - String - Required

Example
```
POST /orders/
Authorization: Bearer <YOUR TOKEN>

{
  "bookId": 1,
  "customerName": "John"
}
```

The response body will contain the order Id.

### 5) Get all orders ###

GET `/orders`

Allows you to view all orders. Requires authentication.

### 6) Get an order ###

GET `/orders/:orderId`

Allows you to view an existing order. Requires authentication.

### 7) Update an order ###

PATCH `/orders/:orderId`

Update an existing order. Requires authentication.

The request body needs to be in JSON format and allows you to update the following properties:

 - `customerName` - String

 Example
```
PATCH /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>

{
  "customerName": "John"
}
```

### 8) Delete an order ###

DELETE `/orders/:orderId`

Delete an existing order. Requires authentication.

The request body needs to be empty.

 Example
```
DELETE /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>
```

## 9) API Authentication ##

To submit or view an order, you need to register your API client.

POST `/api-clients/`

The request body needs to be in JSON format and include the following properties:

 - `clientName` - String
 - `clientEmail` - String

 Example

 ```
 {
    "clientName": "Ram",
    "clientEmail": "demo@example.com"
}
 ```

The response body will contain the access token. The access token is valid for 7 days.

**Possible errors**

Status code 409 - "API client already registered." Try changing the values for `clientEmail` and `clientName` to something else.

### End of Library management system API page ###
#### Author by Chirag Moradiya #### 
