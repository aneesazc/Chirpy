# Chirpy

Chirpy is a simple RESTful web service built with Go, providing endpoints for user authentication, chirp management, and more. The project uses JWT for authentication and includes features such as sorting and filtering chirps.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Configuration](#configuration)

## Features

- User authentication with JWT
- Create, retrieve, and delete chirps
- Filter chirps by author
- Sort chirps by ID in ascending or descending order
- Refresh tokens for extended sessions

## Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/aneesazc/chirpy.git
   cd chirpy-api
   ```

2. Install dependencies:

   ```sh
   go mod download
   ```

3. Build the project:
   ```sh
   go build
   ```

## Usage

1. Run the server:

   ```sh
   ./chirpy
   ```

2. The API server will start on `http://localhost:8080`.

## Example Usage of the APIs

- **POST /api/login**

  Request:

  ```json
  {
    "email": "lane@example.com",
    "password": "04234"
  }
  ```

  Response:

  ```json
  {
    "id": 1,
    "email": "lane@example.com",
    "token": "access_token",
    "refresh_token": "refresh_token"
  }
  ```

### Chirps

- **GET /api/chirps**

  Query Parameters:

  - `author_id` (optional): Filter chirps by author ID
  - `sort` (optional): Sort chirps by ID (`asc` or `desc`)

  Response:

  ```json
  [
    {
      "id": 1,
      "author_id": 1,
      "body": "This is a chirp"
    },
    {
      "id": 2,
      "author_id": 2,
      "body": "Another chirp"
    }
  ]
  ```

- **DELETE /api/chirps/{chirpID}**

  Headers:

  - `Authorization: Bearer <token>`

  Response:

  - `204 No Content` on success
  - `403 Forbidden` if the user is not the author of the chirp
  - `401 Unauthorized` if the token is invalid or missing

## API Endpoints

- **Static File Server**

  - `GET /app/*`: Serves static files from the `app` directory.

- **Health and Reset**

  - `GET /api/healthz`: Check the health of the API.
  - `GET /api/reset`: Reset the application state.

- **Webhooks**

  - `POST /api/polka/webhooks`: Handle Polka webhooks.

- **Authentication**

  - `POST /api/revoke`: Revoke a token.
  - `POST /api/refresh`: Refresh a token.
  - `POST /api/login`: User login.

- **User Management**

  - `POST /api/users`: Create a new user.
  - `PUT /api/users`: Update an existing user.

- **Chirps Management**

  - `DELETE /api/chirps/{chirpID}`: Delete a chirp.
  - `POST /api/chirps`: Create a new chirp.
  - `GET /api/chirps`: Retrieve chirps.
  - `GET /api/chirps/{chirpID}`: Get a specific chirp.

- **Metrics**
  - `GET /admin/metrics`: Retrieve API metrics.

## Configuration

- **JWT Secret**: Set your JWT secret in the `apiConfig` struct.
- **Database**: Currently, the database is an in-memory map. Adjust the `DB` struct as needed for persistent storage.
