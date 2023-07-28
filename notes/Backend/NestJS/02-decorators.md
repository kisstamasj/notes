## NestJS Decorators

## Controller

- ```@Controller('controller-name')```

```ts
import { Controller} from '@nestjs/common';

@Controller('users')
export class UserController {}
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

## Attribute decorators

- ```@Param()```

```ts
// user/:id
@Get(':id')
async findOne(@Param() id:string) {
    return await this.userService.findAllUsers();
}
```

- ```@Query()```

```ts
// user?name=test
@Get()
async findOne(@Query() name:string) {
    return await this.userService.findAllUsers();
}
```
  