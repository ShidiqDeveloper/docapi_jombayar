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
  "message": "string",
  "data": [
    "email": [
      "Email is required"
    ],
    "password": [
      "Password is required"
    ]
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
  "data": {
    "id": "string" (id dari users),
    "email": "string",
  }
}
```

# Check token reset password
URL : POST <base_url>/api/check-token-reset-password

Payload 
- (id dari users)
- otp

```
{
  "status": true,
  "status_code": 200,
  "message": "Token is valid!",
  "data": {
    "id": "string" (id dari users),
    "email": "string",
  }
}
```


# Reset Password
URL : POST <base_url>/api/reset-password

Payload:
- id (id dari users)
- password
- password_confirmation
- otp

```
{
  "status": true,
  "status_code": 200,
  "message": "Success reset password!",
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
  "data": {
    "hash_uid": "string",
    "email": "string"
  }
}
```

# Send OTP Register
URL : <base_url>/api/check-token-register

Payload :
- id (id dari users)
- token

Response
```
{
  "status": true,
  "status_code": 200,
  "message": "Success verify your account",
  "data": []
}
```


# Get card related
URL : GET <base_url>/api/cards
Header : 
- Authorization : Bearer {token}

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
- Authorization : Bearer {token}

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
- Authorization : Bearer {token}

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

# Topup API
URL : POST <base_url>/api/student/{hash_uid}/topup

Headers :
- Authorization : Bearer {token}

Payload
- amount (decimal)

Responses
```
{
  "status": true,
  "status_code": 200,
  "message": "Success!",
  "data": {
    "transaction_number": "string" 
  }
}
```

# Check Status Payment Topup API
URL : GET <base_url>/api/topup/{transaction_id}

Headers :
- Authorization : Bearer {token}

Responses
```
{
  "status": true,
  "status_code": 200,
  "message": "Success!",
  "data": {
    "transaction_id": "string",
    "transaction_time": "integer",
    "transaction_amount": "decimal",
    "grant_total": "decimal",
    "transaction_status": {
      "id": "integer",
      "transaction_status": "string"
    },
    "student": {
      "hash_uid": "string",
      "student_name": "string",
      "student_number_id": "string"
    },
    "payment_gateway_attribute": {
      "payment_url": "string"
    }
  }
}
```

> Transaction Status ID
>
> 1 = Not Paid
> 2 = Paid
> 3 = Cancel
> 
> Transaction time using timestamp format

# Get Profile
URL : GET <base_url>/api/profile

Headers : 
- Authorization : Bearer {token}

Response
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": {
    "parent_name": "string",
    "parent_email": "string",
    "parent_phone": "string",
    "parent_address": "string
  }
}
```

# Update Profile
URL : PUT <base_url>/api/profile

Headers : 
- Authorization : Bearer {token}

Payload
- parent_name (required, string)
- parent_phone (required, string)
- parent_address (required, string)

Response
```
{
  "status": true,
  "status_code": 200,
  "message": "Success updated profile!",
  "data": []
}
```

# Receive transaction
URL : POST base_url/api/pos/transactions

Header: 
- Api-key: string
- Authorization: base64_encode(merchant_code)

Payload : 
```
{
  "transaction_amount": "string",
  "transaction_discount": "string",
  "items": [
    {
      "name": "string",
      "qty": "string",
      "price": "string"
    },
    {
      "name": "string",
      "qty": "string",
      "price": "string"
    },
  ]
}
```
Response Success
```
{
  "status": true,
  "status_code": 200,
  "message": "Success store transactions!",
  "data": {
    "transaction_hash_id" => "string",
    "transaction_number" => "string"
  }
}
```
Response Fails
```
{
  "status": true,
  "status_code": 403,
  "message": "Insufficient student balance!",
  "data": []
}
```

# Get balance merchants
URL : GET base_url/api/pos/merchants/balance

Header :
- Api-key: string
- Authorization: base64_encode(merchand_code)

Response : 
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": {
    "merchant_balance": "string"
  }
}
```

# Get list withdraw
URL : GET base_url/api/pos/merchants/withdraws

Header :
- Api-key: string
- Authorization: base64_encode(merchand_code)

Response : 
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": [
    {
      "withdraw_uid": "string",
      "withdraw_number": "string",
      "withdraw_time": "string",
      "withdraw_amount": "string",
      "status": {
        "id": "string",
        "merchant_withdraw_status": "string"
      },
    }
  ]
}
```

# Request withdraw
URL: POST base_url/api/pos/merchants/balance

Header :
- Api-key: string
- Authorization: base64_encode(merchand_code)

Payload : 
- amount: "string"

Response : 
```
{
  "status": true,
  "status_code": 200,
  "message": "Found!",
  "data": {
    "withdraw_hash_uid": "string",
    "withdraw_number": "string",
    "withdraw_time": "string",
    "withdraw_amount": "string",
    "status": {
      "id": "string",
      "merchant_withdraw_status": "string"
    },
  }
}
```