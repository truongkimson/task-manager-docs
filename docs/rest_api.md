# REST API

## Task Resource

The Task Resource is exposed with `{base_url}:8080/api/v1/task`. This resource provide endpoints to carry out CRUD actions on Task instances.
Variable `{base_url}` should be the address of the host on which the service is currently running. If you are running the application locally. `{base_url}` should be `http://localhost`

## Endpoints

### **1. Get all tasks**

#### URL

```
{base_url}:8080/api/v1/task/all
```

#### Method

<code><span style="color:green">GET</span></code>

### Parameters

None

### Example request

```
http://localhost:8080/api/v1/task/all
```

### Example response

CODE: <code><span style="color:green">200</span></code>

```json
[
    {
        "id": 1,
        "description": "See dentist B",
        "date": "2021-07-25",
        "overdue": false
    },
    {
        "id": 4,
        "description": "New task",
        "date": "2021-07-27",
        "overdue": false
    }
]
```

### **2. Create new task**

#### URL

```
{base_url}:8080/api/v1/task/create
```

#### Method

<code><span style="color:orange">POST</span></code>

### Parameters

Header

```
Content-Type: application/json
```

### Example request

```
http://localhost:8080/api/v1/task/create
```

Request body

```json
{
    "description": "calculate microchip",
    "date": "2021-07-21"
}
```

### Example response

CODE: <code><span style="color:green">201</span></code>

```json
{
    "id": 78,
    "description": "calculate microchip",
    "date": "2021-07-21",
    "overdue": false
}
```

CODE: <code><span style="color:blue">422</span></code>

```json
{
    "errors": [
        "date must be a date in the present or in the future",
        "description must not be blank"
    ]
}
```

### **3. Update existing task**

#### URL

```
{base_url}:8080/api/v1/task/update
```

#### Method

<code><span style="color:blue">PUT</span></code>

### Parameters

Header

```
Content-Type: application/json
```

### Example request

```
http://localhost:8080/api/v1/task/update
```

Request body

```json
{
    "id": 78,
    "description": "reboot bandwidth",
    "date": "2021-07-22"
}
```

### Example response

CODE: <code><span style="color:green">200</span></code>

```json
{
    "id": 78,
    "description": "reboot bandwidth",
    "date": "2021-07-22",
    "overdue": false
}
```

CODE: <code><span style="color:blue">422</span></code>

```json
{
    "errors": [
        "date must be a date in the present or in the future",
        "description must not be blank"
    ]
}
```

### **4. Delete existing task**

#### URL

```
{base_url}:8080/api/v1/{task_id}/delete
```

#### Method

<code><span style="color:red">DELETE</span></code>

### Parameters

`{task_id}`: id of the task to be deleted

Header

```
Content-Type: application/json
```

### Example request

```
http://localhost:8080/api/v1/task/78/delete
```

### Example response

CODE: <code><span style="color:green">200</span></code>

CODE: <code><span style="color:blue">404</span></code>
