# Drizzle ORM and PosgreSQL

> The examples made under docker environment with NextJS
> 

## Install packages

- `pnpm add drizzle-orm pg postgres dotenv dotenv-expand`
- `pnpm add -D @types/pg drizzle-kit esbuild-register`

## Create env file

```env
ENV_TYPE=dev | prod
POSTGRES_DB=my-db-${ENV_TYPE}
POSTGRES_USER=my-db-${ENV_TYPE}
POSTGRES_PASSWORD=1234
POSTGRES_INTERNAL_PORT=5432
POSTGRES_EXTERNAL_PORT=5432

DATABASE_EXTERNAL_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:${POSTGRES_EXTERNAL_PORT}/${POSTGRES_DB}?schema=public
DATABASE_INTERNAL_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@database:${POSTGRES_INTERNAL_PORT}/${POSTGRES_DB}?schema=public
```

## Setup migration

### Folder structure

- `db/migrations`

### Create `migrate.ts`

```ts
import "dotenv/config";
import "dotenv-expand/config";
import { Pool } from "pg";
import { drizzle } from "drizzle-orm/node-postgres";
import { migrate } from "drizzle-orm/node-postgres/migrator";

const pool = new Pool({
  connectionString: process.env.DATABASE_EXTERNAL_URL,
});

const db = drizzle(pool);

async function main() {
  console.log("Running migrations...");
  await migrate(db, { migrationsFolder: "db/migrations" });
  console.log("Migrations completed!");
  process.exit(0);
}

main().catch((err) => {
  console.log(err);
  process.exit(0);
});
```

### Create scripts to the `package.json`
```json
...

"migration:generate": "drizzle-kit generate:pg --schema=./db/schemas index.ts --out=./db/migrations",
"migration:deploy": "node -r esbuild-register ./db/migrate.ts",
"migrate": "pnpm migration:generate && pnpm migration:deploy"

...
```

## Schemas

### Folder sturcture

- `db/schemas/index.ts` (barrel export all schema)
```ts
// export all the users related schemas
export * from "./users";
```

### Data types in PostgreSQL

#### Numeric data types

- **Integer**
  - Signed 4 bytes
  - 1 bit is set aside for SIGN
  - Ranges from -2<sup>31</sup> to -2<sup>31</sup>
  - -2,147,483,648 to 2,147,483,647
```ts
// example
import { pgTable, integer } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    qty: integer("qty")
})
```
- **Smallint**
  - Signed 2 bytes
  - 1 bit is set aside for SIGN
  - Ranges from -2<sup>7</sup> to 2<sup>7</sup>
  - -32,768 to 32,767
```ts
// example
import { pgTable, smallint } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    qty: smallint("qty")
})
```
- **Bigint**
  - Signed 8 bytes
  - 1 bit is set aside for SIGN
  - Ranges from -2<sup>63</sup> to 2<sup>63</sup>
  - -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
```ts
// example
import { pgTable, bigint } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    qty: bigint("qty", {
            mode: "number" /* 2^31 to 2^53 */ | "bigint"
    })
})
```
- **Serial**
  - auto increment
  - serial / serial4
  - smallserial / serial2
  - bigserial / serial8
```ts
// example
import { pgTable, serial, smallserial, bigserial } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    id: serial("id"),
    smallid: smallserial("smallid"),
    bigid: bigserial("bigid", {mode: "number" | "bigint"})
})
```
- **Decimal**
  - selectable precision
  - very large number of digits
  - **131072** digits before the decimal point
  - up to **16383** after the decimal point
```ts
// example
import { pgTable, decimal, numeric } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    price: decimal("price", {
        precision: 7, // total number of digits
        scale: 2 // the number of fractional point
    }),
    // the numeric and the decimal is the same in postgres
    priceNum: numeric("priceNum", {
        precision: 7, // total number of digits
        scale: 2 // the number of fractional point
    }),
})
```
- **Real / float4**
  - Single precision floating-point number (4 bytes)
  - 1E-37 ti 1E+37
  - 6 decimal digits precision
```ts
// example
import { pgTable, real } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    score: real("score")
})
```
- **Double precision / float8**
  - Double precision floating-point number (8 bytes)
  - 1E-307 ti 1E+308
  - 15 decimal digits precision
```ts
// example
import { pgTable, double } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    score: double("score")
})
```
- **Boolean**
  - 0 / 1
  - True / False
```ts
// example
import { pgTable, boolean } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    delivered: boolean("delivered")
})
```

#### Text data types

- **Text**
  - Variable-length (unlimited) character string
```ts
// example
import { pgTable, text } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    description: text("description")
})
```
- **Varchar**
  - Variable-length charachter string, can store strings up to `n` characters (not bytes)
```ts
// example
import { pgTable, varchar } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    name: varchar("name", { length: 256 })
})
```
- **Char(n)**
  - Fixed-length
  - Blank padded character string (if the given charactres less then `n` then it will fill the rest with blank space)
  - Can store strings up to `n` characters (not bytes)
```ts
// example
import { pgTable, char } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    name: char("name", { length: 10 })
})
```

- **JSON**
  - Textual JSON data
```ts
// example
import { pgTable, json } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    data: json("data")
})
```

- **JSONB**
  - Binary JSON data, decomposed
```ts
// example
import { pgTable, jsonb } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    data: jsonb("data")
})
```

#### **DateTime Data Types**

- **Time**
  - Only time
```ts
// example
import { pgTable, time } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    startAt: time("startAt", {
        precision: 6, /* for the fractional seconds */
        withTimezone: true}).defaultNow()
})
```
- **TimeStamp**
  - Date plus time
```ts
// example
import { pgTable, timestamp } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    datetime: timestamp("datetime", {
        precision: 6, /* for the fractional seconds */
        withTimezone: true
        mode: "string" | "date" /* save as string or date type*/
    }).defaultNow()
})
```
- **Date**
  - Only date
```ts
// example
import { pgTable, date } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    date: date("date", {
        mode: "string" | "date" /* save as string or date type*/
    }).defaultNow()
})
```
- **Interval**
  - Interval of time
  - Number of milliseconds between to datetime
  - It can be store long intervals (ex.: years)
```ts
// example
import { pgTable, interval } from "drizzle-orm/pg-core";

export const testTable = pgTable("testTable", {
    date: interval("date")
})
```

#### Enum
```ts
import { pgTable, pgEnum } from "drizzle-orm/pg-core";

export const moodEnum = pgEnum("mood", ['sad','ok','happy'])
export const testTable = pgTable("testTable", {
    mood: moodEnum("mood")
})
```

### Default values
It can be chaind to each data type: 
- `.defaultNow()` (only date or time types)
- `.default("value")`
- `.notNull()`
- `.primaryKey()`
- `.references()`

## Connection to database

- `db/index.ts`:
```ts
import { drizzle } from "drizzle-orm/node-postgres";
import { Client } from "pg";
import * as schemas from "./schemas";

const client = new Client({
  connectionString: process.env.DATABASE_INTERNAL_URL,
});

client.connect();

export const db = drizzle(client, {
  schema: schemas,
});
```

- query data:
```ts
import { db } from "@/db";
import { users } from "@/db/schemas";

const result = await db.select().from(users);
```