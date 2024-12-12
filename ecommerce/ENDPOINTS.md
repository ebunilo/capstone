# E-commerce API Endpoints

## **User Management**

### 1. Register a User

**Endpoint**: `/api/users/register`

- **Method**: `POST`
- **Request Body** (JSON):

  ```json
  {
      "username": "string",
      "email": "string",
      "password": "string",
      "first_name": "string",
      "last_name": "string",
      "phone_number": "string"
  }
  ```

- **Response**:
  - **201 Created**:

    ```json
    {
        "id": "int",
        "username": "string",
        "email": "string",
        "created_at": "datetime"
    }
    ```

  - **400 Bad Request**:

    ```json
    { "error": "string" }
    ```

### 2. Login

**Endpoint**: `/api/users/login`

- **Method**: `POST`
- **Request Body** (JSON):

  ```json
  {
      "email": "string",
      "password": "string"
  }
  ```

- **Response**:
  - **200 OK**:

    ```json
    {
        "token": "string",
        "user": {
            "id": "int",
            "username": "string",
            "role": "string"
        }
    }
    ```

  - **401 Unauthorized**:

    ```json
    { "error": "Invalid credentials" }
    ```

### 3. Get User Profile

**Endpoint**: `/api/users/profile`

- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Response**:
  - **200 OK**:

    ```json
    {
        "id": "int",
        "username": "string",
        "email": "string",
        "first_name": "string",
        "last_name": "string",
        "phone_number": "string"
    }
    ```

  - **401 Unauthorized**:

    ```json
    { "error": "Authentication required" }
    ```

---

## **Product Management**

### 4. List Products

**Endpoint**: `/api/products`

- **Method**: `GET`
- **Query Parameters**:
  - `category` (optional): `int`
  - `search` (optional): `string`
  - `min_price` (optional): `decimal`
  - `max_price` (optional): `decimal`
- **Response**:
  - **200 OK**:
  
    ```json
    [
        {
            "id": "int",
            "name": "string",
            "price": "decimal",
            "stock": "int",
            "vendor": "string",
            "category": "string"
        }
    ]
    ```

### 5. Get Product Details

**Endpoint**: `/api/products/{id}`

- **Method**: `GET`
- **Response**:
  - **200 OK**:

    ```json
    {
        "id": "int",
        "name": "string",
        "description": "string",
        "price": "decimal",
        "discount_price": "decimal",
        "stock": "int",
        "vendor": {
            "id": "int",
            "name": "string"
        },
        "category": {
            "id": "int",
            "name": "string"
        }
    }
    ```

  - **404 Not Found**:

    ```json
    { "error": "Product not found" }
    ```

---

## **Order Management**

### 6. Create an Order

**Endpoint**: `/api/orders`

- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Request Body** (JSON):

  ```json
  {
      "items": [
          {
              "product_id": "int",
              "quantity": "int"
          }
      ],
      "shipping_address_id": "int"
  }
  ```

- **Response**:
  - **201 Created**:

    ```json
    {
        "order_id": "int",
        "total_price": "decimal",
        "status": "string"
    }
    ```

  - **400 Bad Request**:

    ```json
    { "error": "string" }
    ```

### 7. Get User Orders

**Endpoint**: `/api/orders`

- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Response**:
  - **200 OK**:

    ```json
    [
        {
            "order_id": "int",
            "total_price": "decimal",
            "status": "string",
            "created_at": "datetime"
        }
    ]
    ```

---

## **Cart Management**

### 8. Add to Cart

**Endpoint**: `/api/cart`

- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Request Body** (JSON):

  ```json
  {
      "product_id": "int",
      "quantity": "int"
  }
  ```

- **Response**:
  - **200 OK**:

    ```json
    { "message": "Item added to cart" }
    ```

  - **400 Bad Request**:

    ```json
    { "error": "string" }
    ```

### 9. View Cart

**Endpoint**: `/api/cart`

- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Response**:
  - **200 OK**:

    ```json
    [
        {
            "product_id": "int",
            "name": "string",
            "quantity": "int",
            "price": "decimal"
        }
    ]
    ```

---

## **Payment**

### 10. Process Payment

**Endpoint**: `/api/payments`

- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Request Body** (JSON):

  ```json
  {
      "order_id": "int",
      "payment_method": "string"
  }
  ```

- **Response**:
  - **200 OK**:

    ```json
    { "message": "Payment successful" }
    ```

  - **400 Bad Request**:

    ```json
    { "error": "string" }
    ```

