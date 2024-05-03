# Error Response
Error code 500
```
{
  "status": false,
  "status_code": 500,
  "message": "Server error!",
  "data": []
}
```

Error Validation
Header response code 422
```
{
  "email": [
    "Email is required"
  ],
  "password": [
    "Password is required"
  ]
}
```

# Login
URL : POST <base_url>/api/login
Payload : 
- Email
- Password

Response 
```
{
  "status": true,
  "status_code": 200,
  "message": "Success Login!",
  "data": {
    "id": "",
    "name": "",
    "token": ""
  }
}
```

# Forgot Password
URL : POST <base_url>/api/forgot-password

Payload : 
- Email

Response
```
{
  "status": true,
  "status_code": 200,
  "message": "Success send link OTP!",
  "data": []
}
```

# Register
URL : POST <base_url>/api/register

Payload : 
- first_name
- last_name
- email
- phone
- password
- password_confirmation
    
    
Response 
```
{
  "status": true,
  "status_code": 200,
  "message": "Success reset register! Please check your email for verify your account!",
  "data": []
}
```

# Get card related
URL : GET <base_url>/api/cards
Header : 
- Authorization : Bearer <token>

Response
```
{
  "status": false,
  "status_code": 500,
  "message": "Found!",
  "data": [
    {
      "hash_uid": "string",
      "student_name": "string",
      "student_number_id": "string",
      "student_balance": 0
    },
    {
      "hash_uid": "string",
      "student_name": "string",
      "student_number_id": "string",
      "student_balance": 0
    },
    {
      "hash_uid": "string",
      "student_name": "string",
      "student_number_id": "string",
      "student_balance": 0
    }
  ]
}
```

# Get Card
URL : GET <base_url>/api/cards/{hash_id / isi NFC Card}
Header : 
- Authorization : Bearer <token>

Response 
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": {
    "hash_uid": "string",
    "student_name": "string",
    "student_number_id": "string",
    "student_balance": 0
  }
}
```

# Get transactions
URL : GET <bsae_url>/api/card/{hash_uid}/transctions?iimit=10

Query String
- limit (Opsional, Default 10)

Header
- Authorization : Bearer <token>

Responses
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": [
    {
      "hash_uid": "string",
      "transaction_time": "integer timestamp",
      "grand_total": "integer",
      "merchant": {
        "merchant_name": "string"
      }
    },
    {
      "hash_uid": "string",
      "transaction_time": "integer timestamp",
      "grand_total": "integer",
      "merchant": {
        "merchant_name": "string"
      }
    },
    {
      "hash_uid": "string",
      "transaction_time": "integer timestamp",
      "grand_total": "integer",
      "merchant": {
        "merchant_name": "string"
      }
    },
  ]
}
```