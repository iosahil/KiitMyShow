# KiitMyShow: Movie booking web-app
This is our K-Explore Web Designing Group Project for [KIIT University]([url](https://kiit.ac.in/)).

> [!NOTE]
> This repository current mainly aims to focus on the backend part.
> For the frontend part, refer to: [Link](https://github.com/naitik7475/KiitMyShow)

## Tech Stack
- [NodeJS](https://nodejs.org/en): Backbone of backend
- [Fly.io](https://fly.io/): Hosting & deployment
- [ImageKit](https://imagekit.io/): Image CDN
- [Auth0](https://auth0.com/): For Authentication
- [MailGun](https://www.mailgun.com/): To send mail
- <details>
  <summary>Azure Serverless SQL: Since its free & usable</summary>
  <img src="https://github.com/user-attachments/assets/48868375-e814-4ce2-b23f-c0a144eb5347" alt="Azure SQL">
</details>

## Basics Knowledge
- Two Users: _Admin_ & _Customer_
- _Admin_: Able to CRUD movies and theatres, read transactions, read stats.
- _Customer_: Able to search, sort, filter, check movies & theatre based on their location. They would be able to read their transactons and download or cancel their tickets.
- Transaction Control of all seat booking must be considered to prevent conflicts.

## Extras
- Using [Unofficial IMdB API to get Movies records](https://imdb.iamidiotareyoutoo.com/docs/index.html#tag/default/GET/search)

## Data Model
### ER Diagram
![image](https://github.com/user-attachments/assets/1a9e41c8-4b63-4d91-9370-e4a37f920ab4)

### SQL Query
  ```sql
CREATE TABLE Movie
(
    id           INT PRIMARY KEY UNIQUE,
    name         VARCHAR NOT NULL,
    duration     INT     NOT NULL,
    genre        VARCHAR,
    imdb_id      VARCHAR,
    trailer_link VARCHAR,
    poster_link  VARCHAR
);

CREATE TABLE Cinema
(
    id    INT PRIMARY KEY UNIQUE,
    name  VARCHAR NOT NULL,
    city  VARCHAR NOT NULL,
    state VARCHAR NOT NULL
);

CREATE TABLE Halls
(
    id          INT PRIMARY KEY UNIQUE,
    name        VARCHAR NOT NULL,
    cinema_id   INT     NOT NULL,
    hall_number INT     NOT NULL,
    capacity    INT     NOT NULL,
    FOREIGN KEY (cinema_id) REFERENCES Cinema (id)
);

CREATE TABLE Shows
(
    id          INT PRIMARY KEY UNIQUE,
    lang        VARCHAR   NOT NULL,
    movie_id    INT       NOT NULL,
    hall_id     INT       NOT NULL,
    start_time  TIMESTAMP NOT NULL,
    tier1_price INT       NOT NULL,
    tier2_price INT       NOT NULL,
    tier3_price INT       NOT NULL,
    FOREIGN KEY (movie_id) REFERENCES Movie (id),
    FOREIGN KEY (hall_id) REFERENCES Halls (id)
);

CREATE TABLE Users
(
    id              INT PRIMARY KEY UNIQUE,
    name            VARCHAR NOT NULL,
    email           VARCHAR NOT NULL UNIQUE,
    hashed_password VARCHAR NOT NULL,
    role            VARCHAR NOT NULL
);

CREATE TABLE ReservedSeats
(
    id          INT PRIMARY KEY UNIQUE,
    seat_number INT       NOT NULL,
    show_id     INT       NOT NULL,
    user_id     INT       NOT NULL,
    reserved_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    expires_at  TIMESTAMP NOT NULL,
    FOREIGN KEY (show_id) REFERENCES Shows (id),
    FOREIGN KEY (user_id) REFERENCES Users (id)
);

CREATE TABLE Booking
(
    id           INT PRIMARY KEY,
    seat_number  INT       NOT NULL,
    show_id      INT       NOT NULL,
    user_id      INT       NOT NULL UNIQUE,
    booking_time TIMESTAMP NOT NULL,
    status       VARCHAR   NOT NULL,
    amount       INT       NOT NULL,
    FOREIGN KEY (show_id) REFERENCES Shows (id),
    FOREIGN KEY (user_id) REFERENCES Users (id)
);
  ```

