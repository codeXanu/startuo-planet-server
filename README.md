# Startup Planet Server

**An Express.js backend API providing rich startup data filtering and querying capabilities.**

This project serves a curated dataset of the world’s most promising startups with powerful filtering via query parameters and path params.

## Table of Contents

- [Features](#features)
- [Folder Structure](#folder-structure)
- [Requirements](#requirements)
- [Setup \& Installation](#setup--installation)
- [Environment Variables](#environment-variables)
- [Running the Server](#running-the-server)
- [API Endpoints](#api-endpoints)
- [Sample Requests \& Responses](#sample-requests--responses)
- [Technologies Used](#technologies-used)
- [Author](#author)
- [License](#license)


## Features

- Serve comprehensive dataset of startups including details such as location, founders, employees, industry, funding status, and MVP availability.
- Filter startups dynamically by query parameters: `industry`, `country`, `continent`, `is_seeking_funding`, `has_mvp`.
- Search startups by path parameters limited to `country`, `continent`, or `industry`.
- CORS enabled for cross-origin support.
- Robust 404 error handling for unknown routes.


## Folder Structure

```
startup-planet-server/
│
├── controllers/
│   ├── getAllData.js           
│   └── getDataByPathParams.js 
├── data/
│   └── data.js                 
├── node_modules/
├── routes/
│   └── apiRoutes.js            
├── package-lock.json
├── package.json
└── server.js                 
```


## Requirements

- Node.js v18 or above (for native ES modules support)
- npm (Node package manager)


## Setup \& Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/startup-planet-server.git
cd startup-planet-server
```

2. **Install dependencies**
```bash
npm install
```


## Environment Variables

> No special environment variables are required for this project as per the current setup.

## Running the Server

Start the server on port 8000 (default):

```bash
npm start
```

Server log example:

```
The server is connected on the port 8000
```


## API Endpoints

### 1. `GET /api/`

Returns the full startup dataset, optionally filtered by query parameters:

**Query Parameters:** (all optional)


| Parameter | Type | Description |
| :-- | :-- | :-- |
| `industry` | string | Filter startups by industry (case-insensitive) |
| `country` | string | Filter startups by country (case-insensitive) |
| `continent` | string | Filter startups by continent (case-insensitive) |
| `is_seeking_funding` | boolean | Filter startups by funding seeking status (`true` or `false`) |
| `has_mvp` | boolean | Filter startups by whether they have a Minimum Viable Product (MVP) (`true` or `false`) |

**Example:**
`GET /api?industry=AI&country=USA&is_seeking_funding=true`

### 2. `GET /api/:field/:term`

Search startups by a specific field and term.

- `field` - Must be one of: `country`, `continent`, `industry`.
- `term` - The exact value to filter by (case-insensitive).

**Example:**
`GET /api/country/Australia`

**Invalid fields** will result in `400 Bad Request`.

## Sample Requests \& Responses

### Example 1: Filter startups by query parameters

**Request:**
`GET /api?industry=AI&is_seeking_funding=true`

**Response:** (JSON array of startups matching filters)

```json
[
  {
    "id": 1,
    "name": "TechNova AI",
    "industry": "AI",
    "founded": 2021,
    "country": "USA",
    "continent": "North America",
    "business_address": {
      "street": "123 Innovation Drive",
      "city": "San Francisco",
      "state": "California"
    },
    "founders": [
      { "name": "Emma Richardson", "role": "CEO" },
      { "name": "Liam Patel", "role": "CTO" }
    ],
    "employees": 50,
    "website": "https://www.technova.ai",
    "mission_statement": "Empowering businesses with cutting-edge AI-driven solutions.",
    "description": "TechNova AI specializes in developing machine learning models for predictive analytics, customer insights, and automation.",
    "is_seeking_funding": true,
    "has_mvp": true
  }
]
```


### Example 2: Search startups by path params

**Request:**
`GET /api/continent/Europe`

**Response:** (JSON array of startups in Europe)

```json
[
  {
    "id": 2,
    "name": "GreenGrid Energy",
    "industry": "Renewable Energy",
    "founded": 2018,
    "country": "Germany",
    "continent": "Europe",
    "business_address": {
      "street": "45 Solar Avenue",
      "city": "Berlin",
      "state": "Berlin"
    },
    "founders": [{ "name": "Hans Müller", "role": "CEO" }],
    ...
  },
  ...
]
```


### Error Response Example for Invalid Field

```json
{
  "message": "Search field not allowed. Please use only 'country', 'continent', 'industry'"
}
```

Status code: 400 Bad Request.

## Technologies Used

- [Node.js](https://nodejs.org/)
- [Express.js 5](https://expressjs.com/)
- [CORS](https://www.npmjs.com/package/cors)
- ES Modules with native `import` syntax


## Author

[codexAnuj](https://github.com/codexanu)

## License

ISC

**Feel free to contribute, report issues, or suggest features!**


