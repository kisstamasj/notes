## NestJS Decorators

[More about EcmaScript decorators](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841)

## Controller

- ```@Controller('controller-name')```

```ts
import { Controller} from '@nestjs/common';

@Controller('users')
export class UserController {}
```

## Services

- ```@Injectable()```
- you can inject to other classes with dependency injection
  
```ts
//user/user.service.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class UserService {}
```

Dependency injection (Inversion Control!!!)
```ts
//user/user.controller.ts
import { Controller } from '@nestjs/common';
import { UserService } from './user.service';

@Controller('user')
export class UserController {
  constructor(private userService: UserService) {}
}
```

### DI container (Dependency Injection Container)
Holds on all of the class instances.

## Routing

> IF the decorator doesn't get prameter then it will apply as root rout. Example.: ```http://localhost:5000/users```

- ```@Get('route')```

```ts
@Get()
findAll() {
    ...
}
```

- ```@Post('route')```

```ts
@Post()
createUser() {
    ...
}
```

- ```@Put('route')```

```ts
@Put()
updateUser() {
    ...
}
```

- ```@Delete('route')```

```ts
@Delete()
updateUser() {
    ...
}
```

## Argument decorators

- ```@Param()```

```ts
// user/:id
@Get(':id')
findOne(@Param('id') id:string) {
    ...
}
```

- ```@Query()```

```ts
// /user?name=test
@Get()
findOne(@Query('name') name:string) {
    ...
}
```

- ```@Body()```

```ts
// /user
@Post()
createUser(@Body() body:ItShouldBeDTO) {
    ...
}
```

## Custom param decorator

```ts
import { createParamDecorator, ExecutionContext } from '@nestjs/common';

export const CurrentUser = createParamDecorator(
  (data: never, context: ExecutionContext) => {},
);
```
- ```data```: incoming data with param in the decorator (if type is never then is tell us we dont give any parameter for the decorator)
- ```context```: incoming request (http, websocket, grpc etc..)
- we can not use dependency injection inside a param decorator (such as services)
- interceptors are part of the dependency injection system