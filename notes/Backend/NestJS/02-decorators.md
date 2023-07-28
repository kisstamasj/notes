## NestJS Decorators

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

Dependency injection
```ts
//user/user.controller.ts
import { Controller } from '@nestjs/common';
import { UserService } from './user.service';

@Controller('user')
export class UserController {
  constructor(private userService: UserService) {}
}
```

## Routing

> IF the decorator doesn't get prameter then it will apply as root rout. Example.: ```http://localhost:5000/users```

- ```@Get('route')```

```ts
@Get()
async findAll() {
    return await this.userService.findAllUsers();
}
```

- ```@Post('route')```

```ts
@Post()
async createUser() {
    return await this.userService.createUser();
}
```

- ```@Put('route')```

```ts
@Put()
async updateUser() {
    return await this.userService.updateUser();
}
```

- ```@Delete('route')```

```ts
@Delete()
async updateUser() {
    return await this.userService.updateUser();
}
```

## Argument decorators

- ```@Param()```

```ts
// user/:id
@Get(':id')
async findOne(@Param('id') id:string) {
    return await this.userService.findAllUsers();
}
```

- ```@Query()```

```ts
// user?name=test
@Get()
async findOne(@Query() query:any) {
    return await this.userService.findAllUsers();
}
```

- ```@Body()```

```ts
// user?name=test
@Post()
async createUser(@Body() body:any) {
    return console.log(body)
}
```
  