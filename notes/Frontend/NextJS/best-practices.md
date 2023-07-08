# UI Libraries

- [shadcn/ui](https://ui.shadcn.com/docs/installation/next)
- [radix-ui](https://www.radix-ui.com/)

# UI components

- toast message: [react-hot-toast](https://react-hot-toast.com/)

# Validator

- [zod validator](https://zod.dev/)

# State management:

- [zustand](https://github.com/pmndrs/zustand)
  
# Cloud Serverless Providers

- [supabase](https://supabase.com/)
- [planetscale](https://app.planetscale.com/)

# Authentication service and user management

- [clerk](https://clerk.com/)

# Database connection provider

### [prisma](https://www.prisma.io/)

#### Usage

- install: ```npm i -D prisma``` ```npm i @prisma/client```
- init: ```npx primsa init```
```ts
// lib/prisma.ts

import { PrismaClient } from "@prisma/client";

declare global {
    var prisma: PrismaClient | undefined;
}

const prismadb = globalThis.prisma || new PrismaClient();

if (process.env.NODE_ENV !== "production")
    globalThis.prisma = prismadb;

export default prismadb;
```
- set the ```DATABASE_URL``` in the ```.env``` file
- set the preferd settings in the ```schema.prisma``` in the ```datasource db``` section
- make models
```prisma
// example

model Store {
  id        String   @id @default(uuid())
  name      String
  userId    String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```
