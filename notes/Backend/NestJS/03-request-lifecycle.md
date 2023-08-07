# Request lifecycle

![Alt text](./images/req-life-cycle.png)

> **More info:** https://slides.com/yariv-gilad/nest-js-request-lifecycle/fullscreen
> 
> **Official docs:** https://docs.nestjs.com/faq/request-lifecycle

## Middleware
- first station of the request lifecycle.
- can put data into the request 

```ts
// src/users/middlewares/current-user.middleware.ts

import { Injectable, NestMiddleware } from '@nestjs/common';
import { Request, Response, NextFunction } from 'express';
import { UsersService } from '../users.service';

// tell to the typescript can be a currentUser property in the Request object 
declare global {
  namespace Express {
    interface Request {
      currentUser?: User;
    }
  }
}

@Injectable()
export class CurrentUserMiddleware implements NestMiddleware {
  constructor(private usersService: UsersService) {}
  async use(req: Request, res: Response, next: NextFunction) {
    const { userId } = req.session || {};
    if (userId) {
      const user = await this.usersService.findOne(userId);
      req.currentUser = user;
    }

    next();
  }
}
```
applying in the users module
```ts
// src/users/users.module.ts
import { MiddlewareConsumer, Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersController } from './users.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './user.entity';
import { AuthService } from './auth.service';
import { CurrentUserMiddleware } from './middlewares/current-user.middleware';

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  controllers: [UsersController],
  providers: [UsersService, AuthService],
})
export class UsersModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(CurrentUserMiddleware).forRoutes('*');
  }
}
```

## Guard
- run after middlewares
- class wich implements ```CanActivate``` from ```@nestjs/common```
- required method: CanActivate
- return with boolean (can activate or not)
```ts
import { CanActivate, ExecutionContext } from '@nestjs/common';

export class AdminGuard implements CanActivate {
  canActivate(context: ExecutionContext) {
    const request = context.switchToHttp().getRequest();

    if (!request.currentUser) {
      return false;
    }

    return request.currentUser.admin;
  }
}
```

## Pipe

### ValidationPipe

- runs before controller methods
- built in NestJS
- Validating the request data

1. Tell Nest to use global validation
```ts
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { ValidationPipe } from '@nestjs/common';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(new ValidationPipe({
    whitelist: true // <--- it will filter the request with the DTO (only the declared props will be presented in the request)
  }));
  await app.listen(process.env.BACKEND_API_PORT || 5000);
}
bootstrap();
```
> If we setup Pipes like this, it will cause some issues in the e2e tests. [Check the testing section of the notes.](./09-testing.md#e2e-testing-end-to-end-testing)

2. Create a class that describes the different properties that the request body should have (Dto -> Data transfer object)
```ts
// user/dtos/create-user.dto.ts
export class CreateUserDto {
  name: string;
  // all the properties which contain in the request
}
```
3. Add validation rules to the class
    - required dependencies: ```yarn add class-validator class-transformer```
    - ```class-validator```: validate the request with classes (https://github.com/typestack/class-validator)
    - ```class-transformer```: transform request json objets to classes (https://github.com/typestack/class-transformer)

```ts
// user/dtos/create-user.dto.ts
import { IsString } from 'class-validator';

export class CreateUserDto {
  @IsString()
  name: string;
}
```
transform property:
```ts
@Transform(({ value }) => parseInt(value))
@IsNumber()
@Min(1930)
@Max(2050)
year: number;
```

4. Apply that class to the request handler
```ts
// user/user.controller.ts
import { Body, Controller, Post } from '@nestjs/common';
import { CreateUserDto } from './dtos/create-user.dto';

@Controller('user')
export class UserController {
  constructor() {}

  @Post()
  createUser(@Body() body: CreateUserDto) {
    console.log(body);
  }
}
```

## Controller

- Handle requests. 
- API end points.
- decorators tells the method type

## Service
- Business logic
- initialize in the controller constructor as arguments: ```constructor(private userService: UserService) {}```
- needed the ```@Injectable()``` decorator

## Repository
> Read and write to the database. TypeORM create automatically.