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

#### In GET method, we have passed end point's URL and /status which will give status of end point. Here got Status: 200 OK means everything is working fine.
####
<img src="/Images/Rest-API 3.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

- Now you can see in end point address's mapped with {{baseURL}} which is set as variable.

####
<img src="/Images/Rest-API 4.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

### 2) List of books available in library ###

GET `/books`

Returns a list of books.

Optional query parameters:

- type: fiction or non-fiction
- limit: a number between 1 and 20.

#### Here we have filtered books based on 'type' which is passed on parameter and can see the result.
####
<img src="/Images/Rest-API 1.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

#### If you entered type value which is incorrect, can get output as per below.
####
<img src="/Images/Rest-API 6.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

####
<img src="/Images/Rest-API 7.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

### 3) Get a single book detail ###

GET `/books/:bookId`

Retrieve detailed information about a book.

#### You can also get single book details as per below.

####
<img src="/Images/Rest-API 2.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

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
#### Here We have ordered book which having bookId = 1 and can see output as true, however you need to have authentication as per step 9.
#### Once we get accessToken from step 9, we can pass as bearer token and order a book.

####
<img src="/Images/Rest-API 9.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

The response body will contain the order Id.

### 5) Get all orders ###

GET `/orders`

Allows you to view all orders. Requires authentication.

#### You can get all orders by giving orderId as parameter along with access token.

####
<img src="/Images/Rest-API 9.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

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
#### You can see new name as john jacobs and we have got status 204 which means request is successfully completed.

####
<img src="/Images/Rest-API 11.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

####
<img src="/Images/Rest-API 12.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####


### 8) Delete an order ###

DELETE `/orders/:orderId`

Delete an existing order. Requires authentication.

The request body needs to be empty.

 Example
```
DELETE /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>
```
#### You can see DELETE method on header and given which order we need to delete. And we you get list of available books can see ID=1 book is available

####
<img src="/Images/Rest-API 13.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####


####
<img src="/Images/Rest-API 5.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

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

#### Here I have registered  myself by giving ClientName and clientEmail and got accessToken.

####
<img src="/Images/Rest-API 8.png" width="auto" height="auto" style="border:5px double black;"
     alt="REST API"
     style="float: left; margin-right: 6px;" />
####

**Possible errors**

Status code 409 - "API client already registered." Try changing the values for `clientEmail` and `clientName` to something else.

### End of Library management system API page ###
#### Author by Chirag Moradiya #### 
