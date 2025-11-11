# Prisma - SQLite Setup & Configuration for Nextjs App

This document summarizes the **full Prisma and SQLite setup and configuration** for nextjs project. 

---

## 1. Installing and Initializing Prisma

Install Prisma and SQLite, then initialize Prisma:
```bash
npm install prisma @prisma/client
npx prisma init
```
> Creates the `prisma/` folder and `.env` file.


## 2. Configuring `.env`

If you have not a `.env` file at root folder, create a `.env` file in the project root to define the SQLite database connection:
```env
DATABASE_URL="file:./dev.db"
```
> This tells Prisma to create/use the SQLite database file `dev.db` in the `prisma/` folder.
