# Telegram Dating Web App - Backend
# Project Overview

This repository contains the backend code for a Telegram Dating Web App. Built using Laravel, it provides essential functionalities such as user management, profiles, matches, and API endpoints for seamless interactions. Visit our [front-end repository](https://github.com/biruknova/telegramDating) for the complete dating experience.



## Project Setup Instructions

### Prerequisites

1. **Server Requirements**:
   - Ensure you have access to a web server or hosting environment with PHP installed.
   - Make sure your server meets the Laravel framework's [server requirements](https://laravel.com/docs/10.x/deployment#server-requirements).

2. **Composer**:
   - Install Composer, a PHP package manager, if you haven't already. You can download it from [Composer's official website](https://getcomposer.org/download/).

3. **Git**:
   - Install Git for version control. You can download it from [Git's official website](https://git-scm.com/downloads).

### Step 1: Clone the Repository

1. Open your terminal or command prompt.

2. Navigate to the directory where you want to store the project.

3. Clone the GitHub repository:
   ```bash
   git clone https://github.com/tesfaX/TelegramDating-Backend.git
### Step 2: Install Dependencies

1. **Navigate to the project directory:**

   ```bash
   cd TelegramDating-Backend
2. **Install PHP dependencies using Composer:**

   ```bash
   composer install
   ```
   
## Step 3: Telegram Bot Token and Payment Provider Setup

1. **Create a Telegram Bot Get Your Token:**
   - Go to [BotFather](https://t.me/BotFather) on Telegram.
   - Create a new bot using the `/newbot` command.
   - Follow the instructions to give your bot a name and a unique username (ending in "bot").
   - BotFather will provide you with a token in the format: `1234567890:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`.   
   - Copy the token generated by BotFather

2. **Get your PAYMENT_PROVIDER_TOKEN:**
   - List your bots using the `/mybots` command inside [BotFather](https://t.me/BotFather)
   - Select your bot and open "Payments" section
   - Select your preferred payment provider and follow the instruction given on the bot to get your payment token.

### Step 4: Configure Environment Variables

1. Create a copy of the `.env.example` file and name it `.env`:

   ```bash
   cp .env.example .env
2. Open the .env file using a text editor and update the following environment variables

    ```env
    TELEGRAM_BOT_TOKEN=your-telegram-bot-token
    TELEGRAM_MINI_APP_URL=your-mini-app-web-url
    PAYMENT_PROVIDER_TOKEN=your-payment-provider-token
    
    DB_DATABASE=your-database-name
    DB_USERNAME=your-database-username
    DB_PASSWORD=your-database-password
    ```
### Step 5: Generate Application Key
Generate a unique application key by running the following command:
```bash
php artisan key:generate
```

### Step 6: Migrate and Seed the Database
Run the following command to create and populate the database tables:
```bash
php artisan migrate
```


## API Endpoints

### User Login

**Endpoint:** `{{BASE_URL}}/api/login`

**HTTP Method:** POST

**Request:**

```http
POST {{BASE_URL}}/api/login HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "check_value": "your_check_value_here"
}

```

**Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "success": true,
  "user": {
    "id": 8,
    "name": "User Name",
    "tg_id": "123456789",
    "age": "30",
    "tg_username": "username123",
    "bio": "This is a sample bio.",
    "photos": [
      "https://example.com/photourl1",
      "https://example.com/photourl2"
    ],
    "has_telegram_premium": false,
    "is_pro_user": true,
    "user_type": "1",
    "status": "1",
    "gender_id": "1",
    "interested_in": "2",
    "gender": {
      "id": 1,
      "name": "Male"
    }
  },
  "token": "your_auth_token_here",
  "message": "Login successful"
}
```

### User Registration

**Endpoint:** `{{BASE_URL}}/api/register`

**HTTP Method:** POST

**Request:**

```json
POST {{BASE_URL}}/api/register HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "Account Name.",
  "gender_id": 1,
  "age": 24,
  "tg_data": "user=%7B%22id%22%3A534550713%2C%22first_name%22%3A%22%E2%80%8C%E2%80%User%20N.%22%2C%22last_name%22%3A%22%22%2C%22username%22%3A%22uskeyr%22%2C%22language_code%22%3A%22en%22%2C%22allows_write_to_pm%22%3Atrue%7D&chat_instance=75837123455566130038&chat_type=private&auth_date=1696926911&hash=f79181a31a95274ce6d04754f1cd9ac53dd08e6462dae1eacc100af41c36cc86"
}
```

**Response - 201 Created:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "success": true,
  "user": {
    "name": "John Doe",
    "age": 30,
    "gender_id": 1,
    "tg_id": 123456789,
    "tg_username": "johndoe123",
    "has_telegram_premium": false,
    "interested_in": 2,
    "user_type": 1,
    "status": 1,
    "is_pro_user": false,
    "photos": [
      "https://example.com/photo1.jpg",
      "https://example.com/photo2.jpg"
    ],
    "id": 123,
    "gender": {
      "id": 1,
      "name": "Male"
    }
  },
  "token": "your_auth_token_here",
  "message": "User registered successfully"
}
```

**Response - 409 Conflict:**

```http
HTTP/1.1 409 Conflict
Content-Type: application/json

{
  "success": false,
  "message": "User already exists"
}

```

### Update User Profile

**Endpoint:** `{{LOCAL_BASE_URL}}/api/profile`

**HTTP Method:** PATCH

**Request:**

```http
PATCH {{LOCAL_BASE_URL}}/api/profile HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer your_access_token_here

{
  "name": "John Doe",
  "bio": "A brief bio goes here.",
  "age": 30,
  "gender_id": 1,
  "interests": [1, 2]
}

```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```

### Get User Profile

**Endpoint:** `{{BASE_URL}}/api/profile`

**HTTP Method:** GET

**Request:**

```http
GET {{BASE_URL}}/api/profile HTTP/1.1
Host: api.example.com
Authorization: Bearer your_access_token_here
```

**Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "user": {
        "id": 11,
        "name": "John Doe",
        "tg_id": "123456789",
        "age": "30",
        "tg_username": "johndoe123",
        "bio": "A brief bio goes here.",
        "photos": [
            "https://example.com/photo1.jpg",
            "https://example.com/photo2.jpg"
        ],
        "has_telegram_premium": false,
        "is_pro_user": false,
        "user_type": "1",
        "status": "1",
        "interested_in": "2",
        "gender": {
            "id": 1,
            "name": "Male"
        }
    }
}
```

### Fetch Available Users

**Endpoint:** `{{BASE_URL}}/api/fetch-users?page=1`

**HTTP Method:** GET

**Request:**

```http
GET {{BASE_URL}}/api/fetch-users?page=1 HTTP/1.1
Host: api.example.com
Authorization: Bearer your_access_token_here
```

**Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "success": true,
  "users": [
    {
      "id": 3,
      "name": "User 1",
      "tg_id": "1234567890",
      "age": "25",
      "tg_username": "user1",
      "bio": "User 1's bio.",
      "has_telegram_premium": true,
      "is_pro_user": false,
      "user_type": "1",
      "status": "1",
      "interested_in": "1",
      "gender": {
        "id": 2,
        "name": "Female"
      },
      "photos": [
        "https://example.com/photo1.jpg"
      ],
      "liked_you": false
    },
    {
      "id": 5,
      "name": "User 2",
      "tg_id": "2345678901",
      "age": "26",
      "tg_username": "user2",
      "bio": "User 2's bio.",
      "has_telegram_premium": false,
      "is_pro_user": false,
      "user_type": "1",
      "status": "1",
      "interested_in": "1",
      "gender": {
        "id": 2,
        "name": "Female"
      },
      "photos": [
        "https://example.com/photo2.jpg"
      ],
      "liked_you": false
    }
  ],
  "current_page": 1,
  "per_page": 15,
  "total": 4,
  "has_next_page": false
}
```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```


### Like User Profiles

**Endpoint:** `{{BASE_URL}}/api/like`

**HTTP Method:** POST

**Request:**

```http
POST {{LOCAL_BASE_URL}}/api/like HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer your_access_token_here

{
  "user_id": 5
}
```

**Response - 201 Created:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "success": true,
    "message": "Like stored"
}
```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```


### Dislike User Profiles

**Endpoint:** `{{BASE_URL}}/api/dislike`

**HTTP Method:** POST

**Request:**

```http
POST {{LOCAL_BASE_URL}}/api/like HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer your_access_token_here

{
  "user_id": 5
}
```

**Response - 201 Created:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "success": true,
    "message": "Dislike stored"
}
```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```

### Fetch Matched Users

**Endpoint:** `{{BASE_URL}}/api/matches`

**HTTP Method:** GET

**Request:**

```http
GET {{BASE_URL}}/api/matches HTTP/1.1
Host: api.example.com
Authorization: Bearer your_access_token_here
```

**Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "matches": [
        {
            "id": 1,
            "name": "Matched User 1",
            "tg_id": "1234567890",
            "age": "30",
            "tg_username": "matcheduser1",
            "bio": "Matched User 1's bio.",
            "photos": [
                "https://example.com/photo1.jpg"
            ],
            "has_telegram_premium": false,
            "is_pro_user": false,
            "user_type": "1",
            "status": "1",
            "gender_id": "1",
            "interested_in": "2",
            "match_id": 1,
            "gender": {
                "id": 1,
                "name": "Male"
            }
        }
    ]
}
```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```

### Unmatch with Users

**Endpoint:** `{{BASE_URL}}/api/unmatch`

**HTTP Method:** POST

**Request:**

```http
POST {{BASE_URL}}/api/unmatch HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "match_id": 1
}
```


**Response - 200 OK:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "message": "User unmatched"
}
```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```


### Generate Telegram Payment URL

**Endpoint:** `{{BASE_URL}}/api/generate-invoice`

**HTTP Method:** POST

**Request:**

```http
POST {{BASE_URL}}/api/generate-invoice HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer your_access_token_here
```

**Response - 200 OK:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "payment_url": "https://t.me/$b-CO6OVZKasdfOAQAAh90_Wiu8I0A",
    "message": "Payment invoice generated"
}

```

**Response - 401 Unauthorized:**

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "message": "Unauthenticated."
}

```

### Fetch App Metadata

**Endpoint:** `{{BASE_URL}}/api/app-metas`

**HTTP Method:** GET

**Request:**

```http
GET {{BASE_URL}}/api/app-metas HTTP/1.1
Host: api.example.com
```

**Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "genders": [
            {
                "id": 1,
                "name": "Male"
            },
            {
                "id": 2,
                "name": "Female"
            }
        ],
        "interests": [
            {
                "id": 1,
                "name": "Hiking"
            },
            {
                "id": 2,
                "name": "Reading"
            }
        ],
        "relationship_types": [
            {
                "id": 1,
                "name": "Friendship"
            },
            {
                "id": 2,
                "name": "Marriage"
            }
        ]
    }
}
```


