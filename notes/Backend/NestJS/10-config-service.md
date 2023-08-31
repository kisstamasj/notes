# NestJS Config Service

- install: ```npm i @nestjs/config```
- read env files
- expose all of the env variables to the whole application
- env for development: ```.env.development```
- env for testing: ```.env.test```
- Config module and TypeORM together:
```ts
// app.module.ts
import { ConfigModule, ConfigService } from '@nestjs/config';

import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ReportsModule } from './reports/reports.module';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './users/user.entity';
import { Report } from './reports/report.entity';
import { ConfigModule, ConfigService } from '@nestjs/config';

@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true,
      envFilePath: `.env.${process.env.NODE_ENV}`,
    }),
    UsersModule,
    ReportsModule,
    TypeOrmModule.forRootAsync({
      inject: [ConfigService],
      useFactory: (config: ConfigService) => {
        return {
          type: 'sqlite',
          database: config.get<string>('DB_NAME'),
          synchronize: true,
          entities: [User, Report],
        };
      },
    }),
  ],
  controllers: [ AppController ],
  providers: [ AppService ],
})
export class AppModule {}
```
- for running applicaion in different mode (test, development):
    - install: ```npm install cross-env```
    - update package.json scripts:
    ```json
    "start": "cross-env NODE_ENV=development nest start",
    "start:dev": "cross-env NODE_ENV=development nest start --watch",
    "start:debug": "cross-env NODE_ENV=development nest start --debug --watch",

    "test": "cross-env NODE_ENV=test jest",
    "test:watch": "cross-env NODE_ENV=test jest --watch --maxWorkers=1",
    "test:cov": "cross-env NODE_ENV=test jest --coverage",
    "test:debug": "cross-env NODE_ENV=test node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "cross-env NODE_ENV=test jest --config ./test/jest-e2e.json"
    ```
 - validate env file content with ```joi```
    - install: ```npm i joi```
    - usage:
     ```ts
      import { Module } from '@nestjs/common';
      import { ConfigService, ConfigModule as NestConfigModule } from '@nestjs/config';
      import * as Joi from 'joi';
      
      @Module({
          imports: [NestConfigModule.forRoot({
              validationSchema: Joi.object({
                  MONGODB_URI: Joi.string()
              })
          }) ],
          providers: [ConfigService],
          exports: [ConfigService]
      })
      export class ConfigModule {}
     ```
