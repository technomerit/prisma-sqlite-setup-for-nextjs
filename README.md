# Prisma - SQLite Setup & Configuration for Nextjs App

This document summarizes the **full Prisma and SQLite setup and configuration** for nextjs project. 

---

## 1. Installing and Initializing Prisma

Install Prisma and SQLite, then initialize Prisma:
```bash
npm install prisma @prisma/client
npx prisma init --datasource-provider sqlite
```
> Creates the `prisma/` folder and `.env` file.


## 2. Configuring `.env`

If you have not a `.env` file at root folder, create a `.env` file in the project root to define the SQLite database connection:
```env
DATABASE_URL="file:./dev.db"
```
> This tells Prisma to create/use the SQLite database file `dev.db` in the `prisma/` folder.

---

## 3. Defining Prisma Models (`schema.prisma`)

Edit `prisma/schema.prisma` with your project models:
* (Sample models used here, replace them with your own projet models)

```prisma
datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  mobile    String?
  password  String
  orders    Order[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Product {
  id          Int      @id @default(autoincrement())
  name        String
  description String?
  price       Float
  imageUrl    String?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  orderItems  OrderItem[]
}

model Order {
  id        Int         @id @default(autoincrement())
  user      User        @relation(fields: [userId], references: [id])
  userId    Int
  total     Float
  createdAt DateTime    @default(now())
  updatedAt DateTime    @updatedAt
  items     OrderItem[]
}

model OrderItem {
  id        Int      @id @default(autoincrement())
  order     Order    @relation(fields: [orderId], references: [id])
  orderId   Int
  product   Product  @relation(fields: [productId], references: [id])
  productId Int
  quantity  Int      @default(1)
  price     Float
}
```
> Supports users, products, orders, and order items with relationships.

---
