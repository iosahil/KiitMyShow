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
