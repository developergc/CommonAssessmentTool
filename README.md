This will contain the model used for the project that based on the input information will give the social workers the clients baseline level of success and what their success will be after certain interventions.

The model works off of dummy data of several combinations of clients alongside the interventions chosen for them as well as their success rate at finding a job afterward. The model will be updated by the case workers by inputing new data for clients with their updated outcome information, and it can be updated on a daily, weekly, or monthly basis.

This also has an API file to interact with the front end, and logic in order to process the interventions coming from the front end. This includes functions to clean data, create a matrix of all possible combinations in order to get the ones with the highest increase of success, and output the results in a way the front end can interact with.

# Documentation

### **PUT /clients/{client_id}**

#### **Description**
Updates specific fields of an existing client record.

---

### **Path Parameters**

| Parameter   | Type     | Description                            |
|-------------|----------|----------------------------------------|
| `client_id` | `string` | The unique ID of the client to update. |

---

### **Request Body**

The fields to be updated must be passed as a JSON object. Unspecified fields will remain unchanged.

| Field                          | Type    | Example                | Description                             |
|--------------------------------|---------|------------------------|-----------------------------------------|
| `age`                          | integer | `32`                  | Age of the client.                     |
| `gender`                       | string  | `"Male"`              | Gender of the client.                  |
| `work_experience`              | integer | `7`                   | Years of total work experience.        |
| `canada_workex`                | integer | `3`                   | Years of work experience in Canada.    |
| `dep_num`                      | integer | `1`                   | Number of dependents.                  |
| `canada_born`                  | string  | `"No"`                | Whether the client was born in Canada. |
| `citizen_status`               | string  | `"Citizen"`           | Citizenship status of the client.      |
| `level_of_schooling`           | string  | `"Master's degree"`   | Highest level of education completed.  |
| `fluent_english`               | string  | `"Yes"`               | Whether the client is fluent in English. |
| `reading_english_scale`        | integer | `10`                  | English reading skill level (1-10).    |
| `speaking_english_scale`       | integer | `10`                  | English speaking skill level (1-10).   |
| `writing_english_scale`        | integer | `10`                  | English writing skill level (1-10).    |
| `numeracy_scale`               | integer | `10`                  | Numeracy skill level (1-10).           |
| `computer_scale`               | integer | `10`                  | Computer skill level (1-10).           |
| `transportation_bool`          | string  | `"No"`                | Whether transportation support is needed. |
| `caregiver_bool`               | string  | `"No"`                | Whether the client is a primary caregiver. |
| `housing`                      | string  | `"Homeowner"`         | Housing status of the client.          |
| `income_source`                | string  | `"Employment"`        | Source of income.                      |
| `felony_bool`                  | string  | `"No"`                | Whether the client has a felony record. |
| `attending_school`             | string  | `"No"`                | Whether the client is currently a student. |
| `currently_employed`           | string  | `"Yes"`               | Employment status of the client.       |
| `substance_use`                | string  | `"No"`                | Whether the client has a substance use disorder. |
| `time_unemployed`              | integer | `0`                   | Time unemployed in years.              |
| `need_mental_health_support_bool` | string | `"No"`               | Whether the client needs mental health support. |

---

### **Request Example**

**URL**:
PUT /clients/61


**Request Body**:
```json
{
    "age": 32,
    "work_experience": 7,
    "canada_workex": 3,
    "level_of_schooling": "Master's degree",
    "fluent_english": "Yes",
    "currently_employed": "Yes",
    "housing": "Homeowner"
}
```

**Responses**
**200 OK**

The client information was successfully updated.

**Response Example:**
```json
{
    "success": true,
    "message": "Client 61 successfully updated",
    "client_id": "61"
}
```
**404 Not Found**

No client with the specified client_id exists.

**Response Example:**
```json
{
    "detail": "Client with ID 61 not found."
}
```
**400 Bad Request**

The client_id is invalid or improperly formatted.

**Response Example:**
```json
{
    "detail": "Invalid client_id format."
}
```
**500 Internal Server Error**

An unexpected error occurred on the server.

**Response Example:**
```json
{
    "detail": "An error message describing the issue."
}
```

## DELETE `/clients/{client_id}`

### Description
Deletes a client with the specified `client_id` from the database.

### Path Parameters

| Parameter   | Type     | Description                            |
|-------------|----------|----------------------------------------|
| `client_id` | `string` | The unique ID of the client to delete. |

### Request Example

**URL:**

```
DELETE /clients/1
```
## Responses

**200 OK**

The client was successfully deleted.

**Response Example:**
```json
{
    "success": true,
    "message": "Client 1 successfully deleted",
    "client_id": "1"
}
```

**404 Not Found**

No client with the specified `client_id` exists.

**Response Example:**
```json
{
    "detail": "Client with ID 1 not found."
}
```

**500 Internal Server Error**

An unexpected error occurred on the server.

**Response Example:**
```json
{
    "detail": "An error message describing the issue."
}
```

### Notes

This endpoint requires the `client_id` to be a valid **integer string**.


### **GET /clients/{client_id}**

#### **Description**
Retrieves information for a client with the specified `client_id` from the database.

---

### **Path Parameters**

| Parameter  | Type   | Description                           |
|------------|--------|---------------------------------------|
| `client_id` | string | The unique ID of the client to retrieve. |

---

### **Request Example**

**URL**:

```http
GET /clients/123

Responses
200 OK
The client information was successfully retrieved.

Response Example:
{
    "success": true,
    "data": {
        "name": "John Doe",
        "email": "john@example.com"
    }
}

404 Not Found
No client with the specified client_id exists.

Response Example:
{
    "detail": "Client with ID 123 not found."
}

400 Bad Request
The client_id is invalid or improperly formatted.

Response Example:
{
    "detail": "Invalid client_id format."
}


500 Internal Server Error
An unexpected error occurred on the server.

Response Example:
{
    "detail": "An error message describing the issue."
}

Notes
The client_id must be a valid string that matches the expected format in the database.
Ensure the client_id exists before making the request to avoid a 404 error.
Copy code
