# Cookie session

- install: ```npm install cookie-session @types/cookie-session```
- register in the ```main.ts``` as a middleware
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { ValidationPipe } from '@nestjs/common';

const cookieSession = require('cookie-session');

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  // here
  app.use(
    cookieSession({
      keys: ['asd123'],
    }),
  );
  //
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
    }),
  );
  await app.listen(3000);
}
bootstrap();
```
- signin method with cookie session
```ts
import {  Session } from '@nestjs/common';

...

@Post('/signin')
async signin(@Body() body: CreateUserDto, @Session() session: any) {
    const user = await this.authService.signin(body.email, body.password);
    session.userId = user.id;
    return user;
}
```

- signout with cookie session
```ts
@Post('/signout')
async signout(@Session() session: any) {
    session.userId = null;
}
```