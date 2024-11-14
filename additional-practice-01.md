**MySQL Table Setup:**

```sql
CREATE TABLE satays (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    meatType VARCHAR(50) NOT NULL,
    spicyLevel INT CHECK(spicyLevel BETWEEN 0 AND 5),
    price DECIMAL(10, 2) NOT NULL
);

-- Insert initial data into the satays table
INSERT INTO satays (name, meatType, spicyLevel, price) VALUES
('Beef Satay', 'Beef', 2, 10.00),
('Chicken Satay', 'Chicken', 3, 8.00);
```

---

**Question 1: Add a new satay item**

- **HTTP METHOD + URI**: POST /satays

- **Request Body Example**:
  ```json
  {
    "name": "Lamb Satay",
    "meatType": "Lamb",
    "spicyLevel": 3,
    "price": 12.0
  }
  ```

- **Response Body Examples**:
  - **201 Created**:
    ```json
    {
      "message": "Satay created successfully",
      "id": "s003",
      "satay": {
        "name": "Lamb Satay",
        "meatType": "Lamb",
        "spicyLevel": 3,
        "price": 12.0
      }
    }
    ```
  - **400 Bad Request**:
    ```json
    {
      "error": "Invalid input: price must be a positive number"
    }
    ```

---

**Question 2: Get details of a specific satay item**

- **HTTP METHOD + URI**: GET /satays/:id

- **Response Body Examples**:
  - **200 OK**:
    ```json
    {
      "id": 1,
      "name": "Beef Satay",
      "meatType": "Beef",
      "spicyLevel": 2,
      "price": 10.0
    }
    ```
  - **404 Not Found**:
    ```json
    {
      "error": "Satay item with ID s001 not found"
    }
    ```

---

**Question 3: List all satay items**

- **HTTP METHOD + URI**: GET /satays

- **Response Body Examples**:
  - **200 OK**:
    ```json
    [
      {
        "id": 1,
        "name": "Beef Satay",
        "meatType": "Beef",
        "spicyLevel": 2,
        "price": 10.0
      },
      {
        "id": 2,
        "name": "Chicken Satay",
        "meatType": "Chicken",
        "spicyLevel": 3,
        "price": 8.0
      }
    ]
    ```
  - **204 No Content**:
    ```json
    {
      "message": "No satay items found"
    }
    ```