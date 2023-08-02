# Guards

Guard can protect endpoints of the controllers.

## Example for checking the user is authenticated:
```ts
// src/guards/auth.guard.ts
import { CanActivate, ExecutionContext } from '@nestjs/common';

export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext) {
    const request = context.switchToHttp().getRequest();

    return request.session.userId;
  }
}
```

## Usage in controller
```ts
import { Get, UseGuards } from '@nestjs/common';
import { AuthGuard } from 'src/guards/auth.guard';
import { CurrentUser } from './decorators/current-user.decorator';

...

@Get('/whoami')
@UseGuards(AuthGuard)
whoAmI(@CurrentUser() user: User) {
    return user;
}

...
```
