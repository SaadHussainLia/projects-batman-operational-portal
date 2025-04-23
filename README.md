# Batman Operations Portal

A fun and educational web app built with **Flask**, **MySQL**, and **REST APIs**. Themed around Batman and the Gotham City Police Department, this project lets users act as Gotham's tech squad reporting incidents.

## Project Idea

You will create a full-stack application with:

- **User authentication** (login/register)
- A web interface for managing data
- A **REST API** for programmatic access
- Integration with a **third-party API**
- Batman theme :)

## Features

### Authentication
- User Registration
- User Login
- Password Hashing
- IP + location tracking using `ipapi.co`
- Location stored in database

### Incident Reporting
- Report Joker sightings, tech thefts, etc.
- Fields: `title`, `priority`, `location`, `details`
- Assign incidents to users (like Batman or Nightwing)

### Dashboard
- Logged-in users can:
- View active incidents
- Filter by status, date, or priority
- See Gotham's real-time weather using **OpenWeather API**

## REST API Endpoints

### Authentication
- `POST /api/v1/register`
- `POST /api/v1/login`

### Incidents
- `GET /api/v1/incidents` -> List all
- `GET /api/v1/incidents/<id>` -> Get single incident
- `POST /api/v1/incidents` -> Create new incident
- `PUT /api/v1/incidents/<id>` -> Update an incident
- `DELETE /api/v1/incidents/<id>` -> Delete incident

### Third-Party API Integration
- Pull real-time weather data for Gotham using the [OpenWeather API](https://openweathermap.org/api)
- Show current Gotham weather on the dashboard
- Cache weather results upto 1 hour to reduce API calls
- Pull location of user when they first register using the [IpAPI]( https://ipapi.co)
- Store the location (ipaddress, country, city) of each user in the database

## How to Use API in Postman

Each API request that modifies data (POST, PUT, DELETE) requires an **Authorization header** with a bearer token, obtained from logging in.

---

### 1. Register User  
**POST** `/api/v1/register`  
**Body (JSON)**:
```json
{
  "Username": "batman",
  "Password": "darkknight"
}
```
**Expected Result:**  
Returns success message, saves user's IP and location from [ipapi.co](https://ipapi.co) into the database.

```json
{
  "ApiHttpResponse": 201,
  "ApiMessages": "INFO - Request processed successfully",
  "ApiResult": ""
}
```
---

### 2. Login  
**POST** `/api/v1/login`  
**Body (JSON)**:
```json
{
  "Username": "batman",
  "Password": "darkknight"
}
```
**Expected Result:**  
Returns an authentication token like:
```json
{
  "Token": "eyJhbGciOi..."
}
```

---

### 3. Create an Incident Report  
**POST** `/api/v1/incidents`  
**Headers:**
```
Authorization: Bearer <your_token_here>
```
**Body (JSON):**
```json
{
  "Title": "Joker sighting",
  "Description": "Spotted near Ace Chemicals",
  "Priority": "High",
  "Location": "Gotham East"
}
```
**Expected Result:**  
Creates a new incident record and assigns it to dashboard.

```json
{
  "ApiHttpResponse": 201,
  "ApiMessages": "INFO - Request processed successfully",
  "ApiResult": ""
}
```
---

### 4. View All Incidents  
**GET** `/api/v1/incidents`  
**Headers:**
```
Authorization: Bearer <your_token_here>
```
**Expected Result:**  
Returns all incident reports accessible to the user.

```json
{
  "ApiHttpResponse": 200,
  "ApiMessages": "INFO - Request processed successfully",
  "ApiResult": [
    {
      "Id": 1,
      "Location": "Gotham Central",
      "Priority": "High",
      "Description": "Joker spotted near station",
      "Status": "Open"
    },
    {
      "Id": 2,
      "Location": "Arkham Asylum",
      "Priority": "Medium",
      "Description": "Breach reported in west wing",
      "Status": "In Progress"
    }
  ]
}
```

and so on..

## Tech Stack

- **Backend**: Python + Flask
- **Database**: MySQL
- **Frontend**: HTML/CSS/React.js
- **API**: Flask RESTful
- **External APIs**: OpenWeatherMap API + IpAPI

## Developer Tools

- **Postman** – For testing and exploring the REST API
- **MySQL Workbench** – For managing and querying the MySQL database
- **Git/GitHub** – For version control and collaboration

## Educational Value

This project helps practice:

- Flask routing & sessions
- Database schema design (MySQL)
- RESTful API principles
- Integration with third-party APIs
- Authentication & security best practices

---

Remember your code will help keep Gotham safe.